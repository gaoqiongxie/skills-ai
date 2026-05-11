---
name: "claude-obsidian-reporter"
description: "Obsidian报告生成器：自动读取Git提交记录，生成Obsidian格式的日报/周报/月报。当用户说'生成Obsidian报告'、'Git提交转笔记'、'自动日报'、'Obsidian周报'、'开发日志'、'提交记录汇总'、'工作日志自动生成'时触发。核心特点：Git解析、Obsidian格式、模板定制、时间维度聚合。"
---

> **来源**: Anthropic Skills PR #664
>
> **发布时间**: 2026-05
>
> **理念**: "让 Git 提交替你写周报。"

# 📓 Claude Obsidian Reporter — Obsidian 报告生成器

自动将 Git 提交记录转化为结构化的 Obsidian 笔记。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **Git 解析** | 读取指定时间范围的提交记录、分支、合并 |
| **智能分类** | 按 feat/fix/docs/refactor 等类型归类提交 |
| **Obsidian 格式** | 输出标准 Markdown + YAML Frontmatter + WikiLinks |
| **多时间维度** | 日报（当日）、周报（本周）、月报（本月） |
| **模板定制** | 支持自定义报告模板 |
| **标签自动提取** | 从提交信息提取项目/模块标签 |

---

## 📋 报告模板

### 日报模板

```markdown
---
date: 2026-05-09
type: daily-report
tags: [dev-log, backend]
---

# 开发日报 — 2026-05-09

## 今日提交 (5)

### ✨ 功能
- `feat(auth): 实现JWT刷新令牌` ([a1b2c3d])
- `feat(user): 添加用户资料编辑` ([b2c3d4e])

### 🐛 修复
- `fix(api): 修复订单查询NPE` ([c3d4e5f])

### 📝 文档
- `docs(readme): 更新API文档` ([d4e5f6g])

## 代码统计
- 新增: +320 行
- 删除: -85 行
- 文件变更: 7

## 明日计划
- [ ] 完成支付接口对接
- [ ] 补充单元测试
```

### 周报模板

```markdown
---
week: "2026-W19"
date-range: "2026-05-05 ~ 2026-05-11"
type: weekly-report
tags: [weekly, sprint-3]
---

# 周报 — Sprint 3 第2周

## 本周概览
- 总提交: 23
- 功能完成: 3
- Bug修复: 5
- 文档更新: 2

## 主要进展
[[feat-payment-gateway]] — 支付网关对接（完成 80%）
[[fix-memory-leak]] — 修复内存泄漏问题

## 代码趋势
- 后端: +1,240 / -320
- 前端: +680 / -150
- 测试: +420 / -80

## 下周计划
- [ ] 支付接口联调
- [ ] 性能压测
```

---

## 🚀 使用方式

### 方式一：生成日报

```
生成今天的开发日报
仓库路径: D:/xgq/work/myproject
```

### 方式二：生成周报

```
生成本周的周报
时间范围: 本周一 至 今天
输出到: D:/xgq/Obsidian/Weekly/
```

### 方式三：生成月报

```
生成上个月的月报
包含代码统计、提交趋势、主要里程碑
```

---

## 🔗 与其他 Skill 的关系

| | claude-obsidian-reporter | weekly-report | git-commit |
|---|---|---|---|
| **输入** | Git 提交记录 | 工作内容描述 | 变更文件 |
| **输出** | Obsidian Markdown | 周报文本 | 提交信息 |
| **最佳组合** | git-commit 规范提交 → claude-obsidian-reporter 自动生成报告 → weekly-report 润色汇报内容 |

---

> "你的每一次 commit 都在讲述一个故事，Reporter 帮你把它写成日记。"
