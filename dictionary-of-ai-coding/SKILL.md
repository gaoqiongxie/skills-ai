---
name: "dictionary-of-ai-coding"
description: "AI编码术语词典：用大白话解释AI编程领域的专业术语，包括skill、agent、vibe-coding、prompt-engineering等。当用户说'AI编程术语'、'这个词什么意思'、'AI黑话'、'agent是什么'、'skill和prompt的区别'、'vibe-coding是什么'、'AI编程概念'时触发。核心特点：术语速查、对比辨析、通俗解释、中英对照。"
---

> **来源**: mattpocock/dictionary-of-ai-coding
>
> **发布时间**: 2026-05
>
> **理念**: "AI 编程时代，不懂术语就像不会用工具箱。"

# 📖 Dictionary of AI Coding — AI 编码术语词典

用大白话解释 AI 编程领域的所有黑话。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **术语速查** | 快速查询任何 AI 编程相关术语 |
| **对比辨析** | 区分容易混淆的概念（如 Skill vs Prompt） |
| **通俗解释** | 不用专业术语，用类比和例子说明 |
| **中英对照** | 提供英文原词和中文翻译 |
| **关联推荐** | 查询一个术语时推荐相关术语 |

---

## 📚 核心术语表

### 基础概念

| 术语 | 英文 | 通俗解释 |
|------|------|---------|
| **Skill** | Skill | AI 的"专业技能卡"——教 AI 在特定场景下怎么做事的说明书 |
| **Prompt** | Prompt | 给 AI 的"指令"——你告诉 AI 要做什么的那段话 |
| **Agent** | Agent | AI "代理"——能自主做决策、调用工具、完成多步骤任务的 AI |
| **Vibe Coding** | Vibe Coding | "氛围编程"——用聊天 vibe 写代码，不细看 AI 生成的代码 |
| **Prompt Engineering** | Prompt Engineering | "提示工程"——研究怎么写 Prompt 让 AI 输出更好 |

### 开发与工具

| 术语 | 英文 | 通俗解释 |
|------|------|---------|
| **RAG** | Retrieval-Augmented Generation | "检索增强生成"——AI 回答前先查资料，再基于查到的内容回答 |
| **MCP** | Model Context Protocol | "模型上下文协议"——让 AI 和外部工具（如数据库、浏览器）说同一种语言的协议 |
| **Context Window** | Context Window | "上下文窗口"——AI 能记住的对话长度，超过就"失忆" |
| **Token** | Token | "词元"——AI 处理文本的最小单位，中文约 1-2 个字 |
| **Temperature** | Temperature | "温度"——AI 创造力的旋钮，0=死板，1=天马行空 |

### 方法论

| 术语 | 英文 | 通俗解释 |
|------|------|---------|
| **TDD** | Test-Driven Development | "测试驱动开发"——先写测试再写代码，确保代码满足需求 |
| **BMAD** | - | "AI 驱动敏捷开发"——让多个 AI 角色（架构师、开发、测试）协作完成项目 |
| **SDD** | Spec-Driven Development | "规范驱动开发"——先写详细规范，AI 按规范生成代码 |
| **PDD** | Prompt-Driven Development | "提示驱动开发"——把 Prompt 当代码版本化管理 |

### Agent 相关

| 术语 | 英文 | 通俗解释 |
|------|------|---------|
| **Agent Loop** | Agent Loop | "代理循环"——AI 观察→思考→行动→观察的循环 |
| **Tool Use** | Tool Use | "工具调用"——AI 调用外部工具（如搜索、计算器）完成任务 |
| **Orchestration** | Orchestration | "编排"——协调多个 AI Agent 分工协作 |
| **Swarm** | Swarm | "蜂群"——大量简单 Agent 并行工作，类似蚁群算法 |

### 质量与评估

| 术语 | 英文 | 通俗解释 |
|------|------|---------|
| **Hallucination** | Hallucination | "幻觉"——AI 一本正经地胡说八道 |
| **Confidence** | Confidence | "置信度"——AI 对自己答案的把握程度 |
| **Backpressure** | Backpressure | "背压"——质量不合格就退回重做，防止烂代码进入下游 |
| **Eval** | Evaluation | "评估"——用测试集检验 AI 的表现 |

---

## 🔄 易混淆概念辨析

### Skill vs Prompt

| | Skill | Prompt |
|---|---|---|
| **比喻** | 职业技能证书 | 具体工作指令 |
| **复用性** | 高，一个 Skill 多次使用 | 低，每次对话重新写 |
| **持久性** | 保存为文件，长期有效 | 会话结束就消失 |
| **关系** | Skill 里包含优化的 Prompt | Prompt 是 Skill 的一部分 |

### Vibe Coding vs PDD

| | Vibe Coding | PDD |
|---|---|---|
| **风格** | 随意、直觉、快速 | 结构化、精确、可控 |
| **代码审查** | 不怎么看 | 严格审查 |
| **适用场景** | 原型、探索、个人项目 | 生产、团队协作、复杂系统 |
| **风险** | 技术债累积 | 前期投入大 |

### Agent vs LLM

| | Agent | LLM |
|---|---|---|
| **能力** | 自主决策 + 调用工具 | 文本生成 + 推理 |
| **自主性** | 高，能自己规划步骤 | 低，需要人给明确指令 |
| **记忆** | 持久化记忆 | 会话级记忆 |
| **关系** | Agent 通常包含 LLM 作为大脑 | LLM 是 Agent 的核心组件 |

---

## 🚀 使用方式

### 方式一：查询术语

```
"RAG" 是什么意思？
```

### 方式二：对比概念

```
Skill 和 Prompt 有什么区别？
```

### 方式三：解释给非技术人员

```
用大白话向产品经理解释什么是 Agent
```

---

## 🔗 与其他 Skill 的关系

| | dictionary-of-ai-coding | jargon-translator | skill-orchestrator |
|---|---|---|---|
| **侧重** | AI 编程术语 | 通用专业术语 | Skill 使用指南 |
| **最佳组合** | 看不懂术语 → dictionary 查询 → skill-orchestrator 推荐相关 Skill |

---

> "术语不是障碍，是钥匙——掌握了它，你就打开了 AI 编程世界的大门。"
