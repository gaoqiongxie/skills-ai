---
name: "skill-orchestrator"
description: "Skill编排器：统一管理67个Skills的智能入口，根据你的需求自动推荐最佳Skill组合和工作流。当用户说'帮我选个skill'、'不知道该用哪个'、'怎么组合使用'、'推荐技能'、'帮我搭配'、'完整工作流'、'从需求到上线'、'帮我规划怎么用AI'时触发。核心特点：场景智能匹配、多Skill串联编排、标准工作流模板、一键启动组合任务。"
---

> **来源**: 自建（你的 Skills 库专属导航）
>
> **发布时间**: 2026-05-06
>
> **理念**: "67 个 Skills 不是负担，是 67 把工具。编排器就是工具箱。"

# 🎛️ Skill 编排器

一句话描述需求，自动匹配最佳 Skill 或 Skill 组合。

---

## 🎯 使用方法

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
```

---

## 🗂️ 完整 Skill 索引

### 🔧 开发方法论类（26 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **skill-lookup** | 发现热门 Skill | 想找新的、别人在用的 Skill |
| **skill-creator** | 创建新 Skill | 想把自己的经验变成 Skill |
| **skill-orchestrator** | ⭐ 本 Skill，统一入口 | 不知道用哪个 / 要组合多个 |
| **bmad-method** | AI 敏捷团队开发 | 从零做一个完整产品 |
| **ai-dlc** | AI 开发生命周期 | 需要质量门控和阶段管理 |
| **prompt-driven-dev** | 提示词版本化开发 | 需要稳定、可重复的 AI 生成 |
| **openspec-sdd** | 规范驱动开发 | 需求模糊，要先对齐规范 |
| **systematic-debugging** | 系统化调试 | 遇到 Bug，要根因分析 |
| **test-driven-development** | TDD 测试驱动 | 写代码前先写测试 |
| **brainstorming** | 结构化头脑风暴 |  coding 前思考方案 |
| **writing-plans** | 详细实施计划 | 需要可执行的任务分解 |
| **confidence-check** | AI 置信度评估 | AI 回答不确定，要它自评 |
| **karpathy-skills** | LLM 编程避坑 | 代码总出问题，要学最佳实践 |
| **hermes-experience** | 经验沉淀系统 | 想把踩过的坑记下来复用 |
| **memory-system** | 记忆系统设计 | 了解缓存/Session/消息队列原理 |
| **memory-bank** | 项目文档化记忆 | 手动维护项目核心文档 |
| **claude-mem** | 跨会话持久记忆 | 自动记录和检索项目历史 |
| **api-doc-generator** | API 文档生成 | 写接口文档 |
| **git-commit** | Git 提交规范 | 生成规范的提交信息 |
| **browser-use** | 浏览器自动化 | 网页截图、填表、抓取数据 |
| **database-designer** | 数据库设计 | 设计表结构、生成 DDL |
| **erd-document** | 系统设计文档 | 输出完整的 Word/PDF 设计文档 |
| **screenshot-to-prd** | 截图转 PRD | 有设计稿，要输出需求文档 |
| **prd-to-demo** | PRD 转原型 | 有需求文档，要生成可点击原型 |
| **screenshot-to-prototype** | 截图转原型 | 有截图/草图，直接生成原型 |
| **ai-trend-radar** | AI 趋势雷达 | 了解 AI 领域最新动态 |

### 🎨 设计类（4 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **frontend-design** | 前端 UI 设计 | 做产品界面，拒绝 AI slop |
| **huashu-design** | 花叔 HTML 设计 | 做品牌网页、落地页 |
| **diagram-design** | 编辑级图表 | 画架构图、流程图、数据可视化 |
| **html-ppt-skill** | HTML PPT 生成 | 做演示文稿，无需 PowerPoint |

### 💼 工作类（7 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **weekly-report** | 周报生成 | 周末写周报 |
| **meeting-notes** | 会议纪要 | 会议记录太乱，要整理 |
| **leave-request** | 请假话术 | 不知道怎么请假 |
| **elevator-pitch** | 电梯演讲 | 30 秒介绍项目/自己 |
| **anti-pua** | 职场反 PUA | 老板/同事说话难听 |
| **argue-winner** | 吵架应对 | 被甩锅、被投诉 |
| **bs-translator** | 废话翻译 | 把黑话翻译成人话 |

### 🎨 生活类（6 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **travel-planner** | 旅行规划 | 出去玩，要做攻略 |
| **food-picker** | 外卖选择 | 不知道吃什么 |
| **outfit-weather** | 穿搭天气 | 明天穿什么 |
| **recipe-random** | 菜谱随机 | 冰箱里有什么做什么 |
| **gift-advisor** | 礼物参谋 | 不知道送什么 |
| **weather-pro** | 专业气象 | 需要专业气象分析 |

### 📚 学习类（4 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **skill-accelerator** | 技能加速器 | 学任何新技能的方法论 |
| **knowledge-card** | 知识卡片 | 把知识整理成记忆卡片 |
| **jargon-translator** | 术语翻译 | 专业术语看不懂 |
| **wrong-answer** | 错题分析 | 分析错题，找类似题 |

### 🧠 思考/创意类（13 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **choice-helper** | 两难选择 | 选 A 还是选 B |
| **personality-test** | 人格测试 | MBTI/九型等测试 |
| **relationship-patterns** | 关系模式 | 分析亲密关系 |
| **year-summary** | 年终总结 | 年底写总结 |
| **poetry-scenery** | 诗意风景 | 用诗词发朋友圈 |
| **moments-copywriter** | 朋友圈文案 | 发圈不知道写什么 |
| **idiom-chain** | 成语接龙 | 玩成语游戏 |
| **feihua-ling** | 飞花令 | 玩诗词游戏 |
| **letter-future** | 给未来写信 | 写时间胶囊 |
| **horoscope** | 星座运势 | 看运势/抽签 |
| **rural-story-writer** | 乡土小说 | 写祖孙故事 |
| **epitaph-generator** | 墓志铭 | 思考人生意义 |
| **sleep-story** | 睡前故事 | 睡不着 |

### 🏠 居家类（5 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **photo-organizer** | 照片整理 | 相册太乱 |
| **declutter-judge** | 断舍离 | 东西扔不扔 |
| **home-design** | 装修灵感 | 想装修 |
| **plant-care** | 绿植养护 | 植物怎么养 |
| **home-storage** | 家居收纳 | 整理房间 |

### 🎮 其他（2 个）

| Skill | 一句话说明 | 何时用它 |
|-------|-----------|---------|
| **emoji-translator** | Emoji 翻译 | 不知道表情什么意思 |
| **venting-hole** | 吐槽树洞 | 心情不好想发泄 |

---

## 🔄 标准工作流（按场景）

### 场景 1：从零开发一个产品（完整版）

```
需求描述 → ai-dlc/bmad-method（启动项目管理）
    → openspec-sdd（写规范）
    → prd-to-demo（生成原型与客户确认）
    → frontend-design/huashu-design（UI 设计）
    → database-designer（数据库设计）
    → bmad-method（开发实现）
    → test-driven-development（写测试）
    → systematic-debugging（排查问题）
    → api-doc-generator（出接口文档）
    → git-commit（规范提交）
    → erd-document（出系统设计文档）
```

**一句话启动**：`"我想从零做一个 [产品名称]，帮我走完整流程"`

---

### 场景 2：快速开发一个功能（精简版）

```
需求描述 → bmad-method（快速路径）
    → brainstorming（技术方案）
    → writing-plans（任务拆分）
    → test-driven-development（编码+测试）
    → git-commit（提交）
```

**一句话启动**：`"帮我快速实现 [功能描述]"`

---

### 场景 3：排查生产 Bug

```
报错信息 → systematic-debugging（根因分析）
    → confidence-check（评估修复方案可信度）
    → karpathy-skills（检查是否犯了常见错误）
    → 修复 → test-driven-development（补充测试）
    → git-commit（提交）
    → hermes-experience（沉淀经验，避免再犯）
```

**一句话启动**：`"生产环境报错了，帮我排查"`

---

### 场景 4：设计一个页面/产品原型

```
需求描述 → prd-to-demo（快速出原型）
    或 → screenshot-to-prototype（有截图时）
    → frontend-design（UI 设计）
    或 → huashu-design（品牌网页）
    → diagram-design（需要架构图时）
```

**一句话启动**：`"帮我设计一个 [页面类型]"`

---

### 场景 5：写周报/汇报材料

```
工作内容 → weekly-report（生成周报）
    → meeting-notes（需要会议纪要时）
    → html-ppt-skill（需要做 PPT 汇报时）
    → elevator-pitch（需要做口头汇报时）
```

**一句话启动**：`"帮我写周报"` 或 `"帮我准备汇报材料"`

---

### 场景 6：学习新技能

```
想学 XX → skill-accelerator（六阶段学习法）
    → skill-lookup（找相关学习资源）
    → knowledge-card（整理学习笔记）
    → hermes-experience（沉淀为可复用经验）
```

**一句话启动**：`"我想学 [技能名称]，帮我规划"`

---

### 场景 7：规划旅行

```
想去 XX → travel-planner（完整攻略）
    → weather-pro（分析目的地天气）
    → outfit-weather（准备穿搭）
```

**一句话启动**：`"帮我规划去 [地点] 的行程"`

---

### 场景 8：截图→原型→PRD→开发（设计驱动）

```
截图 → screenshot-to-prototype（生成原型）
    → screenshot-to-prd（输出 PRD）
    → prd-to-demo（完善原型）
    → frontend-design（UI 设计）
    → bmad-method（进入开发）
```

**一句话启动**：`"这张截图帮我做成可开发的产品"`

---

### 场景 9：代码审查/质量保证

```
代码提交前 → ai-dlc（Backpressure Gate）
    → test-driven-development（测试覆盖）
    → confidence-check（自评代码质量）
    → git-commit（规范提交）
```

**一句话启动**：`"帮我审查这段代码"`

---

### 场景 10：心情/生活

```
心情不好 → venting-hole（吐槽）
    或 → choice-helper（纠结时）
    或 → personality-test（想了解自己）
    或 → sleep-story（睡不着）
    或 → year-summary（年底复盘）
```

**一句话启动**：直接描述你的状态，编排器会匹配

---

## 🧠 智能匹配逻辑

编排器根据你的描述，按优先级匹配：

### 匹配优先级

1. **直接关键词匹配** — 描述中包含 Skill 的触发词
2. **场景推断** — 根据上下文推断最适合的 Skill
3. **组合推荐** — 复杂任务推荐多个 Skill 的组合工作流
4. **追问澄清** — 信息不足时询问细节，精准匹配

### 示例匹配

| 你说 | 匹配结果 |
|------|---------|
| "帮我设计一个科技感官网" | frontend-design |
| "这个页面从截图开始做" | screenshot-to-prototype → prd-to-demo |
| "下周去云南，5天" | travel-planner + weather-pro |
| "接口报 500" | systematic-debugging |
| "从零做一个任务管理工具" | bmad-method 完整路径 |
| "写周报：完成了用户模块" | weekly-report |
| "不知道怎么请假" | leave-request |
| "想学 Python" | skill-accelerator |
| "老板说我效率低" | anti-pua |
| "这张设计稿帮我转成可开发的产品" | screenshot-to-prototype → prd-to-demo → frontend-design → bmad-method |

---

## 💡 最佳实践

### DO
- ✅ 直接描述你的场景，不用记 Skill 名字
- ✅ 复杂任务直接说"帮我走完整流程"
- ✅ 不确定时说"我该用什么 skill"
- ✅ 多任务时说"先帮我做 A，再做 B"

### DON'T
- ❌ 不用记住 67 个 Skill 的名字
- ❌ 不用纠结"这个该用 A 还是 B"
- ❌ 不用手动串联多个 Skill

---

## 🚀 快速入口

记不住的时候，直接说：

```
"帮我选 skill"
"不知道该用什么"
"从需求到上线"
"完整工作流"
"帮我搭配"
```

---

> "你不需要记住 67 个 Skill，只需要记住 1 个 —— Skill 编排器。"
