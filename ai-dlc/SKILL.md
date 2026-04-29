---
name: "ai-dlc"
description: "AI驱动开发生命周期：四阶段工程化AI开发方法论（构思→执行→运维→反思）。当用户说'AI开发流程'、'开发生命周期'、'工程化AI开发'、'AI-DLC'、'质量门控'、'Hat-based工作流'、'AI项目管理'、'规范化AI开发'时触发。核心特点：四阶段闭环、Hat-based角色切换、质量门控阻断机制、Backpressure反馈、DAG依赖编排。"
---

> **来源**: [TheBushidoCollective/ai-dlc](https://github.com/TheBushidoCollective/ai-dlc) — AI-Driven Development Lifecycle
>
> **发布时间**: 2026-04-29
>
> **理念**: "AI 编程不是聊天，而是工程。每个阶段都有入口标准、出口标准和质量门控。"

# 🔄 AI-DLC — AI 驱动开发生命周期

把 AI 辅助开发变成可重复、可审计、可改进的工程流程。

---

## 🎯 核心概念

AI-DLC（AI-Driven Development Lifecycle）将软件开发的全生命周期映射到 AI 协作场景，形成**四阶段闭环**：

```
构思(Elaboration) → 执行(Execution) → 运维(Operation) → 反思(Reflection)
         ↑___________________________________________________________↓
```

**与传统 AI 编程的区别：**

| | 传统 AI 编程 | AI-DLC |
|---|---|---|
| 流程 | 无，想到哪问到哪 | 四阶段严格闭环 |
| 角色 | 你和 AI 两个人 | Hat-based 多角色切换 |
| 质量 | 事后检查 | 阶段门控，不通过就阻断 |
| 可追溯 | 聊天记录散落 | 每个决策都有 Intent + Unit 记录 |
| 改进 | 靠经验 | Reflection 阶段系统化复盘 |

---

## 🎩 Hat-based 角色工作流

AI-DLC 的核心是 **"换帽子"** —— 同一个 AI 在不同阶段戴不同的帽子，扮演不同角色：

| 帽子 | 角色 | 职责 | 阶段 |
|------|------|------|------|
| 🎩 **Planner** | 规划师 | 需求分析、范围界定、风险评估 | Elaboration |
| 🔨 **Builder** | 构建者 | 代码实现、单元测试、文档编写 | Execution |
| 🔍 **Reviewer** | 审查者 | 代码审查、安全审计、合规检查 | Execution/Operation |
| 🔴 **Red Team** | 红队 | 故意找茬、攻击假设、发现盲点 | 贯穿全程 |
| 🔵 **Blue Team** | 蓝队 | 防御验证、修复验证、回归测试 | Operation |
| 📝 **Scribe** | 记录员 | 文档维护、决策日志、知识沉淀 | Reflection |
| 🎯 **Skeptic** | 怀疑者 | 质疑过度设计、推动 MVP | Elaboration |

**换帽规则**：
- 每个阶段开始时明确声明"现在戴 XX 帽子"
- 同一轮对话中不换帽子（避免角色混乱）
- 复杂任务强制引入 Red Team 审查

---

## 📋 四阶段详解

### 阶段 1：构思（Elaboration）

**目标**：搞清楚"做什么"和"为什么做"，产出清晰的开发意图。

**入口标准**：用户提出需求或问题
**出口标准**：Intent 文档通过 Red Team 审查

#### 关键产出：Intent 文档

```markdown
# Intent: {功能名称}

## 问题陈述
用户遇到什么痛点？

## 目标
- 目标 1：...
- 目标 2：...

## 范围
### 包含（In Scope）
- ...

### 不包含（Out of Scope）
- ...

## 约束条件
- 时间：...
- 技术：...
- 资源：...

## 成功标准
- [ ] 标准 1
- [ ] 标准 2

## 风险评估
| 风险 | 概率 | 影响 | 缓解措施 |
|------|------|------|---------|
| ... | 高/中/低 | 高/中/低 | ... |

## Red Team 审查意见
- [ ] 假设是否合理？
- [ ] 范围是否过度？
- [ ] 是否有遗漏的边界情况？
```

#### 阶段内工作流

```
Planner 分析需求 → Skeptic 质疑范围 → Red Team 攻击假设
    → 修订 Intent → 用户确认 → 进入下一阶段
```

---

### 阶段 2：执行（Execution）

**目标**：按 Intent 实现功能，通过所有质量门控。

**入口标准**：Intent 文档已确认
**出口标准**：所有 Unit 通过 Backpressure Gate

#### 关键产出：Unit 文档

```markdown
# Unit: {功能单元名称}

## 关联 Intent
- Intent: {链接到父 Intent}

## 实现任务
- [ ] 任务 1：...
- [ ] 任务 2：...

## 技术决策
- 决策 1：选择 XX 而不是 YY，原因...

## 验收标准
- [ ] 功能正确性：...
- [ ] 性能：...
- [ ] 安全：...

## Backpressure Gate
- [ ] 单元测试通过
- [ ] 类型检查通过
- [ ] Linter 通过
- [ ] 安全扫描通过
- [ ] 代码审查通过
```

#### 阶段内工作流

```
Planner 拆分为 Units → Builder 逐个实现
    → Reviewer 代码审查 → Red Team 攻击实现
    → Blue Team 验证修复 → Backpressure Gate 检查
    → 通过 → 进入下一阶段
    → 不通过 → 返回 Builder 修复
```

#### Backpressure 质量门控

每个 Unit 必须通过以下检查才能进入下一阶段：

| 门控 | 检查内容 | 阻断级别 |
|------|---------|---------|
| **测试门控** | 单元测试覆盖率 > 80%，全部通过 | 🔴 阻断 |
| **类型门控** | 静态类型检查无错误 | 🔴 阻断 |
| **规范门控** | Linter/Formatter 无警告 | 🟡 警告 |
| **安全门控** | 无 SQL 注入/XSS/硬编码密钥 | 🔴 阻断 |
| **审查门控** | Reviewer 批准 | 🔴 阻断 |

---

### 阶段 3：运维（Operation）

**目标**：功能上线并稳定运行，收集真实反馈。

**入口标准**：所有 Unit 通过 Backpressure Gate
**出口标准**：运行指标达标，无 P0/P1 故障

#### 关键活动

| 活动 | 说明 |
|------|------|
| **部署** | 使用蓝绿/金丝雀发布，降低风险 |
| **监控** | 关键指标：错误率、延迟、吞吐量 |
| **告警** | P0（立即处理）、P1（2小时内）、P2（24小时内） |
| **日志** | 结构化日志，可追踪到具体 Intent/Unit |
| **反馈收集** | 用户行为数据、错误报告、性能数据 |

#### 运维检查清单

```markdown
# Operation Checklist

## 部署前
- [ ] 回滚方案已准备
- [ ] 数据库迁移脚本已测试
- [ ] 配置项已核对

## 部署中
- [ ] 金丝雀流量比例：5% → 25% → 50% → 100%
- [ ] 每阶段观察 10 分钟，指标正常才继续

## 部署后
- [ ] 错误率 < 0.1%
- [ ] P95 延迟 < 200ms
- [ ] 无 P0/P1 告警持续 1 小时
```

---

### 阶段 4：反思（Reflection）

**目标**：复盘全过程，沉淀经验，改进流程。

**入口标准**：功能稳定运行至少 1 个迭代周期
**出口标准**：Reflection 文档产出，改进项进入 backlog

#### 关键产出：Reflection 文档

```markdown
# Reflection: {功能名称}

## 执行摘要
- 计划工期：x 天
- 实际工期：y 天
- 偏差原因：...

## 做得好的
1. ...
2. ...

## 做得不好的
1. ...
2. ...

## 意外发现
- ...

## 改进项
| 改进项 | 优先级 | 负责人 | 预计工时 |
|--------|--------|--------|---------|
| ... | P0/P1/P2 | ... | ... |

## 知识沉淀
- 模式：{可复用的设计/代码模式}
- 陷阱：{踩过的坑及避免方法}
- 工具：{好用的工具/脚本}
```

#### 反思会议议程（AI 版）

```
1. Scribe 回顾全过程（Intent → Units → Operation）
2. Planner 评估范围控制是否准确
3. Builder 评估技术决策是否恰当
4. Reviewer 评估代码质量趋势
5. Red Team 指出遗漏的风险
6. 全体讨论改进项，按优先级排序
7. Scribe 记录并归档
```

---

## 🔗 DAG 依赖编排

复杂项目的多个 Unit 之间存在依赖关系，用 DAG（有向无环图）管理：

```
Unit A（用户模型）
   ↓
Unit B（认证服务） ←→ Unit C（权限服务）
   ↓                    ↓
Unit D（API 网关） ← Unit E（业务接口）
   ↓
Unit F（前端页面）
```

**执行规则**：
- 无依赖的 Unit 可并行开发
- 有依赖的 Unit 必须等前置 Unit 通过 Gate
- 发现循环依赖时，Planner 重新拆分

---

## 💡 使用示例

### 示例1：Bug 修复（快速流程）

```
用户：生产环境登录接口偶尔 500 错误

AI-DLC：
1. Elaboration（Planner）：
   - 收集日志、复现条件、影响范围
   - 输出 Intent："修复登录接口偶发 500 错误"

2. Execution（Builder + Reviewer）：
   - Unit：修复连接池超时问题
   - Backpressure：单元测试 + 类型检查 + 审查

3. Operation（Blue Team）：
   - 金丝雀发布，监控错误率

4. Reflection（Scribe）：
   - 根因：连接池配置不合理
   - 改进：建立连接池配置规范
```

### 示例2：新功能开发（完整流程）

```
用户：加一个用户积分系统

AI-DLC：
1. Elaboration（Planner + Skeptic + Red Team）：
   - Intent：用户积分获取/消费/查询
   - Skeptic：质疑是否需要实时计算
   - Red Team：攻击并发一致性假设
   - 最终 Intent 确认

2. Execution（多 Unit DAG）：
   - Unit 1：积分数据模型（无依赖）
   - Unit 2：积分获取接口（依赖 Unit 1）
   - Unit 3：积分消费接口（依赖 Unit 1）
   - Unit 4：积分查询接口（依赖 Unit 1）
   - Unit 5：前端积分页面（依赖 Unit 4）
   - 每个 Unit 通过 Backpressure Gate

3. Operation：
   - 灰度发布，监控积分一致性

4. Reflection：
   - 并发处理方案有效
   - 改进：积分日志需要更详细的审计
```

---

## 🆚 与其他方法论的关系

| | AI-DLC | BMAD | OpenSpec-SDD |
|---|---|---|---|
| **核心** | 四阶段生命周期 | 多角色协作 | 规范先行 |
| **特色** | 质量门控 + 反思 | 文档分片 + 上下文工程 | 六阶段评审 |
| **适用** | 全流程项目管理 | 中大型产品开发 | 需求对齐 |
| **最佳组合** | AI-DLC 管流程 + BMAD 管角色 + SDD 管规范 |

**推荐组合方式**：
```
AI-DLC 四阶段框架
├── Elaboration：调用 OpenSpec-SDD 做规范评审
├── Execution：调用 BMAD 的多角色协作开发
│   ├── Planner → PM
│   ├── Builder → Dev
│   └── Reviewer → QA
├── Operation：调用 systematic-debugging 处理线上问题
└── Reflection：调用 hermes-experience 沉淀经验
```

---

## 🚀 快速开始

```
用户：我想用 AI-DLC 方法开发一个 [功能]

AI：
1. 确认进入 Elaboration 阶段
2. Planner 帽子：分析需求，输出 Intent
3. 用户确认 Intent
4. 进入 Execution 阶段，Builder 拆分 Units
5. 逐个实现，通过 Backpressure Gate
6. 进入 Operation 阶段（如需上线）
7. 进入 Reflection 阶段（运行稳定后）
```

---

> "质量不是测试出来的，是流程保证的。AI-DLC 让质量内建于每个阶段。"
