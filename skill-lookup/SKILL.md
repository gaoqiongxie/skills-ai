---
name: "skill-lookup"
description: "元技能：搜索和发现WorkBuddy可用的Skills，支持一键安装。本技能可帮助用户找到满足特定需求的Skill，当用户询问'有什么skill'、'有没有xxx的skill'、'推荐一个skill'时触发。"
---

# Skill Lookup - Skills发现与安装助手

> **来源**: skills.sh (418K+ 安装量) - AI Skills生态系统核心元技能
> 
> **参考**: github.com/anthropics/skills, github.com/JackyST0/awesome-agent-skills

## 核心定位

Skill Lookup是一个"元技能"(Meta-Skill)，它的唯一职责是帮助用户发现和安装其他Skills。当你不确定某个功能是否有现成的Skill时，先用这个技能来搜索。

## 工作流程

### 1. 理解用户需求

当用户提出类似问题时触发：
- "有没有做xxx的skill"
- "帮我找个xxx助手"
- "有什么好用的skill推荐"
- "我想做xxx，有什么工具吗"

**分析步骤**：
1. 提取用户需求的核心关键词
2. 判断需求类别（工作/生活/学习/创意/开发）
3. 搜索现有Skills库

### 2. 搜索Skills库

检查本地Skills库 `~/.workbuddy/skills/` 和项目Skills `.workbuddy/skills/`

**常见需求匹配**：

| 需求类型 | 可能匹配的Skills |
|---------|-----------------|
| 写作/文案 | moments-copywriter, letter-future, poetry-scenery |
| 生活决策 | food-picker, gift-advisor, outfit-weather, recipe-random |
| 学习辅导 | study-buddy, wrong-answer, knowledge-card |
| 职场工作 | meeting-notes, weekly-report, leave-request, argue-winner |
| 创意娱乐 | epitaph-generator, horoscope, emoji-translator, sleep-story |
| 开发技术 | docx, pdf, pptx, xlsx (Anthropic官方) |
| 家居生活 | declutter-judge, home-design, plant-care, home-storage |
| 情感倾诉 | venting-hole, choice-helper |

### 3. 推荐与安装

**推荐格式**：
```
📦 发现匹配Skill: [skill-name]

功能描述：一句话说明功能
来源：标明是本地已有还是需要安装
安装方式：如果是新Skill，告知安装路径
使用示例：给出1-2个使用示例
```

**安装新Skill**：
- 用户级安装：`cp -r <skill-path> ~/.workbuddy/skills/`
- 项目级安装：`cp -r <skill-path> .workbuddy/skills/`

## Skills市场资源

当本地没有匹配时，可参考以下热门市场：

### 官方市场
- **Anthropic官方Skills**: github.com/anthropics/skills (114K⭐)
  - docx, pdf, pptx, xlsx, 创意类技能
  
### 社区精选
- **awesome-agent-skills**: github.com/JackyST0/awesome-agent-skills (441⭐)
  - 精选列表，支持一键安装脚本
  
### 热门开发Skills (Top 20)
| Skill | Stars | 用途 |
|-------|-------|------|
| create-pr | 169.7K | 自动创建GitHub PR |
| frontend-code-review | 126.3K | 前端代码审查 |
| component-refactoring | 126.3K | React组件重构 |
| cache-components-expert | 137.2K | LLM缓存优化 |

### 热门平台
- **skills.sh**: skills.sh - 一键安装
- **awesomeskills.dev**: awesomeskills.dev - 最大精选目录
- **MCP Market**: agentskill.sh - 36万+ Skills

## 需求扩展

如果现有Skills都不能满足需求，可以：

1. **组合现有Skills**：多个简单Skills组合使用
2. **创建新Skill**：参考 skill-creator 指引创建
3. **推荐外部工具**：非Skills类的优秀工具

## 注意事项

- 优先推荐本地已安装的Skills
- 标注每个Skill的来源和人气
- 安装前确认安装路径
- 提供使用示例帮助用户上手
