# 📚 Memory Bank - 项目记忆系统

> 快速为项目搭建 AI 友好的文档结构，让 AI Agent 每次都能"秒懂"项目

---

## 🎯 是什么

Memory Bank 是一套**项目文档结构规范**，包含：
- AI 必读的全局上下文文件
- 快速导航索引
- 开箱即用的 Prompt 模板
- 技术决策记录（ADR）
- 模块化文档组织

---

## 📁 目录结构

```
memory-bank/
├── AGENTS.md           # 🔴 核心：项目全局上下文（必读）
├── INDEX.md            # 📖 文件导航
├── README.md           # 项目说明
├── templates/          # 📝 Prompt 模板
│   ├── feature-prompt.md    # 功能开发
│   ├── bugfix-prompt.md     # Bug修复
│   ├── code-review-prompt.md # 代码审查
│   └── test-prompt.md       # 测试用例
├── knowledge/          # 💡 技术决策记录（ADR）
└── projects/           # 📚 各模块详细文档
```

---

## 📄 核心文件说明

### AGENTS.md（必读）
AI Agent 启动项目时第一个读取的文件，包含：
- 项目概述和技术栈
- 代码规范和分层策略
- Git 规范和常用命令
- 环境信息和安全规范

### templates/（可选）
常用开发场景的 Prompt 模板：
| 模板 | 适用场景 |
|------|---------|
| feature-prompt.md | 新功能开发 |
| bugfix-prompt.md | Bug 修复 |
| code-review-prompt.md | 代码审查 |
| test-prompt.md | 测试用例编写 |

### knowledge/（按需）
技术决策记录（ADR），记录重要技术选型的背景和理由

---

## 🚀 快速开始

```
用户：帮我搭建项目记忆系统
AI：请告诉我项目名称和技术栈

用户：CRM系统，Java Spring Boot + MySQL
AI：[生成完整的 memory-bank 目录结构]
```

---

## ✨ 特色

- 🎯 **AI 优先**：AGENTS.md 让 AI 秒懂项目
- 📝 **模板丰富**：开箱即用的开发模板
- 🔄 **可扩展**：按需添加，自定义灵活
- 📚 **结构清晰**：INDEX.md 快速导航

---

## 📦 相关 Skill

- [memory-system](../memory-system/) - Java 缓存/会话/消息队列技术方案
- [mysql-java-codegen](../mysql-java-codegen/) - MySQL 建表 + Java 代码生成
