# Hermes 经验沉淀系统

> 灵感来源：Hermes Agent（ nousresearch/hermes-agent ⭐62.8K）
> 核心：把成功的经验转化为可复用的 Skill，让 AI 越用越懂你
> 触发关键词：经验沉淀、技能积累、让AI学习、项目规则、编码规范

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
├── rules/                    # 📋 项目规则（重点）
│   ├── shared-rules.md              # 项目共享规则
│   ├── coding-standards.md         # 编码规范
│   ├── git-workflow.md             # Git工作流
│   └── code-review.md              # Code Review要点
└── project-map.md             # 跨项目依赖关系
```

---

## 📋 项目规则（核心）

### shared-rules.md — 项目共享规则

```markdown
# <项目中文全称> 项目共享规则

> 本文件是项目规则的单一事实来源，供 AI 助手共同引用。

---

## 项目清单

| 项目 | 代码路径 | 说明 |
|------|----------|------|
| <项目中文全称> | <代码路径> | <项目说明> |

---

## 技术栈

<技术栈>

---

## 编码规范

### 必须遵守
- 遵循项目现有代码风格
- 新增方法必须有 Javadoc
- 复杂逻辑加行注释
- ServiceImpl 禁止直接注入外部 Feign Client，统一走 proxy 层
- 金额用 BigDecimal，日期用 LocalDateTime
- 禁止使用 `System.out.println()`，统一用 `@Slf4j` 的 `log`

### 数据库规范
- 表名、字段名使用小写下划线
- 必须有 `id`、`create_time`、`update_time`
- 逻辑删除用 `deleted` 字段

### API 规范
- 统一响应：`{"code": 200, "msg": "success", "data": {...}}`
- 分页响应：`{"total": 100, "list": [...]}`

---

## Git 规范

### 分支策略
- `main`：主分支，仅通过 PR 合并
- `develop`：开发分支
- `feature/xxx`：功能分支
- `bugfix/xxx`：修复分支

### Commit 格式
```
<type>: story#<禅道编号> <需求名称> <具体改动>

example: feat: story#12345 用户登录接口实现
```

---

## 工作流程

1. **查规范再动手**：编码前先看同模块已有文件的写法
2. **最小修改**：只做必要改动，不改无关文件
3. **边做边记录**：有价值的信息及时写入对话日志

### 快捷指令

| 用户说法 | 执行操作 | 说明 |
|---------|---------|------|
| "更新下代码" | `git pull` | 直接执行，无需确认 |
| "提交代码" | `git add` + `git commit` | 需确认提交信息 |
| "推送代码" | `git push` | 需确认 |

---

## 禁止行为

- 禁止执行 `git reset --hard`、`git rebase` 等改写历史的操作
- 禁止修改无关文件和测试逻辑
- 禁止在 memory-bank 目录存放非 .md 文件
```

---

### coding-standards.md — 编码规范

```markdown
# 编码规范

## Java 规范

### 命名规范
| 类型 | 规范 | 示例 |
|------|------|------|
| 类名 | 大驼峰 | UserService |
| 方法名 | 小驼峰 | getUserById |
| 常量 | 全大写下划线 | MAX_RETRY_COUNT |
| 变量 | 小驼峰 | userName |
| 包名 | 全小写 | com.xxx.crm |

### 分层规范
```
Controller    → 参数校验、参数转换、调用Service
Service       → 业务逻辑处理、事务管理
Mapper        → 数据库操作（只做CRUD）
VO/DTO/Req   → 数据传输对象
```

### 方法规范
- 方法长度控制在 50 行以内
- 参数不超过 5 个
- 优先使用卫语句减少嵌套
- 异常要捕获处理，不能裸抛

## SQL 规范

```sql
-- ✅ 正确
SELECT id, name, create_time
FROM sys_user
WHERE deleted = 0 AND status = 1;

-- ❌ 错误：SELECT *
SELECT *
FROM sys_user;
```

### 索引规范
- 区分度高的字段放前面
- 不要在索引列上使用函数
- 避免冗余索引

## 日志规范

```java
// ✅ 正确
@Slf4j
public class UserService {
    public void login() {
        log.info("用户登录: phone={}", phone);
        try {
            // 业务逻辑
        } catch (BusinessException e) {
            log.warn("业务异常: {}", e.getMessage());
            throw e;
        } catch (Exception e) {
            log.error("系统异常", e);
            throw new SystemException("操作失败");
        }
    }
}

// ❌ 错误
System.out.println("用户登录");
```

## API 规范

### 请求格式
```json
{
  "phone": "13800138000",
  "code": "123456"
}
```

### 响应格式
```json
// 成功
{
  "code": 200,
  "msg": "success",
  "data": {
    "userId": 1,
    "token": "xxx"
  }
}

// 分页
{
  "code": 200,
  "msg": "success",
  "data": {
    "total": 100,
    "list": [...]
  }
}

// 失败
{
  "code": 400,
  "msg": "参数错误",
  "data": null
}
```
```

---

### git-workflow.md — Git工作流

```markdown
# Git 工作流

## 分支命名

| 类型 | 格式 | 示例 |
|------|------|------|
| 功能 | feature/故事编号-简短描述 | feature/12345-user-login |
| 修复 | bugfix/故事编号-简短描述 | bugfix/12346-fix-null-pointer |
| 发布 | release/v1.0.0 | release/v1.0.0 |

## Commit 规范

### 格式
```
<type>: story#<禅道编号> <需求名称> <具体改动>

type: feat | fix | docs | style | refactor | test | chore
```

### 示例
```
feat: story#12345 用户登录接口实现
fix: story#12346 修复用户列表空指针异常
docs: 更新README用户登录说明
refactor: 重构用户服务，提取公共方法
```

## PR 规范

1. PR 标题同 Commit 格式
2. 描述包含：改动内容、测试结果、截图（如有UI）
3. 必须通过 CI 才能合并
4. 至少 1 人 review 通过

## 快捷指令

| 用户说法 | 执行 | 命令 |
|---------|------|------|
| 更新代码 | git pull | `git pull origin develop` |
| 提交代码 | git commit | `git add . && git commit -m "..."` |
| 推送代码 | git push | `git push origin feature/xxx` |
| 查看状态 | git status | `git status` |
| 查看日志 | git log | `git log --oneline -10` |
```

---

### code-review.md — Code Review要点

```markdown
# Code Review 要点清单

## 1. 代码规范 ⭐⭐⭐
- [ ] 命名是否符合项目规范
- [ ] 是否有 SonarLint 警告
- [ ] 是否有硬编码（密码、密钥）
- [ ] 是否有 TODO 未完成

## 2. 业务逻辑 ⭐⭐⭐
- [ ] 逻辑是否正确
- [ ] 边界条件是否处理（空指针、数组越界）
- [ ] 并发安全（如果是多线程场景）
- [ ] 事务边界是否正确

## 3. 安全性 ⭐⭐⭐
- [ ] SQL 注入风险（是否参数化查询）
- [ ] XSS 风险（输出是否转义）
- [ ] 越权风险（权限校验是否完整）
- [ ] 敏感信息泄露（日志是否打印敏感数据）

## 4. 性能 ⭐⭐
- [ ] 是否有 N+1 查询
- [ ] 是否有不必要的循环查库
- [ ] 大数据量是否分页/分批处理
- [ ] 是否有缓存机会

## 5. 可维护性 ⭐⭐
- [ ] 代码是否重复（DRY原则）
- [ ] 是否过度设计
- [ ] 注释是否充分
- [ ] 是否易于扩展

## 审查意见格式

### 🔴 必须修改（阻塞）
```
[BLOCK] 描述问题
位置：xxx.java:123
建议：xxx
```

### 🟡 建议修改
```
[NIT] 描述问题
位置：xxx.java:456
建议：xxx
```

### 🟢 通过
```
[LGTM] 可以合并
```
```

---

## 🔄 经验沉淀工作流

```
┌─────────────────────────────────────────────────────────┐
│                   经验沉淀四步法                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1️⃣ 识别                       2️⃣ 记录                  │
│  这个问题值得沉淀吗？              写进 rules/              │
│  - 重复出现 ≥2次                  - 编码规范              │
│  - 解决耗时 >30分钟                - Git工作流            │
│  - 有通用性                       - Review要点            │
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

### rules/ 目录（项目规则）

| 文件 | 内容 | 优先级 |
|------|------|--------|
| shared-rules.md | 共享规则入口 | ⭐⭐⭐ |
| coding-standards.md | Java/SQL/日志/API规范 | ⭐⭐⭐ |
| git-workflow.md | Git工作流和快捷指令 | ⭐⭐ |
| code-review.md | Code Review检查清单 | ⭐⭐ |

### patterns/ 目录（经验模式）

| 场景 | Pattern 文件 |
|------|-------------|
| 异常处理 | exception-handling.md |
| 缓存策略 | cache-strategy.md |
| API 设计 | api-design.md |
| 分页 | pagination-pattern.md |

### snippets/ 目录（代码片段）

| 语言 | 文件 |
|------|------|
| Java | pagination.java, result-wrapper.java |
| SQL | soft-delete.sql, audit-log.sql |

---

## 🎯 快速记录模板

### 新增规则
```
## [规则名称]

### 要求
- xxx
- xxx

### 示例
```代码
代码示例
```

### 禁止
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

### 改动记录
| 日期 | 改动 | 作者 |
|------|------|------|
| 2024-01-01 | 初始版本 | 张三 |
```

---

## 🔗 与 memory-bank 配合

| Skill | 职责 |
|-------|------|
| **memory-bank** | 项目文档结构（AGENTS/模板/索引） |
| **hermes-experience** | 经验沉淀（rules/snippets/patterns） |

```
项目记忆体系：
├── AGENTS.md         ← memory-bank：AI必读上下文
├── rules/            ← hermes-experience：编码规范/Git/Review
├── snippets/         ← hermes-experience：代码片段
└── 99-dialogue-logs/ ← 对话日志
```

---

## 💬 使用方式

```
用户：帮我沉淀这次Bug修复的经验
助手：好的！使用 patterns/exception-handling.md 模板记录

用户：我想把项目的编码规范积累起来
助手：使用 rules/coding-standards.md，我来帮你整理

用户：下次遇到类似问题怎么调用？
助手：hermes-experience 会自动读取 rules/ 下的规范
```
