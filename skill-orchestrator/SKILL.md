---
name: "skill-orchestrator"
description: "Skill编排器：111个Skills的统一智能入口。根据你的需求自动匹配最佳Skill，并推荐多Skill组合工作流。当用户说'帮我选skill'、'推荐技能'、'完整工作流'、'从需求到上线'、'帮我规划怎么用AI'、'不知道该用哪个'、'怎么组合使用'时触发。核心特点：场景智能匹配、多Skill串联编排、递进式推荐、与skill-lookup/skill-quality-analyzer协同。"
---

> **来源**: 自建（你的 Skills 库专属导航）
>
> **发布时间**: 2026-08
>
> **理念**: "111 个 Skills 不是负担，是 111 把工具。编排器就是知道你要什么，并把对的工具递到你手里。"

# 🎛️ Skill 编排器

一句话描述需求，自动匹配最佳 Skill 或 Skill 组合。不知道用哪个 Skill 时，先找我。

---

## 快速使用

### 方式一：直接说场景

```
"我想做一个电商小程序，从需求到上线"           → 启动完整开发工作流
"帮我分析这个 Bug"                              → 启动调试工作流
"设计一个科技感的产品页"                        → 启动设计工作流
"下周去云南玩，帮我规划"                        → 启动旅行工作流
"这个截图帮我转成原型再写成PRD"                 → 启动截图→原型→PRD工作流
"要写周报，但内容很乱"                          → 启动周报工作流
"想学个新技能，但不知道怎么开始"                → 启动学习工作流
```

### 方式二：问"我该用什么"

```
"我该用什么 skill 来...?"
"有没有 skill 可以...?"
"哪个 skill 适合...?"
"帮我选 skill"
"推荐个工作流"
```

### 方式三：递进式探索

如果你只说了一个模糊需求，我会：
1. **先给你一个核心 Skill** 解决最直接的问题
2. **再推荐下一步 Skill** 把结果推进下去
3. **最后给出完整工作流** 供你选择

---

## 技能雷达：按场景找 Skill

### 想写代码 / 做项目

| 阶段 | 推荐 Skill |
|------|-----------|
| 需求理解 | `openspec-sdd`、`brainstorming`、`prd-to-demo` |
| 架构设计 | `database-designer`、`erd-document`、`api-doc-generator`、`diagram-design` |
| UI 设计 | `frontend-design`、`huashu-design`、`taste-skill` |
| 前端开发 | `web-artifacts-builder`、`frontend-code-review`、`stop-slop` |
| 后端开发 | `backend-change-flow`、`enterprise-crm-fullstack` |
| 数据库 | `database-designer`、`postgres-pro` |
| 测试 | `testing-patterns`、`webapp-testing`、`test-driven-development` |
| 安全 | `security-audit`、`cybersecurity-skills` |
| 部署 | `devops-toolchain`、`cloudflare-worker`、`solo-parallel-dev` |
| 质量门控 | `quality-gate`、`create-pr`、`document-typography` |
| 记忆沉淀 | `memory-hub`、`hermes-experience` |

### 想调试 / 排错

```
报错信息 → systematic-debugging（根因分析）
    → confidence-check（评估修复方案可信度）
    → karpathy-skills（检查常见错误）
    → 修复 → test-driven-development（补测试）
    → git-commit（提交）
    → hermes-experience（沉淀经验）
```

### 想做设计 / 生成内容

```
需求描述 → frontend-design / huashu-design（视觉方向）
    → screenshot-to-prototype（有截图时）
    → prd-to-demo（快速原型）
    → web-artifacts-builder（生产级实现）
    → taste-skill（去 AI 味）
```

### 想写文档 / 做汇报

```
工作内容 → weekly-report（周报）
    → meeting-notes（会议纪要）
    → html-ppt-skill（PPT）
    → elevator-pitch（口头汇报）
```

### 想学习 / 成长

```
想学 XX → skill-accelerator（学习路径）
    → knowledge-card（整理笔记）
    → ai-trend-radar（了解趋势）
    → hermes-experience（沉淀经验）
```

### 想处理生活琐事

```
纠结吃什么 → food-picker
准备出行 → travel-planner + weather-pro + outfit-weather
选礼物 → gift-advisor
心情不好 → venting-hole / choice-helper
```

---

## 模糊匹配示例

| 你说 | 推荐 Skill / 工作流 |
|------|---------------------|
| "帮我写个网页" | `web-artifacts-builder` 或 `huashu-design` |
| "这个页面好丑" | `taste-skill` |
| "接口报 500" | `systematic-debugging` |
| "从零做一个任务管理工具" | `dev-flow` / `enterprise-iteration-agent` 完整路径 |
| "写周报" | `weekly-report` |
| "不知道怎么请假" | `leave-request` |
| "想学 Python" | `skill-accelerator` |
| "老板说我效率低" | `anti-pua` |
| "这张截图帮我转成可开发的产品" | `screenshot-to-prototype` → `prd-to-demo` → `web-artifacts-builder` |
| "帮我设计数据库" | `database-designer` |
| "数据库慢查询" | `postgres-pro` |
| "怎么部署到 K8s" | `devops-toolchain` |
| "代码安全检查" | `security-audit` |
| "威胁狩猎" | `cybersecurity-skills` |
| "AI 趋势" | `ai-trend-radar` |
| "去 AI 味" | `stop-slop` |
| "帮我选 skill" | 本 Skill |
| "评估这个 skill" | `skill-quality-analyzer` |
| "找新的 skill" | `skill-lookup` |
| "把 API 封装给 AI 用" | `mcp-builder` |
| "多个 AI 一起干活" | `multi-agent-orchestration` |
| "代码库太乱" | `codebase-inventory-audit` |
| "我想 Vibe Coding" | `vibe-coding` |

---

## 标准工作流

### 工作流 1：从零开发一个产品（完整版）

```
需求描述
  → openspec-sdd（写规范）
  → prd-to-demo（生成原型与客户确认）
  → frontend-design / huashu-design（UI 设计）
  → database-designer（数据库设计）
  → backend-change-flow / enterprise-crm-fullstack（后端开发）
  → web-artifacts-builder（前端实现）
  → testing-patterns + security-audit（测试与安全）
  → quality-gate（质量门控）
  → create-pr（生成 PR）
  → devops-toolchain（部署上线）
  → memory-hub（沉淀经验）
```

### 工作流 2：快速开发一个功能（精简版）

```
需求描述
  → brainstorming（技术方案）
  → writing-plans（任务拆分）
  → test-driven-development（编码+测试）
  → git-commit（提交）
```

### 工作流 3：代码审查 / 质量保证

```
代码变更
  → quality-gate（五维检查）
  → frontend-code-review / backend-change-flow（专项审查）
  → security-audit（安全扫描）
  → create-pr（生成 PR）
```

### 工作流 4：设计驱动开发

```
截图 / 需求
  → screenshot-to-prototype（生成原型）
  → screenshot-to-prd（输出 PRD）
  → frontend-design（UI 设计）
  → web-artifacts-builder（前端实现）
```

### 工作流 5：问题排查

```
报错 / 异常
  → systematic-debugging（根因分析）
  → confidence-check（评估方案）
  → karpathy-skills（避坑检查）
  → 修复 → testing-patterns（补测试）
  → git-commit（提交）
  → hermes-experience（沉淀）
```

---

## 智能匹配逻辑

编排器按以下优先级匹配：

1. **直接关键词匹配** — 描述中包含 Skill 的触发词
2. **场景推断** — 根据上下文推断最适合的 Skill
3. **组合推荐** — 复杂任务推荐多个 Skill 的组合工作流
4. **追问澄清** — 信息不足时询问细节，精准匹配

---

## 与其他元技能的关系

| Skill | 角色 | 何时用它 |
|-------|------|---------|
| **skill-orchestrator** | 自动匹配 + 工作流推荐 | 不知道用哪个 Skill / 要组合多个 |
| **skill-lookup** | 搜索发现 | 想找新的 Skill / 按关键词浏览 |
| **skill-quality-analyzer** | 质量评估 | 评估 Skill 质量 / 优化 description |
| **skill-creator** | 创建新 Skill | 现有 Skill 都不满足需求 |

**最佳组合**：
```
不知道用哪个 → skill-orchestrator
找不到想要的 → skill-lookup
想优化 Skill → skill-quality-analyzer
完全缺失 → skill-creator
```

---

## 最佳实践

### DO
- ✅ 直接描述场景，不用记 Skill 名字
- ✅ 复杂任务直接说"帮我走完整流程"
- ✅ 不确定时说"我该用什么 skill"
- ✅ 多任务时说"先帮我做 A，再做 B"

### DON'T
- ❌ 不用记住 111 个 Skill 的名字
- ❌ 不用纠结"这个该用 A 还是 B"
- ❌ 不用手动串联多个 Skill

---

## 快速入口

```
"帮我选 skill"
"不知道该用什么"
"从需求到上线"
"完整工作流"
"帮我搭配"
"推荐个工作流"
```

---

> "你不需要记住 111 个 Skill，只需要记住 1 个 —— Skill 编排器。"
