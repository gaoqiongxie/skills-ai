---
name: "beads-memory"
description: "编码Agent记忆升级：跨会话持久化代码库上下文。当用户说'记住这个代码库'、'下次继续'、'跨会话记忆'、'记住我的项目'、'别每次都从头了解'时触发。核心特点：自动捕获项目结构/关键决策/未完成任务/技术债，AI压缩存储，下次对话自动加载相关上下文，6倍token节省。"
---

> **来源**: gastownhall/beads ⭐22.1K（2026年5月热门，编码Agent记忆层）
>
> **发布时间**: 2026-05-14
>
> **理念**: "Agent 不应该每次对话都从零认识你——它应该记得你是谁，你在做什么。"

# 🧠 Beads Memory — 编码 Agent 记忆升级

让 AI 记住你的代码库、你的决策、你的进度，跨会话持续可用。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **项目快照** | 自动捕获项目结构、关键文件、技术栈 |
| **决策记录** | 记录架构决策（ADR）、选型理由、废弃方案 |
| **任务追踪** | 记录进行中/已完成/阻塞的任务 |
| **技术债务** | 标记需要重构的代码、临时方案、已知问题 |
| **AI压缩** | 用AI压缩长上下文，保留关键信息，丢弃噪音 |
| **智能加载** | 下次对话自动加载与当前任务相关的上下文 |

---

## 🏗️ 记忆结构

```
.beads/                          # 记忆目录（提交到git）
├── project-snapshot.md          # 项目快照
├── decisions/                   # 决策记录
│   ├── 001-use-postgresql.md
│   ├── 002-dont-use-orm.md
│   └── 003-microservices-boundary.md
├── tasks/                       # 任务追踪
│   ├── active.md                # 进行中
│   ├── backlog.md               # 待办
│   └── completed.md             # 已完成
├── tech-debt.md                 # 技术债务
├── key-files.md                 # 关键文件索引
└── session-summaries/           # 会话摘要（AI生成）
    ├── 2026-05-01-session.md
    └── 2026-05-05-session.md
```

---

## 📝 记忆文件规范

### 1. 项目快照 (project-snapshot.md)

```markdown
# Project Snapshot

## 基本信息
- 名称: my-api-service
- 语言: TypeScript
- 框架: Express.js
- 数据库: PostgreSQL 15
- ORM: 无（原生SQL + pg）

## 目录结构
```
src/
├── controllers/       # HTTP入口
├── services/          # 业务逻辑
├── repositories/      # 数据访问
├── middleware/        # 中间件
├── types/             # 共享类型
└── utils/             # 工具函数
```

## 关键依赖
- express: ^4.18
- pg: ^8.11
- neverthrow: ^6.0 (Result类型)
- zod: ^3.22 (校验)

## 环境变量
- DATABASE_URL
- JWT_SECRET
- PORT

## 启动方式
```bash
npm run dev      # 开发
npm test         # 测试
npm run build    # 构建
```

## 最新变更 (2026-05-10)
- 添加了用户认证模块
- 迁移了订单表（零停机）
```

### 2. 决策记录 (decisions/)

```markdown
# ADR-003: 微服务边界划分

## 状态
Accepted (2026-05-08)

## 背景
单体应用增长，需要拆分

## 决策
按业务域拆分：用户/订单/支付三个服务

## 理由
- 团队已按业务域分工
- 订单和支付有强一致性要求，但用户独立

## 废弃方案
- 按技术层拆分（frontend/backend）→ 导致跨服务调用过多

## 影响
- 需要引入服务发现
- 需要分布式事务方案
```

### 3. 任务追踪 (tasks/)

```markdown
# Active Tasks

## [TASK-005] 支付回调幂等性
- 状态: 🟡 进行中
- 负责人: AI (协助)
- 描述: 支付回调接口需要保证幂等性，防止重复处理
- 阻塞: 等待[TASK-004]事务管理方案确定
- 预计完成: 2026-05-12

## [TASK-004] 分布式事务方案
- 状态: 🔴 阻塞
- 负责人: 用户
- 描述: 选择Saga vs 2PC
- 决策: 待用户确认
```

### 4. 技术债务 (tech-debt.md)

```markdown
# Tech Debt

## 🔴 高优先级
- [ ] 订单查询缺少索引（created_at），生产环境已出现慢查询

## 🟡 中优先级
- [ ] 用户密码哈希算法从 bcrypt 升级到 Argon2
- [ ] 硬编码的魔法数字（分页默认10条）

## 🟢 低优先级
- [ ] 统一错误码格式（目前混用字符串和对象）
```

---

## 🔄 工作流程

### 初始化记忆

```
用户：记住这个项目

AI：
1. 扫描项目结构
2. 识别技术栈
3. 创建 project-snapshot.md
4. 创建 decisions/、tasks/、tech-debt.md 模板
5. 告知用户：记忆已建立，下次对话会自动加载
```

### 会话中更新记忆

```
用户：我决定用 PostgreSQL，不用 MongoDB

AI：
1. 记录决策到 decisions/001-use-postgresql.md
2. 更新 project-snapshot.md 的依赖列表
3. 在 tech-debt.md 中标记"需要迁移脚本"
```

### 会话结束总结

```
AI（自动）：
本次会话摘要：
- 完成了用户认证模块的接口设计
- 决策：使用JWT + Refresh Token方案
- 新增任务：[TASK-006] 实现Token刷新接口
- 技术债务：密码加密算法待升级

保存到 session-summaries/2026-05-10-session.md
```

### 新会话加载

```
用户：继续弄那个支付模块

AI（自动加载）：
根据 beads-memory：
- 项目：my-api-service（Express + PostgreSQL）
- 相关决策：微服务按业务域拆分（ADR-003）
- 相关任务：[TASK-005] 支付回调幂等性（进行中，阻塞于TASK-004）
- 相关技术债：订单查询缺索引

直接进入上下文，无需从零了解。
```

---

## 💡 使用示例

### 示例1：初始化项目记忆

```
用户：这是我的项目，记住它

AI：
1. 扫描项目结构 → Express.js API，PostgreSQL，无ORM
2. 创建 .beads/project-snapshot.md
3. 创建 .beads/decisions/、tasks/、tech-debt.md
4. 输出：
   "已建立项目记忆。下次对话我会自动加载上下文。
   目前识别到：
   - 技术栈：Express + PostgreSQL + TypeScript
   - 关键目录：controllers/services/repositories
   - 待办：你需要填充 decisions/ 和 tasks/"
```

### 示例2：跨会话任务恢复

```
Session 1:
用户：帮我设计支付模块
AI：设计了支付流程，记录了决策（用Stripe）
→ 保存到 beads-memory

Session 2（3天后）:
用户：继续弄支付
AI（自动加载 beads-memory）：
"上次我们决定用 Stripe，支付流程已设计，
 当前阻塞：需要你提供 Stripe API Key。
 要继续实现吗？"
```

---

## 🆚 与其他记忆 Skill 的关系

| Skill | 定位 | 何时使用 |
|-------|------|---------|
| **beads-memory** | 代码库上下文 | 编码项目，需要跨会话记忆 |
| **claude-mem** | 全局持久记忆 | 所有对话，个人偏好 |
| **memory-bank** | 项目文档化记忆 | 手动维护核心文档 |
| **hermes-experience** | 经验沉淀 | 踩坑记录，模式复用 |
| **supermemory** | 向量检索记忆 | 大规模知识检索 |

**最佳实践**：
- 项目级：beads-memory（自动代码库记忆）
- 个人级：claude-mem（跨项目偏好）
- 经验级：hermes-experience（踩坑沉淀）

---

## 🚀 快速开始

```
用户：记住这个项目 / 初始化记忆

AI：
1. 扫描项目结构
2. 创建 .beads/ 目录和文件
3. 记录初始快照
4. 告知记忆已建立

用户：（几天后）继续上次的任务

AI：
1. 自动加载 .beads/ 内容
2. 识别相关上下文
3. 直接进入工作，无需重新了解
```

---

> "好记性不如烂笔头，好Agent不如 beads-memory。"
