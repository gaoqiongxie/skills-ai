# Hermes 经验沉淀系统

> 灵感来源：Hermes Agent（ nousresearch/hermes-agent ⭐62.8K）
> 核心：把成功的经验转化为可复用的 Skill，让 AI 越用越懂你
> 触发关键词：经验沉淀、技能积累、让AI学习、项目知识库

---

## 🌟 核心理念

**"Do it once, Automate forever"**

每次解决一个问题，就把它沉淀下来。下次遇到类似问题，AI 直接调用经验，不再重复劳动。

---

## 📁 经验沉淀目录结构

```
项目-experience/
├── README.md                 # 经验库索引
├── patterns/                 # 通用模式
│   ├── exception-handling.md    # 异常处理模式
│   ├── cache-strategy.md        # 缓存策略
│   └── api-design.md            # API 设计模式
├── snippets/                 # 代码片段库
│   ├── java/
│   │   ├── pagination.java          # 分页封装
│   │   ├── result-wrapper.java      # 统一响应封装
│   │   └── log-template.java        # 日志模板
│   └── sql/
│       ├── soft-delete.sql          # 软删除模板
│       └── audit-log.sql           # 审计日志SQL
└── rules/                    # 项目规则
    ├── naming.md                # 命名规范
    ├── git-workflow.md          # Git 工作流
    └── code-review.md           # Code Review 要点
```

---

## 📝 Pattern 模板（经验模式）

### 异常处理模式
```markdown
# 异常处理模式：XXX场景

## 问题描述
[什么情况下会出现问题]

## 解决方案
```java
// 推荐写法
try {
    // 业务逻辑
} catch (BusinessException e) {
    log.warn("业务异常：{}", e.getMessage());
    throw e;
} catch (Exception e) {
    log.error("系统异常", e);
    throw new SystemException("操作失败，请稍后重试");
}
```

## 适用场景
- 场景1
- 场景2

## 注意事项
- xxx
```

### 缓存策略模式
```markdown
# 缓存策略：XXX场景

## 数据特征
- 读多写少 / 读写相当 / 写多读少
- 数据量：xx 条
- 更新频率：xx

## 缓存方案
| 维度 | 选择 |
|------|------|
| 缓存类型 | 本地 / Redis / 多级 |
| TTL | xx 分钟 |
| 更新策略 | Cache-Aside / Write-Through |

## 代码示例
```java
@Cacheable(value = "xxx", key = "#id", unless = "#result == null")
public Xxx getById(Long id) {
    return xxxMapper.selectById(id);
}
```

## 防坑指南
- xxx
```

---

## 🔄 经验沉淀工作流

```
┌─────────────────────────────────────────────────────────┐
│                   经验沉淀四步法                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1️⃣ 识别                       2️⃣ 记录                  │
│  这个问题值得沉淀吗？              写进 patterns/          │
│  - 重复出现 ≥2次                  - 问题描述              │
│  - 解决耗时 >30分钟                - 解决方案              │
│  - 有通用性                       - 适用场景              │
│                                                         │
│  3️⃣ 抽象                       4️⃣ 复用                  │
│  提炼通用模式                     遇到类似问题时            │
│  - 去掉具体业务细节               直接调用经验              │
│  - 保留核心逻辑                   不用重新踩坑              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 📊 经验分类索引

### 按场景分类

| 场景 | Pattern 文件 | 代码片段 |
|------|-------------|---------|
| **异常处理** | exception-handling.md | - |
| **缓存** | cache-strategy.md | pagination.java |
| **API 设计** | api-design.md | result-wrapper.java |
| **数据库** | - | soft-delete.sql |
| **日志** | - | log-template.java |
| **安全** | security-rules.md | - |

### 按技术分类

| 技术栈 | 相关经验 |
|--------|---------|
| **Java/Spring** | 异常处理、缓存、事务 |
| **MySQL** | SQL 优化、索引、软删除 |
| **Redis** | 缓存策略、分布式锁 |
| **API** | 统一响应、分页、参数校验 |

---

## 🎯 快速记录模板

### 新增 Pattern
```
## [Pattern名称]

### 问题
[一句话描述问题]

### 解决
[核心解决方案]

### 示例
```[语言]
代码示例
```

### 适用
- 场景1
- 场景2

### 注意事项
- xxx
```

### 新增 Snippet
```
## [片段名称]

### 用途
[在什么地方用]

### 代码
```[语言]
代码内容
```

### 依赖
[依赖的库或配置]

### 改动记录
| 日期 | 改动 | 作者 |
|------|------|------|
| 2024-01-01 | 初始版本 | 张三 |
```

---

## 💡 经验提炼技巧

### 好的经验应该：
- ☑️ 一句话能说清楚问题
- ☑️ 有可直接复用的代码
- ☑️ 标注了适用边界
- ☑️ 注明了可能的坑

### 不值得沉淀的：
- ❌ 只用一次的临时方案
- ❌ 过于具体的业务逻辑
- ❌ 没有通用性的奇技淫巧

---

## 🔗 与其他 Skill 配合

- **memory-bank** → 项目的基础文档结构
- **karpathy-skills** → LLM 编程避坑
- **memory-system** → 缓存技术的具体实现

---

## 💬 使用方式

```
用户：帮我沉淀这次 Bug 修复的经验
助手：好的！【引导使用 Pattern 模板】

用户：我想把项目中常用的代码片段积累起来
助手：建议用 snippets/ 结构，我来帮你创建基础模板

用户：下次遇到类似问题怎么调用？
助手：【说明如何关联使用】
```
