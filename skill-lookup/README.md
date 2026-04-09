# Skill Lookup - Skills发现与安装助手

> **来源**: skills.sh (418K+ 安装量) - AI Skills生态系统核心元技能
> 
> **参考**: github.com/anthropics/skills, github.com/JackyST0/awesome-agent-skills

---

## 📌 什么是Skill Lookup？

**Skill Lookup** 是一个"元技能"(Meta-Skill)，它的唯一职责是帮助用户**发现和安装其他Skills**。

当你听到用户问：
- "有没有做xxx的skill"
- "帮我找个xxx助手"
- "有什么好用的skill推荐"

你就知道该用这个技能了！

---

## 🔍 如何使用

### 1️⃣ 分析需求

提取用户需求的核心关键词，判断属于哪类：

| 类别 | 示例需求 |
|-----|---------|
| 写作文案 | 朋友圈文案、写封信、诗词匹配 |
| 生活决策 | 中午吃什么、送礼、明天穿什么 |
| 学习辅导 | 错题分析、背课文、口算练习 |
| 职场工作 | 会议纪要、周报、请假、怼人 |
| 创意娱乐 | 墓志铭、星座抽签、睡前故事 |
| 开发技术 | PDF处理、Word文档、Excel表格 |
| 家居生活 | 断舍离、装修、绿植、收纳 |

### 2️⃣ 搜索Skills库

**本地路径**：
- 用户级：`~/.workbuddy/skills/`
- 项目级：`.workbuddy/skills/`

### 3️⃣ 推荐格式

```markdown
📦 发现匹配Skill: food-picker

✅ 功能：纠结吃什么时，快速帮你做决定
📍 路径：D:\xgq\work\skills-ai\food-picker\
💡 示例："中午吃啥？3个人，川菜，50元预算"
```

---

## 📚 热门Skills推荐（按类别）

### 💼 职场必备
| Skill | 功能 | 来源 |
|-------|------|------|
| meeting-notes | 会议纪要整理 | 本地 |
| weekly-report | 周报生成器 | 本地 |
| leave-request | 请假话术 | 本地 |
| argue-winner | 吵架赢对面 | 本地 |
| anti-pua | 反PUA话术 | 本地 |

### 🎨 生活常用
| Skill | 功能 | Stars |
|-------|------|-------|
| food-picker | 外卖选择困难终结者 | 本地 |
| gift-advisor | 礼物参谋 | 本地 |
| outfit-weather | 穿搭天气助手 | 本地 |
| recipe-random | 菜谱随机抽 | 本地 |

### 📚 学习教育
| Skill | 功能 | Stars |
|-------|------|-------|
| study-buddy | 小学生陪练 | 本地 |
| wrong-answer | 错题本分析 | 本地 |
| knowledge-card | 知识卡片 | 本地 |

### 💡 创意有趣
| Skill | 功能 | Stars |
|-------|------|-------|
| poetry-scenery | 诗意风景描述 | 本地 |
| moments-copywriter | 朋友圈文案 | 本地 |
| epitaph-generator | 墓志铭生成 | 本地 |

---

## 🌐 热门Skills市场

当本地没有匹配时，可参考：

### 官方市场
| 市场 | 地址 | 特点 |
|-----|------|------|
| **Anthropic官方** | github.com/anthropics/skills | ⭐114K，权威可靠 |
| **Superpowers** | obra.github.io/superpowers | ⭐142K，开发方法论 |

### 社区精选
| 市场 | 地址 | 特点 |
|-----|------|------|
| **awesome-agent-skills** | github.com/JackyST0/awesome-agent-skills | 精选列表 |
| **SkillsMap** | awesomeskills.dev | 最大目录 |
| **skills.sh** | skills.sh | 一键安装 |

### 热门开发Skills Top 5
| Skill | Stars | 用途 |
|-------|-------|------|
| create-pr | 169.7K | 自动创建GitHub PR |
| skill-lookup | 142.6K | Skills搜索引擎 |
| frontend-code-review | 126.3K | 前端代码审查 |
| component-refactoring | 126.3K | React组件重构 |
| cache-components-expert | 137.2K | LLM缓存优化 |

---

## 🚀 安装新Skill

如果用户需要安装新的Skill：

```bash
# 用户级安装（推荐）
cp -r <skill-path> ~/.workbuddy/skills/

# 项目级安装
cp -r <skill-path> .workbuddy/skills/
```

---

## 💡 组合使用建议

多个Skills可以组合使用，发挥更大威力：

| 场景 | Skills组合 |
|-----|-----------|
| 写好周报再发朋友圈 | weekly-report + moments-copywriter |
| 辅导孩子学习 | study-buddy + wrong-answer |
| 断舍离+收纳 | declutter-judge + home-storage |
| 职场全面防护 | anti-pua + argue-winner + leave-request |
