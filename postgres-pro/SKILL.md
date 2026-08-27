---
name: "postgres-pro"
description: "PostgreSQL进阶诊断与性能优化：慢查询分析、EXPLAIN解读、索引调优、连接池管理、VACUUM与膨胀诊断、锁与阻塞分析、分区表策略。当用户说'Postgres'、'PostgreSQL'、'慢查询'、'EXPLAIN'、'索引优化'、'数据库性能'、'连接池'、'VACUUM'、'锁分析'、'pg_stat'、'查询优化'、'SQL优化'时触发。核心特点：从现象到根因的完整诊断链路、可落地的优化方案、与数据库设计和系统化调试联动。"
---

> **来源**: crystaldba/postgres-mcp + PostgreSQL 官方文档 + 社区性能优化实践
>
> **发布时间**: 2026-08
>
> **理念**: "慢查询不是病，查不出根因才是病。"

# 🐘 Postgres Pro — PostgreSQL 进阶诊断与性能优化

把 PostgreSQL 运行时的慢查询、索引失效、连接打满、锁冲突、表膨胀等问题，转化为可复现、可验证、可落地的诊断与优化方案。

---

## 核心诊断工作流：SEE → EXPLAIN → FIX → VERIFY

```
发现症状 (Slow Query / 高 CPU / 连接打满)
    │
    ▼
收集证据 (pg_stat_statements / pg_stat_activity / 日志)
    │
    ▼
定位根因 (EXPLAIN ANALYZE / 锁分析 / 索引检查)
    │
    ▼
制定优化 (索引 / 改写 SQL / 参数调优 / 架构调整)
    │
    ▼
验证效果 (执行计划 / 基准测试 / 监控对比)
```

---

## Step 1：发现慢查询

### 启用 pg_stat_statements

```sql
-- postgresql.conf
shared_preload_libraries = 'pg_stat_statements'
pg_stat_statements.track = all
pg_stat_statements.max = 10000
```

### Top 慢查询清单

```sql
SELECT
  query,
  calls,
  mean_exec_time,
  total_exec_time,
  rows,
  100.0 * shared_blks_hit / nullif(shared_blks_hit + shared_blks_read, 0) AS hit_percent
FROM pg_stat_statements
ORDER BY total_exec_time DESC
LIMIT 10;
```

---

## Step 2：EXPLAIN 解读

### 基础执行计划

```sql
EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON)
SELECT * FROM orders WHERE user_id = 123 AND created_at > '2024-01-01';
```

### 关键字段含义

| 字段 | 含义 | 关注信号 |
|------|------|---------|
| **Seq Scan** | 全表扫描 | 大表上出现 = 需要索引 |
| **Index Scan** | 索引扫描 | 好，但注意回表成本 |
| **Index Only Scan** | 覆盖索引扫描 | 最优，不需要回表 |
| **Nested Loop** | 嵌套循环 | 小数据集适合，大数据集危险 |
| **Hash Join** | 哈希连接 | 通常比 Nested Loop 快 |
| **Merge Join** | 归并连接 | 有序数据效率高 |
| **Buffers: shared hit/read** | 缓冲命中/读取 | read 过高说明缓存不足或扫描范围大 |
| **Planning Time / Execution Time** | 计划/执行耗时 | Planning 高可能参数过多 |

### 常见问题速查

```
Seq Scan on 大表        → 加索引
Bitmap Heap Scan + Recheck Cond  → 索引不够精准，考虑复合索引
Sort (cost=...)         → 考虑 ORDER BY 索引
HashAggregate           → 小数据集 OK，大数据集考虑部分聚合
Parallel Seq Scan       → 可能没问题，确认是否必要
```

---

## Step 3：索引调优

### 索引类型选择

| 类型 | 适用场景 | 示例 |
|------|---------|------|
| **B-tree** | 等值、范围、排序（默认） | `WHERE id = 1`、`ORDER BY created_at` |
| **GIN** | JSONB、数组、全文检索 | `WHERE data @> '{"tag": "vip"}'` |
| **GiST** | 地理空间、范围类型 | PostGIS、tsrange |
| **BRIN** | 大表、自然有序列 | 时序数据按时间分区 |
| **Hash** | 仅等值且不可排序 | 很少用，B-tree 通常更好 |

### 复合索引设计原则

```sql
-- 等值条件在前，范围条件在后
CREATE INDEX idx_orders_user_created
  ON orders (user_id, created_at DESC);

-- 覆盖索引：INCLUDE 避免回表
CREATE INDEX idx_orders_user_status
  ON orders (user_id) INCLUDE (status, total_amount);
```

**原则**：
1. 等值查询列放最前面
2. 范围查询列放后面
3. 高选择性列优先
4. 用 `INCLUDE` 实现 Index Only Scan
5. 定期清理重复/未使用索引

### 找出未使用索引

```sql
SELECT
  schemaname,
  relname AS table_name,
  indexrelname AS index_name,
  idx_scan,
  pg_size_pretty(pg_relation_size(indexrelid)) AS index_size
FROM pg_stat_user_indexes
WHERE idx_scan = 0
  AND indexrelname NOT LIKE 'pg_toast%'
ORDER BY pg_relation_size(indexrelid) DESC;
```

---

## Step 4：连接池与并发

### 连接数诊断

```sql
-- 当前连接状态
SELECT state, COUNT(*) FROM pg_stat_activity GROUP BY state;

-- 等待锁的连接
SELECT * FROM pg_stat_activity WHERE wait_event_type = 'Lock';
```

### 推荐架构

```
应用 → pgBouncer (transaction pool) → PostgreSQL
```

**pgBouncer 核心配置**：
```ini
[databases]
mydb = host=localhost port=5432 dbname=mydb

[pgbouncer]
pool_mode = transaction
max_client_conn = 10000
default_pool_size = 25
reserve_pool_size = 5
```

**黄金规则**：
- 应用直接连接数不超过 `max_connections` 的 70%
- 长事务/长连接用 session pool，短连接用 transaction pool
- 避免在事务中做网络 I/O

---

## Step 5：VACUUM 与表膨胀

### 膨胀诊断

```sql
-- 查看膨胀最严重的表
SELECT
  schemaname,
  relname,
  n_dead_tup,
  n_live_tup,
  ROUND(100.0 * n_dead_tup / NULLIF(n_live_tup + n_dead_tup, 0), 2) AS dead_ratio
FROM pg_stat_user_tables
WHERE n_live_tup > 10000
ORDER BY dead_ratio DESC
LIMIT 20;
```

### 维护策略

| 操作 | 作用 | 注意事项 |
|------|------|---------|
| **VACUUM** | 回收死元组空间 | 不会释放磁盘空间，只标记可重用 |
| **VACUUM FULL** | 彻底整理并释放空间 | 会锁表，生产慎用 |
| **ANALYZE** | 更新统计信息 | 大量数据变更后必做 |
| **REINDEX** | 重建索引 | 索引膨胀严重时使用 |

**自动维护配置**：
```sql
-- 启用自动 vacuum
autovacuum = on
autovacuum_vacuum_scale_factor = 0.1
autovacuum_analyze_scale_factor = 0.05

-- 大表单独配置更积极的 vacuum
ALTER TABLE large_table SET (
  autovacuum_vacuum_scale_factor = 0.02,
  autovacuum_analyze_scale_factor = 0.01
);
```

---

## Step 6：锁与阻塞分析

### 实时锁冲突

```sql
-- 查看被阻塞的查询
SELECT
  blocked_locks.pid AS blocked_pid,
  blocked_activity.usename AS blocked_user,
  blocking_locks.pid AS blocking_pid,
  blocking_activity.usename AS blocking_user,
  blocked_activity.query AS blocked_query,
  blocking_activity.query AS blocking_query
FROM pg_catalog.pg_locks blocked_locks
JOIN pg_catalog.pg_stat_activity blocked_activity ON blocked_activity.pid = blocked_locks.pid
JOIN pg_catalog.pg_locks blocking_locks ON blocking_locks.locktype = blocked_locks.locktype
  AND blocking_locks.relation = blocked_locks.relation
  AND blocking_locks.pid != blocked_locks.pid
JOIN pg_catalog.pg_stat_activity blocking_activity ON blocking_activity.pid = blocking_locks.pid
WHERE NOT blocked_locks.granted;
```

**常见锁问题**：
- `ACCESS EXCLUSIVE`：ALTER TABLE、DROP INDEX、VACUUM FULL
- `ROW SHARE` + `ACCESS EXCLUSIVE` 冲突：长事务阻塞 DDL
- 解决方案：低峰期 DDL、在线改表工具 `pg_repack`/`pt-online-schema-change`

---

## Step 7：分区表策略

### 何时分区

| 条件 | 建议 |
|------|------|
| 单表 > 1 亿行 | 考虑分区 |
| 时序/日志数据 | 按时间范围分区 |
| 需要按地区/租户隔离 | 按 LIST 分区 |
| 历史数据频繁删除 | 分区可快速 DROP |

### 声明式分区示例

```sql
CREATE TABLE events (
  id bigint,
  event_time timestamptz NOT NULL,
  data jsonb
) PARTITION BY RANGE (event_time);

CREATE TABLE events_2024_q1
  PARTITION OF events
  FOR VALUES FROM ('2024-01-01') TO ('2024-04-01');
```

---

## 监控指标清单

| 指标 | 告警阈值建议 |
|------|-------------|
| QPS / TPS | 建立基线 |
| 平均查询耗时 | 较基线增长 50% |
| 连接数使用率 | > 80% |
| 缓存命中率 | < 95% |
| 死元组比例 | > 20% |
| 锁等待数量 | > 0 持续 30s |
| WAL 生成速率 | 突增 3 倍以上 |
| 磁盘 I/O 延迟 | > 10ms |

---

## 快速入口

```
"这条 SQL 为什么慢"              → EXPLAIN ANALYZE 解读
"怎么加索引"                     → 复合索引 / 覆盖索引设计
"连接数打满了"                   → pg_stat_activity + pgBouncer 诊断
"表膨胀了怎么办"                 → VACUUM / REINDEX / pg_repack
"锁住了怎么查"                   → 锁冲突查询 + 处理建议
"大表怎么优化"                   → 分区表 + 索引 + 查询改写
"PostgreSQL 性能调优"            → 全流程诊断清单
```

---

## 与其他 Skill 的关系

| Skill | 关系 | 协作场景 |
|-------|------|---------|
| **database-designer** | 前置 | 先设计规范 schema，再由 `postgres-pro` 负责运行时优化 |
| **erd-document** | 前置 | ERD 文档作为理解表关系的基础 |
| **systematic-debugging** | 方法论 | 用系统化调试方法定位慢查询根因 |
| **devops-toolchain** | 部署场景 | K8s/容器化部署 PostgreSQL 时的运维保障 |
| **api-doc-generator** | 上游 | API 性能问题常根因在于数据库查询 |
| **quality-gate** | 质量保障 | SQL 变更上线前做执行计划和索引审查 |

**最佳实践链**：
```
database-designer（schema 设计）
  → erd-document（文档化）
  → api-doc-generator（接口设计）
  → 开发实现
  → postgres-pro（慢查询诊断与索引优化）
  → quality-gate（上线前审查）
  → devops-toolchain（部署与监控）
```

---

> "PostgreSQL 是世界上最先进的开源关系型数据库，但再先进的武器也需要正确的使用姿势。性能优化的本质不是调参数，而是理解数据如何被访问。"
