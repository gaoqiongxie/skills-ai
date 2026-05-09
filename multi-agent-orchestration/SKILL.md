---
name: "multi-agent-orchestration"
description: "多Agent编排框架：将单一AI转变为专业化Agent团队协作，支持并行执行、工作流编排、Git worktree隔离。当用户说'多Agent'、'Agent团队'、'并行Agent'、'编排多个AI'、'AI团队协作'、'多个AI一起工作'、'Agent swarm'时触发。核心特点：角色专业化、并行执行、自动协调、worktree隔离、技能分工。"
---

> **来源**: oh-my-claudecode / GStack / Claude-Code-Game-Studios
>
> **发布时间**: 2026-05
>
> **理念**: "一个人指挥一支 AI 团队。"

# 🎛️ Multi-Agent Orchestration — 多 Agent 编排

把 Claude Code 变成一支由多个专业 Agent 组成的开发团队。

---

## 🎯 核心概念

传统 AI 编程：你和 AI 一对一对话。

多 Agent 编排：你作为**指挥者**，AI 作为**团队**——每个 Agent 有专门的技能和职责，自动协调完成复杂任务。

---

## 🧑‍💻 Agent 角色定义

### 标准团队角色

| Agent | 职责 | 触发场景 |
|-------|------|---------|
| **Planner** | 架构设计、任务分解、依赖分析 | 项目启动、需求分析 |
| **Builder** | 编码实现、功能开发 | 具体功能开发 |
| **Reviewer** | 代码审查、质量检查 | 提交前、PR 时 |
| **Tester** | 测试用例、自动化测试 | 功能完成、回归测试 |
| **Debugger** | Bug 排查、根因分析 | 报错、异常 |
| **Docs** | 文档编写、注释维护 | 代码完成、API 变更 |
| **Security** | 安全审计、漏洞扫描 | 代码审查、上线前 |

### 扩展角色（可选）

| Agent | 职责 |
|-------|------|
| **Performance** | 性能分析、优化建议 |
| **UX** | 用户体验检查、交互优化 |
| **DevOps** | CI/CD、部署脚本 |
| **Data** | 数据库设计、数据迁移 |

---

## 🔄 工作流编排模式

### 模式一：顺序执行（Pipeline）

```
Planner → Builder → Reviewer → Tester → Docs
```

适合：标准开发流程，每个阶段依赖前一阶段输出。

### 模式二：并行执行（Parallel）

```
        ┌→ Builder-A (前端)
Planner ─┼→ Builder-B (后端)
        └→ Builder-C (数据库)
                ↓
            Reviewer
```

适合：大型功能拆分，多个模块可独立开发。

### 模式三：评审循环（Review Loop）

```
Builder → Reviewer
    ↑         ↓
    └─ 不通过 ─┘
```

适合：代码质量要求高的场景。

### 模式四：探索模式（Exploration）

```
Planner → 多个 Builder 并行探索不同方案
                ↓
            对比评估 → 选择最佳方案
```

适合：技术选型、架构决策。

---

## 🏗️ Worktree 隔离机制

每个 Agent 在独立的 Git worktree 中工作，避免文件冲突：

```
project/
├── main/              # 主分支
├── .claude/worktrees/
│   ├── planner-001/   # Planner 的工作区
│   ├── builder-001/   # Builder 的工作区
│   ├── reviewer-001/  # Reviewer 的工作区
│   └── tester-001/    # Tester 的工作区
```

**优势**：
- 并行 Agent 不会互相覆盖文件
- 每个 Agent 的工作可追溯
- 失败可单独回滚

---

## 🚀 使用方式

### 方式一：快速启动标准团队

```
启动多Agent团队开发
项目：用户管理系统
技术栈：React + Node.js
```

自动创建 Planner、Builder、Reviewer、Tester 四个 Agent。

### 方式二：指定角色编排

```
编排 Agent 团队：
- Planner：设计数据库架构
- Builder-A：实现用户API
- Builder-B：实现前端页面
- Reviewer：代码审查
- 并行执行 Builder-A 和 Builder-B
```

### 方式三：自定义工作流

```
定义工作流：
1. Planner 分析需求并输出任务清单
2. 3个 Builder 并行开发不同模块
3. Reviewer 审查所有代码
4. Tester 运行测试
5. 全部通过后合并到主分支
```

---

## 📋 Agent 协作规范

### 通信协议

```yaml
agent_message:
  from: "builder-001"
  to: "reviewer-001"
  type: "code_review_request"
  content:
    file: "src/auth/login.ts"
    changes: "实现JWT登录"
    dependencies: ["database", "redis"]
```

### 状态追踪

| 状态 | 说明 |
|------|------|
| `pending` | 等待执行 |
| `running` | 执行中 |
| `reviewing` | 审查中 |
| `blocked` | 被阻塞（等待依赖） |
| `completed` | 完成 |
| `failed` | 失败 |

---

## 🆚 与 BMAD / AI-DLC 的关系

| | multi-agent-orchestration | bmad-method | ai-dlc |
|---|---|---|---|
| **核心** | 多 Agent 并行协作 | 虚拟 AI 开发团队 | 开发生命周期管理 |
| **侧重点** | 编排与协调 | 角色分工与文档 | 质量门控与阶段 |
| **并行** | ✅ 原生支持 | ❌ 顺序为主 | ❌ 顺序为主 |
| **最佳组合** | 用 bmad-method 定义角色，用 multi-agent 编排执行，用 ai-dlc 质量门控 |

---

## 💡 最佳实践

### DO
- ✅ 大型功能开发时使用多 Agent 并行
- ✅ 为每个 Agent 明确职责边界
- ✅ 使用 worktree 隔离避免冲突
- ✅ 定期同步各 Agent 的进展

### DON'T
- ❌ 小功能也强行多 Agent（协调开销 > 收益）
- ❌ Agent 职责重叠导致冲突
- ❌ 忽视 Agent 间的依赖关系

---

> "一个人顶一个团队？不，一个人指挥一个 AI 团队。"
