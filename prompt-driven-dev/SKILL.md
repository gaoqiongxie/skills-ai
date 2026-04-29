---
name: "prompt-driven-dev"
description: "提示驱动开发：版本化管理AI提示词，实现确定性代码生成。当用户说'提示词版本化'、'Prompt Driven Development'、'PDD'、'管理AI提示词'、'提示词工程'、'确定性AI生成'、'提示词即代码'、'Prompt as Code'时触发。核心特点：提示词版本控制、确定性重新生成、提示词分层架构、与Git集成、避免AI'胡写'。"
---

> **来源**: Prompt Driven Development 社区实践 + VS Code PromptDriven 扩展生态
>
> **发布时间**: 2026-04-29
>
> **理念**: "提示词是新时代的源代码。版本化它，管理它，像对待代码一样对待它。"

# 📝 Prompt Driven Development — 提示驱动开发

让 AI 代码生成从"玄学"变成"工程"。

---

## 🎯 核心概念

**传统 AI 编程的问题：**
- 同一句提示词，每次生成的代码不一样
- 改了一个变量名，AI 把整个文件重写了
- 上周能跑的代码，这周再生成就跑不通了
- 提示词散落在聊天记录里，无法追溯

**PDD 的解决方案：**
- **版本化** — 提示词用 Git 管理，每次变更可追溯
- **确定性** — 相同输入 → 相同输出，可重复构建
- **分层化** — 系统提示 + 上下文提示 + 任务提示，解耦复用
- **可测试** — 提示词改变后，自动验证输出质量

---

## 🏗️ 提示词分层架构

```
prompts/
├── system/                    # 系统级提示（角色+约束）
│   ├── backend-developer.md   # 后端开发角色定义
│   ├── frontend-developer.md  # 前端开发角色定义
│   └── code-reviewer.md       # 代码审查角色定义
│
├── context/                   # 上下文提示（项目知识）
│   ├── architecture.md        # 系统架构概述
│   ├── coding-standards.md    # 编码规范
│   ├── tech-stack.md          # 技术栈说明
│   └── database-schema.md     # 数据库结构
│
├── tasks/                     # 任务提示（具体功能）
│   ├── feature-001-auth.md    # 功能1：用户认证
│   ├── feature-002-payment.md # 功能2：支付接口
│   └── bugfix-003-timeout.md  # Bug修复3：超时问题
│
└── templates/                 # 模板提示（可复用片段）
    ├── api-endpoint.md        # API接口模板
    ├── react-component.md     # React组件模板
    └── unit-test.md           # 单元测试模板
```

---

## 📋 每层提示词规范

### 1. System Prompt（系统提示）

定义 AI 的"身份"和"行为准则"。

```markdown
# System: Backend Developer

## 角色
你是一名资深 Java 后端开发工程师，专注于 Spring Boot 微服务开发。

## 技术栈
- Java 17
- Spring Boot 3.x
- MyBatis Plus
- PostgreSQL 14
- Redis 7

## 编码规范
1. 使用构造函数注入，禁止字段注入
2. 所有 Service 方法必须有单元测试
3. 异常统一使用 BusinessException
4. 日志使用 @Slf4j，禁止 System.out.println
5. 数据库操作必须使用事务

## 禁止事项
- 禁止生成伪代码或 TODO
- 禁止修改无关文件
- 禁止省略异常处理
- 禁止使用已过时的 API

## 输出格式
```java
// 只输出修改后的代码块，用注释标记变更点
// [CHANGED] 这里做了 XX 修改
代码...
```
```

**特点**：
- 一个项目一套 System Prompt
- 变更频率低，稳定后很少修改
- 所有任务提示都继承 System Prompt

---

### 2. Context Prompt（上下文提示）

提供项目特定的"领域知识"。

```markdown
# Context: Project Architecture

## 系统架构
```
用户服务 (User Service)
  ↓ 调用
订单服务 (Order Service)
  ↓ 调用
支付服务 (Payment Service)
```

## 关键约定
- 服务间通信使用 OpenFeign
- 统一响应格式：{"code": 200, "msg": "success", "data": {...}}
- 分页参数：pageNum, pageSize
- 时间格式：ISO 8601 (yyyy-MM-dd'T'HH:mm:ss)

## 数据库命名
- 表名：snake_case，复数形式
- 字段：snake_case
- 主键：id（BIGSERIAL）
- 时间戳：created_at, updated_at

## 已有模块
- 用户模块：/users，已包含注册/登录/信息修改
- 订单模块：/orders，已包含创建/查询/取消
- 当前任务：添加支付模块
```

**特点**：
- 随着项目演进持续更新
- 包含架构决策和关键约定
- 新任务开发前先加载相关 Context

---

### 3. Task Prompt（任务提示）

描述具体要做什么。

```markdown
# Task: 实现支付接口

## 需求
实现订单支付功能，支持支付宝和微信支付。

## 输入
- 订单 ID
- 支付方式（ALIPAY / WECHAT）
- 支付金额

## 输出
- 支付流水号
- 第三方支付链接
- 支付状态（PENDING / SUCCESS / FAILED）

## 约束
- 必须校验订单金额与支付金额一致
- 必须防止重复支付（幂等性）
- 支付超时时间为 30 分钟
- 需要记录支付日志

## 依赖
- 订单服务：查询订单状态
- 用户服务：查询用户余额（余额支付时）

## 参考实现
```java
// 已有的订单查询接口
Order order = orderService.getById(orderId);
```
```

**特点**：
- 每个任务独立一个文件
- 需求描述要具体、可测试
- 包含输入/输出/约束/依赖

---

## 🔄 PDD 工作流

### Step 1：编写提示词

```bash
# 创建任务提示词
prompts/tasks/feature-001-auth.md
```

### Step 2：提交到 Git

```bash
git add prompts/
git commit -m "feat: 添加用户认证任务提示词

- 定义注册/登录/登出三个接口
- 使用 JWT Token 方案
- 包含输入校验规则"
```

### Step 3：执行生成

```bash
# 方式1：命令行
pdd generate prompts/tasks/feature-001-auth.md --output src/

# 方式2：IDE 插件
在 VS Code 中右键提示词文件 → "Generate Code"
```

### Step 4：验证输出

```bash
# 自动运行测试
mvn test

# 静态检查
mvn checkstyle:check

# 安全扫描
sonar-scanner
```

### Step 5：审查与迭代

```
如果测试不通过：
  → 修改提示词（不是修改代码！）
  → git commit -m "fix: 补充幂等性校验约束"
  → 重新生成
  → 再次验证

如果测试通过：
  → 提交生成的代码
  → git commit -m "feat: 实现用户认证接口（由 PDD 生成）"
```

---

## 🧪 提示词即测试

每个提示词本身就是"可执行的需求"。通过验证生成的代码是否满足提示词中的约束，来验证提示词的质量。

### 提示词质量检查清单

| 检查项 | 标准 |
|--------|------|
| **完整性** | 是否包含输入/输出/约束/依赖？ |
| **无歧义** | 是否有多种理解方式？ |
| **可测试** | 是否能写出明确的测试用例？ |
| **原子性** | 是否只描述一件事？ |
| **一致性** | 是否与 System/Context 冲突？ |

### 提示词回归测试

当修改提示词后，自动重新生成并验证：

```yaml
# pdd-regression.yaml
regression:
  - task: prompts/tasks/feature-001-auth.md
    tests:
      - test: AuthControllerTest.registerSuccess
      - test: AuthControllerTest.registerDuplicate
      - test: AuthControllerTest.loginSuccess
      - test: AuthControllerTest.loginWrongPassword
```

---

## 📦 与 Git 集成

### 提交规范

```
prompts/ 目录下的变更：
- feat: 新增任务提示词
- fix: 修复提示词缺陷
- refactor: 优化提示词结构
- docs: 更新上下文文档

src/ 目录下的变更（由 PDD 生成）：
- gen: 由提示词生成/重新生成
```

### 版本锁定

```markdown
# prompts.lock
# 记录每次生成使用的提示词版本

feature-001-auth.md:
  hash: a1b2c3d4
  generated_at: 2026-04-29T10:30:00Z
  commit: 1790da2
  status: ✅ 测试通过

feature-002-payment.md:
  hash: e5f6g7h8
  generated_at: 2026-04-29T11:00:00Z
  commit: 1790da2
  status: ❌ 测试失败（待修复提示词）
```

---

## 🆚 与其他方法的关系

| | PDD | Vibe Coding | Spec-Driven | BMAD |
|---|---|---|---|---|
| **核心** | 提示词版本化 | 即兴对话 | 规范文档 | 角色协作 |
| **确定性** | 高 | 低 | 中 | 中 |
| **可追溯** | 强（Git） | 无 | 中 | 中 |
| **适用** | 需要稳定输出的场景 | 原型探索 | 需求对齐 | 团队协作 |

**最佳实践**：
- **探索阶段**：用 Vibe Coding 快速验证想法
- **确定阶段**：用 PDD 固化提示词，确保稳定输出
- **协作阶段**：用 BMAD 管理多角色，用 SDD 对齐规范

---

## 💡 使用示例

### 示例1：修复提示词缺陷

```
第1次生成：
- 提示词："实现用户注册"
- 输出：注册接口（无密码加密）
- 测试：❌ 安全审计失败

修复提示词：
- 补充约束："密码必须使用 BCrypt 加密存储"

第2次生成：
- 提示词：更新后（含加密约束）
- 输出：注册接口（含 BCrypt 加密）
- 测试：✅ 通过

提交：
- git commit prompts/tasks/feature-001-auth.md
- git commit src/...（生成的代码）
```

### 示例2：多环境提示词

```
prompts/
├── system/
│   ├── backend-developer.md          # 通用后端角色
│   ├── backend-developer-junior.md   # 初级后端（更多注释）
│   └── backend-developer-senior.md   # 高级后端（更简洁）
│
└── tasks/
    ├── feature-001-auth.md           # 通用版本
    ├── feature-001-auth-zh.md        # 中文注释版本
    └── feature-001-auth-en.md        # 英文注释版本
```

### 示例3：提示词模板复用

```markdown
# Task: 实现订单查询接口

## 使用模板
- base: templates/api-endpoint.md      # API接口基础结构
- filter: templates/pagination.md      # 分页查询逻辑
- auth: templates/jwt-auth.md          # JWT认证校验

## 具体需求
- 支持按状态/时间范围查询
- 需要关联用户信息
- 管理员可查全部，普通用户只能查自己的
```

---

## 🚀 快速开始

```
用户：用 PDD 方法帮我实现 [功能]

AI：
1. 分析需求，确定提示词分层
2. 编写 Task Prompt（包含输入/输出/约束/依赖）
3. 检查 System/Context 是否已加载
4. 生成代码
5. 运行测试验证
6. 如果失败 → 修改提示词 → 重新生成
7. 如果成功 → 提交提示词 + 代码
```

---

> "在 AI 时代，写提示词的能力就是写代码的能力。PDD 让这种能力可积累、可传承、可改进。"
