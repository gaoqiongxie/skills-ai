# AI Skills 工具集

> 高琼的 WorkBuddy AI 技能库 —— 让AI成为你工作生活的超级助手
>
> **数据来源**: GitHub热门Skills分析 (github.com/anthropics/skills ⭐114K, obra/superpowers ⭐142K)

---

## 📁 目录结构

```
D:\xgq\work\skills-ai\
├── README.md                     # 本文件 - Skills总览 & 使用指南
├── anti-pua/                     # 职场反PUA话术
├── poetry-scenery/               # 诗意风景描述
├── photo-organizer/              # 照片整理助手
├── rural-story-writer/           # 乡土叙事小说生成器
├── food-picker/                  # 外卖选择困难症终结者
├── gift-advisor/                 # 礼物参谋
├── outfit-weather/               # 穿搭天气助手
├── recipe-random/               # 菜谱随机抽
├── travel-planner/              # 🆕 旅行规划师·国内游（行程/住宿/美食/预算/攻略）
├── html-ppt-skill/              # 🆕 HTML PPT生成器（36主题/31布局/47动画，无需PowerPoint）
├── diagram-design/              # 🆕 编辑级图表设计（13种图表类型，纯HTML+SVG，拒绝Mermaid）
├── huashu-design/               # 🆕 花叔HTML设计（20种设计哲学/5维评审/31布局/品牌识别）
├── meeting-notes/                # 会议纪要整理助手
├── weekly-report/               # 周报生成器
├── leave-request/               # 请假话术助手
├── elevator-pitch/              # 电梯演讲生成器
├── argue-winner/                # 吵架赢对面
├── wrong-answer/                # 错题本分析助手
├── knowledge-card/              # 知识卡片生成器
├── study-buddy/                 # 小学生陪练助手
├── jargon-translator/           # 术语翻译器
├── moments-copywriter/          # 朋友圈文案生成器
├── letter-future/               # 给未来写封信
├── epitaph-generator/           # 墓志铭生成器
├── horoscope/                   # 星座解签
├── emoji-translator/            # Emoji翻译器
├── choice-helper/               # 两难选择器
├── venting-hole/                # 吐槽树洞
├── sleep-story/                 # 睡前故事
├── year-summary/                # 年终总结生成器
├── declutter-judge/             # 断舍离裁判
├── home-design/                 # 装修灵感墙
├── plant-care/                  # 绿植养护指南
├── home-storage/                # 家居收纳指南
├── skill-lookup/                 # 🆕 Skills发现助手（热门来源）
├── systematic-debugging/        # 🆕 系统化调试方法论（obra/superpowers）
├── test-driven-development/      # 🆕 TDD测试驱动开发（obra/superpowers）
├── confidence-check/            # 🆕 AI自我置信度评估（Top 20 Skills）
├── brainstorming/              # 🆕 结构化头脑风暴（obra/superpowers）
├── writing-plans/              # 🆕 详细实施计划（obra/superpowers）
├── idiom-chain/                # 🆕 成语接龙（中国传统文字游戏）
├── feihua-ling/               # 🆕 飞花令（中国古典诗词文化）
├── bs-translator/             # 🆕 废话翻译官（听不懂人话急救包）
├── personality-test/          # 🆕 人格测试大全（MBTI/九型/DISC/星座/血型）
├── relationship-patterns/     # 🆕 亲密关系模式识别（吊桥效应/PUA/煤气灯效应/吹狗哨等）
├── memory-system/            # 🆕 记忆系统（缓存/Session/消息队列）
├── memory-bank/             # 🆕 项目记忆系统（AGENTS/模板/ADR）
├── karpathy-skills/       # 🆕 LLM编程避坑指南（Karpathy最佳实践）
├── hermes-experience/     # 🆕 经验沉淀系统（Do it once, Automate forever）
├── cron-expression/      # 最强Cron表达式（生成/验证/多语言实现）
├── skill-accelerator/   # 技能加速器·滑翔伞学习法（六阶段通用方法论）
├── ai-trend-radar/      # AI趋势雷达（追踪热门AI关键词、技术概念、行业动态）
├── api-doc-generator/   # API文档生成器（Swagger/OpenAPI注解）
├── git-commit/          # Git提交规范生成器（Conventional Commits）
├── browser-use/        # 浏览器自动化（Playwright网页操作）
├── database-designer/  # 数据库设计器（ERD/Mermaid + MySQL DDL + Java Entity）
├── erd-document/      # 完整系统设计文档（Word/PDF，11章节ERD文档）
├── openspec-sdd/     # 🆕 规范驱动开发（OpenSpec六阶段+SDD+Gherkin验收场景）
├── frontend-design/   # 🆕 前端设计规范（拒绝AI slop，6大视觉方向）
├── skill-creator/     # 🆕 Skill创造者（元技能：创建/测试/优化Skills）
├── claude-mem/        # 🆕 跨会话持久记忆（自动捕获/压缩/检索，GitHub Trending #3）
├── weather-pro/       # 🆕 专业气象分析师（农业/航空/航海多场景）
├── bmad-method/       # 🆕 AI驱动敏捷开发（一人顶一团队，多角色协作）
├── ai-dlc/            # 🆕 AI驱动开发生命周期（四阶段闭环+质量门控+Hat-based）
├── prompt-driven-dev/ # 🆕 提示驱动开发（提示词版本化+确定性生成+Prompt as Code）
├── prd-to-demo/       # 🆕 PRD转可交互原型（根据需求文档生成HTML原型Demo）
├── screenshot-to-prototype/ # 🆕 截图转可交互原型（设计稿/草图自动生成HTML原型）
├── screenshot-to-prd/       # 🆕 截图转PRD（UI截图自动生成产品需求文档）
├── skill-orchestrator/ # 🆕 Skill编排器（81个Skill的统一入口，智能匹配+工作流推荐）
├── caveman-skill/     # 🆕 洞穴人Token优化（削减75%token消耗，保持技术准确）
├── supermemory/       # 🆕 跨会话持久记忆（自动加载上下文，LongMemEval基准领先）
├── multi-agent-orchestration/ # 🆕 多Agent编排框架（并行执行，worktree隔离）
├── security-audit/    # 🆕 安全审计工作流（CodeQL/Semgrep，OWASP Top 10覆盖）
├── testing-patterns/  # 🆕 全栈测试模式（单元/React/E2E/Mock，测试金字塔）
├── document-typography/ # 🆕 文档排版质量控制（孤行寡段/编号对齐/字体层级）
├── claude-obsidian-reporter/ # 🆕 Obsidian报告生成（Git提交→日/周/月报）
├── hads/              # 🆕 人-AI双读文档标准（Human-AI Document Standard）
├── skill-quality-analyzer/ # 🆕 Skill质量评估元技能（五维评分体系）
├── codebase-inventory-audit/ # 🆕 代码库清单审计（孤儿代码/重复逻辑/技术债务）
├── agent-governance/  # 🆕 AI Agent治理框架（策略/信任/审计/威胁检测）
└── dictionary-of-ai-coding/ # 🆕 AI编码术语词典（Skill/Prompt/Agent/Vibe Coding大白话）
```

---

## 🔥 热门Skills来源（本次新增标注）

| 来源项目 | Stars | 贡献的Skill理念 |
|---------|-------|----------------|
| **obra/superpowers** | ⭐ 154.2K | systematic-debugging, test-driven-development, brainstorming, writing-plans |
| **Anthropic官方Skills** | ⭐ 114K | docx, pdf, pptx, xlsx (官方文档处理) |
| **skills.sh find-skills** | 418K安装 | skill-lookup (元技能理念) |
| **Top 20 Claude Code** | 169.7K | confidence-check, create-pr (自动化理念) |
| **forrestchang/andrej-karpathy-skills** | ⭐ 42.8K | karpathy-skills (LLM编程避坑) |
| **thedotmack/claude-mem** | ⭐ 57.8K | claude-mem (跨会话持久记忆) |
| **virattt/ai-hedge-fund** | ⭐ 55K | ai-hedge-fund (AI对冲基金团队·多Agent协作) |
| **alchaincyf/huashu-design** | ⭐ 2,839（本周新晋） | huashu-design (HTML原生设计) |
| **lewislulu/html-ppt-skill** | ⭐ 1,754（本周新晋） | html-ppt-skill (HTML PPT生成) |
| **cathrynlavery/diagram-design** | ⭐ 1,320（本周新晋） | diagram-design (编辑级图表) |
| **Donchitos/Claude-Code-Game-Studios** | ⭐ 10.4K | 49个AI Agent + 72个Workflow Skill的游戏工作室 |
| **lsdefine/GenericAgent** | ⭐ 1.9K | 自进化Agent，从3.3K行种子代码生长技能树 |

---

## 🔥 2026 AI 编程热词速查

| 热词 | 含义 | 对应Skill |
|------|------|----------|
| **BMAD** | Spec-first的Agentic Agile框架，21+ AI Agent协作 | `bmad-method` |
| **AI-DLC** | AI驱动开发生命周期，四阶段闭环+质量门控 | `ai-dlc` |
| **PDD** | Prompt-Driven Development，提示词版本化+确定性生成 | `prompt-driven-dev` |
| **OpenSpec-SDD** | 规范驱动开发，Gherkin验收场景对齐需求 | `openspec-sdd` |
| **Agentic AI** | 从聊天助手进化为自主执行工作流的Agent | `multi-agent-orchestration` |
| **Context Engineering** | 比Prompt Engineering更高级的信息环境优化 | `bmad-method` |
| **Vibe Coding** | 自然语言驱动开发，45%AI生成代码有安全漏洞 | 待补充 |
| **MCP** | Model Context Protocol，AI工具集成标准 | 待补充 |
| **Repository Intelligence** | AI理解整个代码库、提交历史、架构意图 | 待补充 |
| **Skill供应链安全** | Snyk发现36%的skills存在恶意提示注入 | `security-audit` |

---

## 🚀 已安装的 Skills（81个）

### 🔧 开发方法论类（40个）

| Skill名称 | 功能 | 来源 | Stars |
|----------|------|------|-------|
| **skill-orchestrator** | ⭐ Skill编排器：81个Skill的统一智能入口，场景匹配+工作流推荐 | 自建 | - |
| **skill-lookup** | Skills发现与安装助手 | skills.sh | 418K安装 |
| **systematic-debugging** | 系统化调试方法论，4阶段根因分析 | obra/superpowers | 142K |
| **test-driven-development** | TDD测试驱动开发，红-绿-重构循环 | obra/superpowers | 142K |
| **brainstorming** | 结构化头脑风暴，编码前思考 | obra/superpowers | 142K |
| **writing-plans** | 详细实施计划生成 | obra/superpowers | 142K |
| **confidence-check** | AI自我置信度评估 | Top 20 Skills | 19.8K |
| **memory-system** | 记忆系统：Redis缓存/多级缓存/分布式Session/消息队列 | 自建 | - |
| **memory-bank** | 项目记忆系统：AGENTS/INDEX/模板/ADR文档结构 | 自建 | - |
| **karpathy-skills** | LLM编程避坑：十大戒律/调试流程/提问模板 | karpathy-skills ⭐14.6K | 14.6K |
| **hermes-experience** | 经验沉淀：patterns/snippets/rules，让AI越用越懂你 | hermes-agent ⭐62.8K | 62.8K |
| **cron-expression** | 最强Cron：50+速查表/自然语言生成/Java+MySQL实现 | 自建 | - |
| **skill-accelerator** | 技能加速器·滑翔伞学习法：六阶段通用方法论 | 自建 | - |
| **api-doc-generator** | API文档生成：Swagger注解/@ApiOperation/字段说明/OpenAPI文档 | awesome-agent-skills | - |
| **git-commit** | 规范化Git提交：Conventional Commits格式/多场景模板/分支命名规范 | awesome-agent-skills | - |
| **browser-use** | 浏览器自动化：截图/填表/数据抓取/Playwright操作 | awesome-agent-skills | - |
| **database-designer** | 数据库设计：ERD/Mermaid图 + MySQL DDL + Java Entity + 索引优化 + 零停机迁移 | superno/claude-skills-sup (GitHub) | - |
| **erd-document** | 完整系统设计文档：Word/PDF（11章节：ERD+DDL+接口+定时任务+安全+性能） | 自建 | - |
| **openspec-sdd** | 规范驱动开发：OpenSpec六阶段工作流+SDD+Gherkin验收场景+任务分解 | OpenSpec (Fission-AI) | - |
| **frontend-design** | 前端设计规范：拒绝AI slop，6大视觉方向（Brutalist/Editorial/Retro等） | Anthropic 官方 | 100K+ installs |
| **skill-creator** | Skill创造者：元技能，创建/测试/优化Skills，含Eval框架 | Anthropic 官方 | 官方内置 |
| **claude-mem** | 跨会话持久记忆：自动捕获/AI压缩/向量检索/渐进式披露 | thedotmack/claude-mem | 65K+ |
| **bmad-method** | AI驱动敏捷开发：一人顶一团队，多角色协作，文档分片+上下文工程 | bmad-code-org | - |
| **ai-dlc** | AI驱动开发生命周期：四阶段闭环+Hat-based角色+Backpressure质量门控 | TheBushidoCollective | - |
| **prompt-driven-dev** | 提示驱动开发：提示词版本化+确定性生成+Prompt as Code | 社区实践 | - |
| **prd-to-demo** | PRD转可交互原型：根据需求文档自动生成HTML原型Demo | 自建 | - |
| **screenshot-to-prototype** | 截图转可交互原型：设计稿/草图/竞品截图自动还原为HTML原型 | 自建 | - |
| **screenshot-to-prd** | 截图转PRD：UI截图自动生成结构化产品需求文档 | 自建 | - |
| **caveman-skill** | 🆕 洞穴人Token优化：削减75%输出token，压缩记忆文件46%，GitHub viral | juliusbrussee/caveman | viral |
| **supermemory** | 🆕 跨会话持久记忆：自动加载上下文，向量检索，LongMemEval基准领先 | SuperMemory | - |
| **multi-agent-orchestration** | 🆕 多Agent编排：并行执行，worktree隔离，AI团队协作框架 | oh-my-claudecode | 26K+ |
| **security-audit** | 🆕 安全审计：CodeQL/Semgrep集成，OWASP Top 10漏洞识别与修复 | trailofbits/skills | - |
| **testing-patterns** | 🆕 全栈测试模式：单元/React组件/E2E/Mock，测试金字塔分层实践 | Anthropic PR #723 | - |
| **document-typography** | 🆕 文档排版质量控制：孤行寡段/编号对齐/字体层级/间距规范 | Anthropic PR #514 | - |
| **claude-obsidian-reporter** | 🆕 Obsidian报告生成：Git提交自动转日/周/月报，YAML Frontmatter | Anthropic PR #664 | - |
| **hads** | 🆕 人-AI双读文档标准：Markdown语义标记，同时服务人类和AI解析 | Anthropic PR #616 | - |
| **skill-quality-analyzer** | 🆕 Skill质量评估元技能：结构/文档/安全/可维护性/触发精度五维评分 | Anthropic PR #83 | - |
| **codebase-inventory-audit** | 🆕 代码库清单审计：孤儿代码/重复逻辑/文档缺口/技术债务量化 | Anthropic Issue #147 | - |
| **agent-governance** | 🆕 AI Agent治理框架：策略执行/信任评分/审计追踪/威胁检测 | Anthropic Issue #412 | - |
| **dictionary-of-ai-coding** | 🆕 AI编码术语词典：Skill/Prompt/Agent/Vibe Coding大白话解释 | mattpocock | 1K+ |

### 💼 工作类（7个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **anti-pua** | 职场反PUA话术，怼回老板的精神控制 | "老板说"、"怎么怼"、"被PUA了" |
| **meeting-notes** | 把混乱会议记录整理成正式纪要 | "整理会议纪要"、"会议记录太乱" |
| **weekly-report** | 根据工作内容生成简洁专业周报 | "写周报"、"本周工作总结" |
| **leave-request** | 生成得体又易批准的请假话术 | "怎么请假"、"请假理由" |
| **elevator-pitch** | 30秒/1分钟电梯演讲生成 | "电梯演讲"、"一句话介绍" |
| **argue-winner** | 应对客户投诉/甩锅/PUA | "吵架"、"怎么回击"、"被甩锅" |
| **bs-translator** | 把大白话翻译成听不懂的版本 | "废话"、"听不懂人话"、"翻译成人话" |

### 🧠 人格测试类（1个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **personality-test** | MBTI/九型人格/DISC/大五/星座/血型全套人格测试 | "MBTI"、"人格测试"、"九型人格"、"星座性格" |

### 🎨 生活类（6个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **food-picker** | 纠结吃什么？帮你快速做决定 | "吃什么"、"点外卖选择" |
| **gift-advisor** | 根据关系/预算推荐贴心礼物 | "送什么礼物"、"生日礼物" |
| **outfit-weather** | 根据天气和场合给出穿搭建议 | "明天穿什么"、"穿搭建议" |
| **recipe-random** | 冰箱里有啥？帮你想菜谱 | "做什么菜"、"菜谱随机" |
| **travel-planner** | 国内游全能规划：行程/住宿/美食/预算/交通/打包清单 | "旅行计划"、"旅游攻略"、"出行规划"、"帮我规划行程" |
| **weather-pro** | 专业气象分析：农业/航空/航海/灾害预警/气候趋势 | "分析天气"、"气象数据"、"农业气象"、"飞行气象"、"台风分析" |

### 📚 学习类（4个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **wrong-answer** | 错题分析+类似题巩固 | "错题分析"、"帮我讲题" |
| **knowledge-card** | 把知识整理成记忆卡片 | "知识卡片"、"帮我背书" |
| **study-buddy** | 陪孩子背课文/听写/口算 | "陪孩子学习"、"听写" |
| **jargon-translator** | 专业术语翻译成大白话 | "术语翻译"、"听不懂" |
| **ai-trend-radar** | AI趋势雷达：追踪最热AI关键词、技术概念和行业动态 | "AI趋势"、"最近AI有什么新东西"、"AI热词" |

### 🎮 传统文化游戏类（2个）🆕

| Skill名称 | 功能 | 来源 | 触发关键词 |
|----------|------|------|-----------|
| **idiom-chain** | 经典成语接龙，考验成语储备 | 原创 | "成语接龙"、"接龙"、"玩接龙" |
| **feihua-ling** | 古诗词飞花令，诗词大会玩法 | 原创 | "飞花令"、"诗词接龙"、"对诗" |

### 💡 创意类（6个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **poetry-scenery** | 诗意风景描述，用诗词描述旅行照片 | "拍了xx照片"、"发朋友圈" |
| **moments-copywriter** | 生成朋友圈/小红书文案 | "朋友圈文案"、"发圈词" |
| **letter-future** | 写一封给未来自己的信 | "给未来写封信"、"时间胶囊" |
| **epitaph-generator** | 墓志铭/人生意义思考 | "墓志铭"、"人生感悟" |
| **horoscope** | 星座运势+趣味抽签 | "星座"、"抽签"、"运势" |
| **emoji-translator** | emoji解读+翻译 | "emoji翻译"、"这个表情什么意思" |

### 🧠 思考类（6个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **rural-story-writer** | 乡土叙事小说生成器，写祖孙故事 | "写乡土小说"、"奶奶的故事" |
| **relationship-patterns** | 亲密关系模式识别：辨别PUA/煤气灯效应/吹狗哨等不健康关系 | "关系模式"、"是不是PUA"、"煤气灯效应" |
| **choice-helper** | 纠结选A还是B？帮你分析 | "选择困难"、"帮我选" |
| **venting-hole** | 吐槽树洞，陪你发泄 | "吐槽"、"气死了"、"心情不好" |
| **sleep-story** | 睡前故事，陪你入睡 | "睡前故事"、"睡不着" |
| **year-summary** | 年度总结生成器 | "年终总结"、"年度复盘" |

### 🏠 居家类（5个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **photo-organizer** | 照片整理助手，按时间/人物/地点归类 | "整理照片"、"相册太乱" |
| **declutter-judge** | 断舍离裁判，判断扔还是留 | "断舍离"、"扔不扔" |
| **home-design** | 装修风格灵感 | "装修灵感"、"北欧风" |
| **plant-care** | 绿植养护指南 | "绿植养护"、"植物怎么养" |
| **home-storage** | 家居收纳指南 | "收纳"、"整理房间" |

### 🎨 设计类（3个）🆕

| Skill名称 | 功能 | 来源 | 触发关键词 |
|----------|------|------|-----------|
| **html-ppt-skill** | HTML PPT生成，36主题/31布局/47动画，无需PowerPoint | lewislulu/html-ppt-skill ⭐1.7K | "做PPT"、"生成演示文稿"、"做汇报材料"、"做幻灯片" |
| **diagram-design** | 编辑级图表设计，13种图表类型，纯HTML+SVG，拒绝Mermaid | cathrynlavery/diagram-design ⭐1.3K | "画架构图"、"画流程图"、"生成图表"、"做一张图" |
| **huashu-design** | 花叔HTML原生设计，20种设计哲学/5维评审/品牌识别 | alchaincyf/huashu-design ⭐2.8K | "做网页"、"设计界面"、"做落地页"、"做活动页" |

---

## 🌐 跨平台兼容性指南

本仓库的 Skills 基于 **Anthropic SKILL.md 标准** 构建，原生支持 Claude Code / Claude WorkBuddy。其他 AI 工具可通过以下方式使用：

| AI 工具 | 支持方式 | 使用方法 |
|---------|---------|---------|
| **Claude Code / WorkBuddy** | ✅ 原生支持 | 复制 Skill 文件夹到 `~/.claude/skills/` 或 `~/.workbuddy/skills/`，重启后自动识别 |
| **Trae** | ⚡ 适配使用 | 打开 **Settings → Builder → System Prompt**，将 SKILL.md 内容粘贴为系统提示词 |
| **Kimi** | ⚡ 适配使用 | 使用 **Kimi+ → 创建智能体**，将 SKILL.md 的 description 作为触发词，正文作为提示词模板 |
| **Cursor** | ⚡ 适配使用 | 将 SKILL.md 内容添加到 `.cursorrules` 文件，或在 Composer 中作为 `@` 提示词引用 |
| **VS Code + Cline** | ⚡ 适配使用 | 在 Cline 设置中配置 Custom System Prompt，粘贴 SKILL.md 内容 |
| **VS Code + Continue** | ⚡ 适配使用 | 在 `~/.continue/config.json` 的 `systemMessage` 中配置 Skill 内容 |
| **通用方法** | 📋 全平台适用 | 直接复制 SKILL.md 内容到对话开头作为上下文，AI 会按 Skill 定义的行为工作 |

### 💡 跨平台使用技巧

**技巧 1：直接粘贴法（所有平台通用）**
```
你现在是 [Skill名称]，请按照以下规范与我协作：

[Paste SKILL.md 全文内容]

现在请开始工作。
```

**技巧 2：Trae Builder 模式**
在 Trae 的 Builder 面板中，点击右上角设置图标 → 编辑 System Prompt，将 Skill 内容粘贴进去。Builder 会自动在每次生成代码前加载该提示词。

**技巧 3：Kimi 智能体**
访问 [kimi.moonshot.cn](https://kimi.moonshot.cn) → 左侧「Kimi+」→ 「创建智能体」→ 填入名称和触发词（复制 SKILL.md 的 description）→ 在「提示词」区域粘贴 SKILL.md 正文。

**技巧 4：Cursor Rules**
在项目根目录创建 `.cursorrules` 文件，将常用 Skill 的内容写入。Cursor 的 AI 聊天和 Composer 会自动读取该文件作为上下文。

---

## 📖 如何使用 Skills

### 方式一：直接对话触发（推荐）

在 WorkBuddy / Claude Code 中直接描述你的需求，例如：

```
# 触发 anti-pua
"老板说'你怎么连这点事都做不好'，怎么怼回去？"

# 触发 food-picker
"两个人吃，100块预算，想吃辣的"

# 触发 choice-helper
"该选A公司月薪2万还是B公司月薪1.5万？"

# 触发 systematic-debugging
"接口报500错误，帮我分析下"
```

WorkBuddy会自动识别并加载对应的Skill。

### 方式二：手动选择Skill

从左侧边栏的「专家」入口，进入「专家中心」，浏览分类后选择对应Skill开始对话。

---

## 🛠️ 如何创建新的 Skill

### Step 1：规划Skill

问自己几个问题：
- 这个Skill解决什么问题？
- 用户会怎么说触发这个Skill？
- 需要哪些参考资料或脚本？

### Step 2：创建目录结构

```
skills-ai/
└── your-skill-name/              # Skill文件夹（英文、中划线）
    ├── SKILL.md                  # ⭐ 必须：Skill配置
    └── references/               # 可选：参考资料
        └── xxx.md
```

### Step 3：编写 SKILL.md

SKILL.md 是Skill的核心，包含两部分：

```markdown
---
name: "Skill名称"
description: "这个Skill做什么的，什么时候触发它"
---

# 标题

你的详细说明...
```

### Step 4：安装Skill（按平台选择）

**Claude Code / WorkBuddy（原生支持）：**
```
# macOS / Linux
~/.claude/skills/
~/.workbuddy/skills/

# Windows
C:\Users\<你的用户名>\.claude\skills\
C:\Users\<你的用户名>\.workbuddy\skills\

# 或者在文件管理器中：
# 打开 %USERPROFILE%\.workbuddy\skills\
# 将你的skill文件夹粘贴进去
```

**Trae（适配使用）：**
打开 Trae → Settings → Builder → System Prompt → 将 SKILL.md 内容粘贴进去

**Kimi（适配使用）：**
访问 [kimi.moonshot.cn](https://kimi.moonshot.cn) → Kimi+ → 创建智能体 → 粘贴 SKILL.md 内容作为提示词

**Cursor（适配使用）：**
在项目根目录创建 `.cursorrules` 文件，将 SKILL.md 内容写入

### Step 5：重启 / 刷新

- **Claude Code / WorkBuddy**：重启客户端后自动加载
- **Trae**：切换 Builder 模式时自动生效
- **Kimi**：创建后立即可用
- **Cursor**：新建对话时自动读取 `.cursorrules`

---

## 📝 SKILL.md 编写规范

### 必需字段

| 字段 | 说明 | 示例 |
|-----|------|------|
| `name` | Skill名称（英文、中划线） | `"food-picker"` |
| `description` | 描述：做什么+何时触发+核心原则 | 见下方示例 |

### description 编写技巧

description 决定WorkBuddy何时触发你的Skill，要包含：
1. **功能描述**：这个Skill做什么
2. **触发场景**：什么情况下应该用它
3. **核心特点**：有什么独特价值

**好例子：**
```
"帮助用户快速做出外卖选择，告别选择困难症。适用于纠结吃什么、点外卖选择困难、不知道吃什么等场景。"
```

---

## 📌 Skill维护记录

| 日期 | 操作 | Skill名称 | 来源 |
|-----|------|----------|------|
| 2026-04-09 | 新建 | anti-pua（职场反PUA话术） | 原创 |
| 2026-04-09 | 新建 | poetry-scenery（诗意风景描述） | 原创 |
| 2026-04-09 | 新建 | photo-organizer（照片整理助手） | 原创 |
| 2026-04-09 | 新建 | rural-story-writer（乡土叙事小说生成器） | 原创 |
| 2026-04-09 | 新建 | food-picker（外卖选择困难症终结者） | 原创 |
| 2026-04-09 | 新建 | gift-advisor（礼物参谋） | 原创 |
| 2026-04-09 | 新建 | outfit-weather（穿搭天气助手） | 原创 |
| 2026-04-09 | 新建 | recipe-random（菜谱随机抽） | 原创 |
| 2026-04-09 | 新建 | meeting-notes（会议纪要整理助手） | awesome-agent-skills |
| 2026-04-09 | 新建 | weekly-report（周报生成器） | 原创 |
| 2026-04-09 | 新建 | leave-request（请假话术助手） | 原创 |
| 2026-04-09 | 新建 | elevator-pitch（电梯演讲生成器） | 原创 |
| 2026-04-09 | 新建 | argue-winner（吵架赢对面） | Top 20 Skills |
| 2026-04-09 | 新建 | wrong-answer（错题本分析助手） | 原创 |
| 2026-04-09 | 新建 | knowledge-card（知识卡片生成器） | 艾宾浩斯 |
| 2026-04-09 | 新建 | study-buddy（小学生陪练助手） | 番茄工作法 |
| 2026-04-09 | 新建 | jargon-translator（术语翻译器） | 原创 |
| 2026-04-09 | 新建 | moments-copywriter（朋友圈文案生成器） | 原创 |
| 2026-04-09 | 新建 | letter-future（给未来写封信） | 原创 |
| 2026-04-09 | 新建 | epitaph-generator（墓志铭生成器） | 原创 |
| 2026-04-09 | 新建 | horoscope（星座解签） | 原创 |
| 2026-04-09 | 新建 | emoji-translator（Emoji翻译器） | 原创 |
| 2026-04-09 | 新建 | choice-helper（两难选择器） | 原创 |
| 2026-04-09 | 新建 | venting-hole（吐槽树洞） | 原创 |
| 2026-04-09 | 新建 | sleep-story（睡前故事） | 原创 |
| 2026-04-09 | 新建 | year-summary（年终总结生成器） | 原创 |
| 2026-04-09 | 新建 | declutter-judge（断舍离裁判） | 原创 |
| 2026-04-09 | 新建 | home-design（装修灵感墙） | 原创 |
| 2026-04-09 | 新建 | plant-care（绿植养护指南） | 原创 |
| 2026-04-09 | 新建 | home-storage（家居收纳指南） | 原创 |
| 2026-04-09 | 🆕新增 | skill-lookup（Skills发现助手） | skills.sh (418K) |
| 2026-04-09 | 🆕新增 | systematic-debugging（系统调试） | obra/superpowers (142K) |
| 2026-04-09 | 🆕新增 | test-driven-development（TDD开发） | obra/superpowers (142K) |
| 2026-04-09 | 🆕新增 | confidence-check（置信度评估） | Top 20 Skills |
| 2026-04-09 | 🆕新增 | brainstorming（结构化头脑风暴） | obra/superpowers (142K) |
| 2026-04-09 | 🆕新增 | writing-plans（详细实施计划） | obra/superpowers (142K) |
| 2026-04-09 | 🆕新增 | idiom-chain（成语接龙） | 原创 |
| 2026-04-09 | 🆕新增 | feihua-ling（飞花令） | 原创 |
| 2026-04-09 | 🆕新增 | bs-translator（废话翻译官） | 原创 |
| 2026-04-09 | 🆕新增 | personality-test（人格测试大全） | 原创 |
| 2026-04-09 | 🆕新增 | memory-system（记忆系统） | 自建 |
| 2026-04-09 | 🆕新增 | memory-bank（项目记忆系统） | 自建 |
| 2026-04-09 | 🆕新增 | karpathy-skills（LLM编程避坑） | karpathy-skills |
| 2026-04-09 | 🆕新增 | hermes-experience（经验沉淀系统） | hermes-agent |
| 2026-04-18 | 🆕新增 | cron-expression（最强Cron表达式） | 自建 |
| 2026-04-20 | 🆕新增 | skill-accelerator（技能加速器·滑翔伞学习法） | 自建 |
| 2026-04-21 | 🆕新增 | ai-trend-radar（AI趋势雷达） | 自建 |
| 2026-04-21 | 🆕新增 | api-doc-generator（API文档生成器） | awesome-agent-skills |
| 2026-04-21 | 🆕新增 | git-commit（Git提交规范生成器） | awesome-agent-skills |
| 2026-04-21 | 🆕新增 | browser-use（浏览器自动化） | awesome-agent-skills |
| 2026-04-21 | 🆕新增 | database-designer（数据库设计器） | superno/claude-skills-sup |
| 2026-04-21 | 🆕新增 | erd-document（完整系统设计文档） | 自建 |
| 2026-04-21 | 🆕新增 | openspec-sdd（OpenSpec规范驱动开发） | Fission-AI/OpenSpec |
| 2026-04-22 | 🆕新增 | travel-planner（旅行规划师·国内游） | 自建 |
| 2026-04-29 | 🆕新增 | html-ppt-skill（HTML PPT生成器） | lewislulu/html-ppt-skill ⭐1.7K（本周热门） |
| 2026-04-29 | 🆕新增 | diagram-design（编辑级图表设计） | cathrynlavery/diagram-design ⭐1.3K（本周热门） |
| 2026-04-29 | 🆕新增 | huashu-design（花叔HTML设计） | alchaincyf/huashu-design ⭐2.8K（本周热门） |
| 2026-04-29 | 🔄更新 | karpathy-skills（Star数更新 14.6K→71.8K） | 本周Trending #1，单周+44K |
| 2026-04-29 | 🆕新增 | frontend-design（前端设计规范） | Anthropic 官方 100K+ installs |
| 2026-04-29 | 🆕新增 | skill-creator（Skill创造者·元技能） | Anthropic 官方内置 |
| 2026-04-29 | 🆕新增 | claude-mem（跨会话持久记忆） | thedotmack/claude-mem ⭐65K+（本周Trending #3） |
| 2026-04-29 | 🆕新增 | weather-pro（专业气象分析师） | 自建（农业/航空/航海/灾害预警） |
| 2026-04-29 | 🆕新增 | bmad-method（AI驱动敏捷开发） | bmad-code-org（多角色协作框架） |
| 2026-04-29 | 🆕新增 | ai-dlc（AI驱动开发生命周期） | TheBushidoCollective（四阶段+质量门控） |
| 2026-04-29 | 🆕新增 | prompt-driven-dev（提示驱动开发） | 社区实践（提示词版本化+确定性生成） |
| 2026-04-29 | 🆕新增 | prd-to-demo（PRD转可交互原型） | 自建（根据PRD生成HTML原型Demo） |
| 2026-04-29 | 🆕新增 | screenshot-to-prototype（截图转可交互原型） | 自建（设计稿/草图自动还原HTML原型） |
| 2026-04-27 | 🆕新增 | ai-trend-radar（AI趋势雷达·追踪热词） | 自建（AI关键词/技术概念/行业动态追踪） |
| 2026-04-27 | 🆕新增 | relationship-patterns（亲密关系模式识别） | 自建（辨别PUA/煤气灯效应/吹狗哨等） |
| 2026-04-27 | 🆕新增 | screenshot-to-prd（截图转PRD） | 自建（UI截图自动生成产品需求文档） |
| 2026-04-29 | 🆕新增 | skill-orchestrator（Skill编排器·统一入口） | 自建（81个Skill智能匹配+标准工作流推荐） |
| 2026-05-09 | 🆕新增 | caveman-skill（洞穴人Token优化·GitHub viral） | juliusbrussee/caveman（削减75%token） |
| 2026-05-09 | 🆕新增 | supermemory（跨会话持久记忆） | LongMemEval/LoCoMo基准领先 |
| 2026-05-09 | 🆕新增 | multi-agent-orchestration（多Agent编排框架） | oh-my-claudecode（26K+⭐） |
| 2026-05-09 | 🆕新增 | security-audit（安全审计工作流） | trailofbits/skills（CodeQL/Semgrep） |
| 2026-05-11 | 🆕新增 | testing-patterns（全栈测试模式·测试金字塔） | Anthropic PR #723 |
| 2026-05-11 | 🆕新增 | document-typography（文档排版质量控制） | Anthropic PR #514 |
| 2026-05-11 | 🆕新增 | claude-obsidian-reporter（Obsidian报告生成·Git→笔记） | Anthropic PR #664 |
| 2026-05-11 | 🆕新增 | hads（人-AI双读文档标准·HADS） | Anthropic PR #616 |
| 2026-05-11 | 🆕新增 | skill-quality-analyzer（Skill质量评估元技能·五维评分） | Anthropic PR #83 |
| 2026-05-11 | 🆕新增 | codebase-inventory-audit（代码库清单审计·技术债务） | Anthropic Issue #147 |
| 2026-05-11 | 🆕新增 | agent-governance（AI Agent治理框架·策略/信任/审计） | Anthropic Issue #412 |
| 2026-05-11 | 🆕新增 | dictionary-of-ai-coding（AI编码术语词典·大白话解释） | mattpocock（1K+⭐） |

---

## ❓ 常见问题

**Q: Skill放在哪里？**
A: 按平台选择：
- **Claude Code / WorkBuddy**: `~/.claude/skills/` 或 `~/.workbuddy/skills/`
- **Trae**: 通过 Settings → Builder → System Prompt 粘贴
- **Kimi**: 通过 Kimi+ → 创建智能体 粘贴
- **Cursor**: 项目根目录创建 `.cursorrules` 文件

**Q: Trae / Kimi / Cursor 能用这些 Skill 吗？**
A: 可以！本仓库所有 Skill 的知识内容是通用的。非 Claude 平台用户可将 SKILL.md 内容作为系统提示词（System Prompt）或上下文粘贴使用。详细方法见上方「跨平台兼容性指南」。

**Q: 一个目录可以放多个Skill吗？**
A: 不可以，每个Skill需要一个独立文件夹。

**Q: Skill不生效怎么办？**
A: 1) 确认SKILL.md格式正确 2) 重启客户端 3) 检查description是否包含触发关键词

**Q: 可以分享给其他人吗？**
A: 可以，把Skill文件夹压缩分享，对方按对应平台方法安装即可。

---

*持续更新中...有新想法？告诉我，我来帮你实现！* ✨
