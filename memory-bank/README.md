# Memory Bank - 项目记忆系统

> 快速为项目搭建 AI 友好的文档结构，让 AI Agent 每次都能"秒懂"项目

---

## 🎯 是什么

Memory Bank 是一套**项目文档结构规范**，包含：
- AI 必读的全局上下文文件（AGENTS.md）
- 快速导航索引
- 开箱即用的开发模板
- 技术决策记录（ADR）
- 项目规则（配套 hermes-experience）

---

## 📁 目录结构

```
memory-bank/
├── AGENTS.md           # 🔴 核心：项目全局上下文（必读）
├── INDEX.md            # 文件导航
├── README.md           # 项目说明
├── templates/          # 开发模板
│   ├── 01-project-profile.md     # 项目概况
│   ├── 07-coding-standards.md    # 编码规范
│   ├── 09-todo-tracker.md        # TODO追踪
│   ├── 10-snippets.md            # 代码片段
│   ├── 11-feign-guide.md         # Feign调用
│   ├── 12-mq-guide.md           # MQ使用
│   ├── feature-prompt.md         # 功能开发
│   ├── bugfix-prompt.md          # Bug修复
│   ├── code-review-prompt.md    # 代码审查
│   └── test-prompt.md            # 测试用例
├── knowledge/          # 技术决策记录（ADR）
├── rules/              # 项目规则（hermes-experience配套）
└── projects/           # 各模块详细文档
```

---

## 🚀 快速开始

```
用户：帮我搭建项目记忆系统
AI：请告诉我项目名称和技术栈

用户：CRM系统，Java Spring Boot + MySQL
AI：[生成完整的 memory-bank 目录结构]
```

---

## 📋 初始化流程

1. 收集项目信息（名称/技术栈/路径）
2. 创建记忆库目录
3. 生成 AGENTS.md 和模板文件
4. 创建项目规则文件
5. 更新项目清单

---

## 🔗 相关 Skill

- [hermes-experience](../hermes-experience/) - 经验沉淀（rules/snippets/patterns）
- [memory-system](../memory-system/) - Java 缓存/会话/消息队列技术方案
- [mysql-java-codegen](../mysql-java-codegen/) - MySQL 建表 + Java 代码生成
