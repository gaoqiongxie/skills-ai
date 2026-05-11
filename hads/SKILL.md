---
name: "hads"
description: "人-AI双读文档标准（Human-AI Document Standard）：一套轻量级Markdown约定，让文档同时服务于人类读者和AI理解。当用户说'双读文档'、'人机共读'、'AI友好的文档'、'文档标准'、'HADS'、'AI文档规范'、'结构化文档'时触发。核心特点：语义标记、AI解析友好、人类可读、版本兼容。"
---

> **来源**: Anthropic Skills PR #616 (Human-AI Document Standard)
>
> **发布时间**: 2026-05
>
> **理念**: "写一份文档，服务两种读者——人类和 AI。"

# 📋 HADS — Human-AI Document Standard

人-AI 双读文档标准：让 Markdown 同时服务于人类理解和 AI 解析。

---

## 🎯 核心概念

传统文档的困境：
- 人类看得懂，AI 理解偏
- AI 解析准，人类阅读累

HADS 的解决方案：
- **语义标记** — 用轻量约定传达结构含义
- **双重兼容** — 不破坏人类阅读体验，增强 AI 解析精度
- **渐进增强** — 按需添加 AI 提示，不强制全套使用

---

## 📝 HADS 标记规范

### 1. 文档元信息（YAML Frontmatter）

```markdown
---
title: "用户认证模块设计"
author: "张三"
date: 2026-05-09
version: "1.2"
hads-version: "1.0"
type: "design-doc"        # design-doc | api-spec | prd | adr
topics: [auth, security, jwt]
audience: [developer, ai]
---
```

### 2. 语义标题标记

```markdown
# [DESIGN] 认证模块架构设计
## [CONTEXT] 背景与现状
## [DECISION] 架构决策
### [OPTION-A] 方案一：Session + Cookie
### [OPTION-B] 方案二：JWT + Refresh Token  ⭐ SELECTED
## [RATIONALE] 决策理由
## [IMPLICATION] 影响与风险
## [TODO] 待办事项
```

### 3. AI 提示块

```markdown
<!-- AI-NOTE: 这是核心决策，后续讨论不要偏离 -->
<!-- AI-CONTEXT: 见 docs/architecture/auth-v1.md 第 3 节 -->
<!-- AI-TODO: 需要补充性能测试数据 -->
<!-- AI-WARNING: 此方案在分布式环境下有已知问题 -->
```

### 4. 结构化表格

```markdown
| 属性 | 值 | [AI-TYPE] |
|------|-----|-----------|
| 接口路径 | /api/v1/auth/login | string |
| 方法 | POST | enum:GET,POST,PUT,DELETE |
| 认证要求 | 否 | boolean |
| 限流 | 100/min | rate-limit |
```

### 5. 决策记录（ADR 精简版）

```markdown
## [ADR-001] 使用 JWT 替代 Session

- **状态**: ✅ ACCEPTED
- **日期**: 2026-05-01
- **决策者**: @张三, @李四

### 上下文
<!-- AI-SUMMARY: 单体应用迁移到微服务，Session 共享成本高 -->

### 决策
采用 JWT + Redis 刷新令牌方案。

### 后果
- ✅ 无状态，易于水平扩展
- ✅ 跨服务认证简单
- ⚠️ Token 吊销需要额外机制
- ❌ Token 体积大于 Session ID
```

---

## 🆚 与普通 Markdown 的区别

| 场景 | 普通 Markdown | HADS |
|------|--------------|------|
| 标题 | `# 背景` | `## [CONTEXT] 背景` |
| 注释 | HTML 注释不可见 | `<!-- AI-NOTE: -->` AI 可见 |
| 表格 | 纯展示 | 加 `[AI-TYPE]` 标注数据类型 |
| 决策 | 分散在段落中 | `[DECISION]` + `[RATIONALE]` 结构化 |

---

## 🚀 使用方式

### 方式一：转换现有文档

```
把这份普通 Markdown 转成 HADS 格式
```

### 方式二：创建新文档

```
用 HADS 标准写一份 API 设计文档
```

### 方式三：审查文档兼容性

```
检查这份文档是否符合 HADS 标准，AI 能否准确解析
```

---

## 💡 最佳实践

### DO
- ✅ 在团队文档中渐进引入 HADS 标记
- ✅ 关键决策使用 `[DECISION]` + `[RATIONALE]`
- ✅ 用 `<!-- AI-NOTE -->` 标注容易误解的地方
- ✅ 保持标记简洁，不牺牲人类可读性

### DON'T
- ❌ 每个标题都加语义标记（过度工程）
- ❌ 用 HADS 替代清晰的自然语言
- ❌ 在对外文档中使用内部 AI 标记

---

## 🔗 与其他 Skill 的关系

| | HADS | openspec-sdd | prd-to-demo |
|---|---|---|---|
| **用途** | 文档格式标准 | 需求规范流程 | 原型生成 |
| **最佳组合** | openspec-sdd 输出规范 → HADS 格式化 → prd-to-demo 生成原型 |

---

> "好的文档标准，让人类和 AI 都能一次读懂。"
