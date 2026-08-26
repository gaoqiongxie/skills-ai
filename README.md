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
├── dictionary-of-ai-coding/ # 🆕 AI编码术语词典（Skill/Prompt/Agent/Vibe Coding大白话）
├── stop-slop/         # 🆕 去除AI味（识别并清除AI填充语/套话/slop模式，输出评分1-10）
├── opinionated-engineer/ # 🆕 工程化脚手架（强制TDD/类型安全/错误处理，禁止TODO，生产级标准）
├── beads-memory/      # 🆕 编码Agent记忆升级（跨会话持久化代码库上下文，AI压缩，6倍token节省）
├── webapp-testing/    # 🆕 Web应用自动化测试（Playwright侦察→行动，E2E/表单/截图对比/性能）
├── memory-hub/        # 🔥 统一记忆中枢（自动路由6层记忆，告别记忆Skill选择困难）
├── dev-flow/          # 🔥 智能开发工作流（自动感知6阶段，方法论自动编排）
├── quality-gate/      # 🔥 代码质量门控（提交前5维检查，不通过不放行）
├── create-pr/         # 🆕 自动生成规范PR（分析git diff，输出标题/摘要/测试计划/影响范围）
├── frontend-code-review/ # 🆕 前端代码结构化审查（React/TS/TSX，性能/可访问性/类型安全）
├── cardiac-arrest-guide/ # 🆕 心脏骤停科普与急救指南（起因/预后/CPR/AED/个人风险评估）
├── music-recommender/    # 🆕 音乐推荐与歌单生成（情绪/场景/天气/流派多维度匹配）
├── backend-change-flow/  # 🆕 后端需求驱动变更工作流（读代码→析需求→对齐→编码→Review→一致性确认）
├── ai-collaboration-safety/ # 🆕 AI协作安全指南（防幻觉/防逼疯/原子输出/熔断机制）
├── solo-parallel-dev/     # 🆕 单人多分支并行开发（worktree隔离/分支看板/冲突预防/上下文恢复）
├── qiaopi-style/          # 🆕 侨批体书信生成（闽南番客家书/半文半白/见字如面/侨批文化）
├── mental-health-check/   # 🆕 专业心理健康自评（PHQ-9/GAD-7/PSS-10/MBI职业倦怠）
├── dev-toolkit-integrator/ # 🆕 禅道·Jira·Wiki三工具集成（需求流转/Bug跟踪/迭代规划/发布版本）
├── web-artifacts-builder/  # 🆕 复杂Web构件构建器（React+Tailwind+shadcn/ui多组件/状态管理/路由）
├── remotion-video/         # 🆕 Remotion React视频生成器（Composition/Sequence/逐帧渲染/FFmpeg导出）
├── algorithmic-art/        # 🆕 算法艺术生成器（p5.js/Canvas/粒子系统/噪声纹理/种子可控复现）
├── cloudflare-worker/      # 🆕 Cloudflare Worker边缘函数（Wrangler/TypeScript/KV/R2/D1/全球边缘节点）
├── taste-skill/            # 🆕 反平庸UI设计（去AI味UI/参数化设计控制/8大设计方向/anti-slop）
├── cybersecurity-skills/   # 🆕 网络安全分析师技能库（754技能/26领域/MITRE ATT&CK/威胁狩猎/事件响应）
├── enterprise-crm-fullstack/ # 🆕 企业级CRM全栈开发规范（Vue 2+Element UI+Java/配置式列表/详情页/国际化/权限）
├── enterprise-iteration-agent/ # 🆕 企业级全栈迭代工作流Agent（7阶段闭环/状态机/路径感知/子Skill编排）
├── mcp-builder/              # 🆕 MCP构建指南（Model Context Protocol / Tool / Resource / Prompt）
├── vibe-coding/              # 🆕 Vibe Coding实战（自然语言驱动开发/护栏/重构固化）
└── repo-intelligence/        # 🆕 仓库智能（代码库问答/变更影响分析/架构意图还原）
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
| **Vibe Coding** | 自然语言驱动开发，45%AI生成代码有安全漏洞 | `vibe-coding` |
| **MCP** | Model Context Protocol，AI工具集成标准 | `mcp-builder` |
| **Repository Intelligence** | AI理解整个代码库、提交历史、架构意图 | `repo-intelligence` |
| **Skill供应链安全** | Snyk发现36%的skills存在恶意提示注入 | `security-audit` |

---

## 🔄 全栈开发周期环绕图

109个技能围绕 **需求 → 设计 → 开发 → 测试 → Review → 部署/记忆** 形成完整的全栈开发闭环。一个迭代通常从需求理解开始，经架构设计、编码开发、测试验证、质量审查，最终部署交付并将经验沉淀为记忆，反哺下一轮迭代。

```
                              ┌──────────┐
                         ┌────│  需求理解  │────┐
                         │    └──────────┘    │
                         │         │          │
                         ▼         ▼          ▼
                  ┌──────────┐  ┌──────────┐  ┌─────────────────┐
                  │ screenshot │  │ dev-toolkit │  │   openspec-sdd   │
                  │  -to-prd   │  │ -integrator │  │  + brainstorming │
                  └──────────┘  └──────────┘  └─────────────────┘
                         │         │          │
                         └────┬────┴────┬─────┘
                              ▼         ▼
                         ┌──────────┐
                         │  架构设计  │
                         └──────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
       ┌──────────┐    ┌──────────┐    ┌──────────┐
       │ database │    │    api   │    │ frontend │
       │ -designer│    │  -doc    │    │ -design  │
       │+erd-doc  │    │-generator│    │+huashu   │
       └──────────┘    └──────────┘    │+taste    │
                                        └──────────┘
                                              │
                              ┌───────────────┴───────────────┐
                              ▼                               ▼
                         ┌──────────┐                  ┌──────────┐
                         │  编码开发  │◀────────────────▶│  测试验证  │
                         └──────────┘                  └──────────┘
                              │                               ▲
        ┌─────────────────────┼─────────────────────┐          │
        ▼                     ▼                     ▼          │
 ┌──────────────┐   ┌──────────────┐   ┌──────────────┐        │
 │ enterprise   │   │   backend    │   │  frontend    │        │
 │ -crm-        │   │  -change-    │   │ -code-review │        │
 │ fullstack    │   │    flow      │   │+opinionated  │        │
 │+web-artifacts│   │+karpathy     │   │ -engineer    │        │
 │ -builder     │   │ -skills      │   │+stop-slop    │        │
 └──────────────┘   └──────────────┘   └──────────────┘        │
        │                     │                     │           │
        └─────────────────────┼─────────────────────┘           │
                              ▼                                 │
                         ┌──────────┐                           │
                         │  质量审查  │───────────────────────────┘
                         └──────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
       ┌──────────┐    ┌──────────┐    ┌──────────┐
       │ quality  │    │  create  │    │ confidence│
       │  -gate   │    │   -pr    │    │  -check   │
       └──────────┘    └──────────┘    └──────────┘
                              │
                              ▼
                         ┌──────────┐
                         │  部署交付  │
                         └──────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
       ┌──────────┐    ┌──────────┐    ┌──────────┐
       │ git-     │    │  solo-   │    │  multi-  │
       │ commit   │    │ parallel │    │ agent    │
       │          │    │   -dev   │    │ -orches  │
       └──────────┘    └──────────┘    └──────────┘
                              │
                              ▼
                         ┌──────────┐
                         │  记忆沉淀  │────┐
                         └──────────┘    │
                              │          │
              ┌───────────────┼──────────┘
              ▼               ▼
       ┌──────────┐    ┌──────────┐
       │ memory   │    │  beads   │
       │  -hub    │    │ -memory  │
       │+hermes   │    │+claude   │
       │ -exp     │    │ -mem     │
       └──────────┘    └──────────┘
                              │
                              └──────────────────────┐
                                                     ▼
                                              ┌──────────┐
                                              │  反哺下一轮 │
                                              │   迭代    │
                                              └──────────┘
```

### 各阶段技能速查

| 阶段 | 核心技能 | 作用说明 |
|------|---------|---------|
| **需求理解** | `screenshot-to-prd` · `prd-to-demo` · `openspec-sdd` · `brainstorming` · `dev-toolkit-integrator` | UI/PRD互转 → 原型验证 → 规范驱动 → 头脑风暴 → 需求流转（禅道/Jira/Wiki） |
| **架构设计** | `database-designer` · `erd-document` · `api-doc-generator` · `diagram-design` · `frontend-design` · `huashu-design` · `taste-skill` | 数据库设计 → 系统文档 → API契约 → 图表表达 → UI设计 → 去AI味设计 |
| **编码开发** | `enterprise-crm-fullstack` · `backend-change-flow` · `web-artifacts-builder` · `cloudflare-worker` · `karpathy-skills` · `opinionated-engineer` · `stop-slop` | 前后端规范编码 → 变更流程 → 复杂构件 → 边缘函数 → 编程避坑 → 工程化 → 去AI味 |
| **测试验证** | `testing-patterns` · `webapp-testing` · `security-audit` · `test-driven-development` | 单元/集成/E2E分层测试 → Web自动化 → 安全审计 → TDD红绿重构 |
| **质量审查** | `quality-gate` · `create-pr` · `frontend-code-review` · `confidence-check` | 提交前五维检查 → 自动PR生成 → 前端结构化Review → AI置信度自评 |
| **部署交付** | `git-commit` · `solo-parallel-dev` · `multi-agent-orchestration` · `ai-collaboration-safety` | 规范提交 → 多分支并行 → 多Agent编排 → 安全协作防幻觉 |
| **记忆沉淀** | `memory-hub` · `hermes-experience` · `beads-memory` · `claude-mem` · `supermemory` | 统一记忆路由 → 经验模式提取 → 代码库上下文持久化 → 跨会话记忆 |

> 💡 **实战建议**：一个标准迭代的典型路径为：
> `openspec-sdd`（规范对齐） → `database-designer` + `api-doc-generator`（设计） → `enterprise-crm-fullstack` + `backend-change-flow`（开发） → `testing-patterns` + `security-audit`（测试） → `quality-gate` + `create-pr`（Review） → `git-commit` + `solo-parallel-dev`（部署） → `memory-hub` + `hermes-experience`（沉淀）。
>
> 🎯 **进阶用法**：激活 `enterprise-iteration-agent`，说一句"开始开发【xxx】需求"，Agent 会自动按上述路径推进，维护迭代状态机，并在每个阶段调用对应 Skill 完成工作。

---

## 🚀 已安装的 Skills（109个）

### 🔧 开发方法论类（56个）

| Skill名称 | 功能 | 来源 | Stars |
|----------|------|------|-------|
| **skill-orchestrator** | ⭐ Skill编排器：90个Skill的统一智能入口，场景匹配+工作流推荐 | 自建 | - |
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
| **opinionated-engineer** | 🆕 工程化脚手架：强制TDD/类型安全/错误处理/日志规范，禁止TODO | mattpocock/skills | 75K |
| **beads-memory** | 🆕 编码Agent记忆升级：跨会话持久化代码库上下文，AI压缩，6倍token节省 | gastownhall/beads | 22.1K |
| **webapp-testing** | 🆕 Web应用自动化测试：Playwright侦察→行动，E2E/表单/截图对比/性能 | 社区实践 | - |
| **memory-hub** | 🔥 统一记忆中枢：自动路由四层记忆（个人/项目/知识/经验），告别选择困难 | 蒸馏（6合1） | - |
| **dev-flow** | 🔥 智能开发工作流：自动感知六阶段，方法论自动编排（OpenSpec→BMAD→PDD→OE→AI-DLC） | 蒸馏（5合1） | - |
| **quality-gate** | 🔥 代码质量门控：提交前五维检查（测试/安全/规范/逻辑/性能），不通过不放行 | 蒸馏（6合1） | - |
| **create-pr** | 🆕 自动生成规范PR：分析git diff，输出标题/摘要/测试计划/影响范围/标签 | 社区热门（169.7K） | - |
| **frontend-code-review** | 🆕 前端代码结构化审查：React/TS/TSX性能/可维护性/可访问性/类型安全检查 | 社区热门 | - |
| **backend-change-flow** | 🆕 后端需求驱动变更工作流：读代码→析需求→影响分析→三对齐→编码→循环Review→一致性确认 | 自建 | - |
| **ai-collaboration-safety** | 🆕 AI协作安全指南：防幻觉/防逼疯/原子输出/熔断机制/四层防御体系 | 自建 | - |
| **solo-parallel-dev** | 🆕 单人多分支并行开发：worktree物理隔离/分支状态看板/冲突预防/上下文恢复协议 | 自建 | - |
| **dev-toolkit-integrator** | 🆕 禅道·Jira·Wiki三工具集成：需求流转/Bug跟踪/迭代规划/发布版本/跨工具同步 | 自建 | - |
| **cloudflare-worker** | 🆕 Cloudflare Worker边缘函数：Wrangler CLI/TypeScript/KV/R2/D1/全球300+边缘节点 | Anthropic官方+社区 | 114K |
| **cybersecurity-skills** | 🆕 网络安全分析师技能库：754技能/26领域/MITRE ATT&CK映射/威胁狩猎/事件响应/渗透测试 | mukul975 | 14K |
| **enterprise-crm-fullstack** | 🆕 企业级CRM全栈开发规范：Vue 2+Element UI+Java/配置式列表页/详情页/国际化/权限控制 | 自建 | - |
| **enterprise-iteration-agent** | 🆕 企业级全栈迭代工作流Agent：需求→设计→开发→测试→Review→部署→记忆7阶段闭环，状态机驱动，子Skill编排 | 自建 | - |
| **mcp-builder** | 🆕 MCP构建指南：Model Context Protocol / Tool / Resource / Prompt 封装，stdio/SSE/HTTP 传输 | Anthropic官方+社区 | 114K |
| **vibe-coding** | 🆕 Vibe Coding实战：自然语言驱动开发/护栏/重构固化，与 quality-gate / stop-slop 联动 | 社区热门 | - |
| **repo-intelligence** | 🆕 仓库智能：代码库问答/变更影响分析/架构意图还原/RAG over Codebase | 自建 | - |

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

### 🎨 生活类（7个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **food-picker** | 纠结吃什么？帮你快速做决定 | "吃什么"、"点外卖选择" |
| **gift-advisor** | 根据关系/预算推荐贴心礼物 | "送什么礼物"、"生日礼物" |
| **outfit-weather** | 根据天气和场合给出穿搭建议 | "明天穿什么"、"穿搭建议" |
| **recipe-random** | 冰箱里有啥？帮你想菜谱 | "做什么菜"、"菜谱随机" |
| **travel-planner** | 国内游全能规划：行程/住宿/美食/预算/交通/打包清单 | "旅行计划"、"旅游攻略"、"出行规划"、"帮我规划行程" |
| **weather-pro** | 专业气象分析：农业/航空/航海/灾害预警/气候趋势 | "分析天气"、"气象数据"、"农业气象"、"飞行气象"、"台风分析" |
| **music-recommender** | 🆕 音乐推荐与歌单生成：按情绪/场景/天气/流派推荐，支持跨平台歌单编排 | "推荐首歌"、"适合跑步的音乐"、"下雨天听什么"、"咖啡时光BGM"、"睡前音乐"、"派对歌单" |

### 📚 学习类（5个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **wrong-answer** | 错题分析+类似题巩固 | "错题分析"、"帮我讲题" |
| **knowledge-card** | 把知识整理成记忆卡片 | "知识卡片"、"帮我背书" |
| **study-buddy** | 陪孩子背课文/听写/口算 | "陪孩子学习"、"听写" |
| **jargon-translator** | 专业术语翻译成大白话 | "术语翻译"、"听不懂" |
| **ai-trend-radar** | AI趋势雷达：追踪最热AI关键词、技术概念和行业动态 | "AI趋势"、"最近AI有什么新东西"、"AI热词" |

### 🏥 健康科普类（2个）🆕

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **cardiac-arrest-guide** | 心脏骤停科普与急救指南：起因/预后/CPR/AED/个人风险评估 | "心脏骤停"、"心肺复苏"、"猝死风险"、"AED怎么用"、"心脏骤停原因" |
| **mental-health-check** | 🆕 专业心理健康自评：PHQ-9抑郁/GAD-7焦虑/PSS-10压力/MBI职业倦怠 | "我觉得抑郁了"、"焦虑测试"、"压力好大"、"心理测试"、"最近情绪很低落"、"burnout" |

### 🎮 传统文化游戏类（2个）🆕

| Skill名称 | 功能 | 来源 | 触发关键词 |
|----------|------|------|-----------|
| **idiom-chain** | 经典成语接龙，考验成语储备 | 原创 | "成语接龙"、"接龙"、"玩接龙" |
| **feihua-ling** | 古诗词飞花令，诗词大会玩法 | 原创 | "飞花令"、"诗词接龙"、"对诗" |

### 💡 创意类（10个）

| Skill名称 | 功能 | 触发关键词 |
|----------|------|-----------|
| **poetry-scenery** | 诗意风景描述，用诗词描述旅行照片 | "拍了xx照片"、"发朋友圈" |
| **moments-copywriter** | 生成朋友圈/小红书文案 | "朋友圈文案"、"发圈词" |
| **letter-future** | 写一封给未来自己的信 | "给未来写封信"、"时间胶囊" |
| **epitaph-generator** | 墓志铭/人生意义思考 | "墓志铭"、"人生感悟" |
| **horoscope** | 星座运势+趣味抽签 | "星座"、"抽签"、"运势" |
| **emoji-translator** | emoji解读+翻译 | "emoji翻译"、"这个表情什么意思" |
| **stop-slop** | 去除AI味：识别并清除AI填充语/套话/slop模式，输出评分1-10 | "去掉AI味"、"太像AI写的了"、"去slop"、"像人写的" |
| **qiaopi-style** | 🆕 侨批体书信生成：闽南番客家书风格，半文半白，见字如面 | "转成侨批体"、"番客写信"、"给阿嬷写封信"、"唐山来批"、"侨批" |
| **remotion-video** | 🆕 Remotion React视频生成器：组件化视频/逐帧渲染/时间轴控制/FFmpeg导出 | "生成视频"、"做动画视频"、"React视频"、"数据动画"、"字幕视频" |
| **algorithmic-art** | 🆕 算法艺术生成器：p5.js/Canvas/粒子系统/噪声纹理/种子可控复现 | "生成艺术"、"算法壁纸"、"p5.js艺术"、"代码画画"、"粒子效果"、"噪声纹理" |

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

### 🎨 设计类（5个）🆕

| Skill名称 | 功能 | 来源 | 触发关键词 |
|----------|------|------|-----------|
| **html-ppt-skill** | HTML PPT生成，36主题/31布局/47动画，无需PowerPoint | lewislulu/html-ppt-skill ⭐1.7K | "做PPT"、"生成演示文稿"、"做汇报材料"、"做幻灯片" |
| **diagram-design** | 编辑级图表设计，13种图表类型，纯HTML+SVG，拒绝Mermaid | cathrynlavery/diagram-design ⭐1.3K | "画架构图"、"画流程图"、"生成图表"、"做一张图" |
| **huashu-design** | 花叔HTML原生设计，20种设计哲学/5维评审/品牌识别 | alchaincyf/huashu-design ⭐2.8K | "做网页"、"设计界面"、"做落地页"、"做活动页" |
| **web-artifacts-builder** | 🆕 复杂Web构件构建器：React+Tailwind+shadcn/ui多组件/状态管理/路由切换 | Anthropic官方 ⭐114K | "做个复杂网页"、"数据看板"、"交互式配置页面"、"React组件页面"、"shadcn界面" |
| **taste-skill** | 🆕 反平庸UI设计：去AI味UI/参数化设计控制/8大设计方向/anti-slop反重复 | Leonxlnx ⭐32.7K | "反平庸设计"、"去AI味UI"、"提升界面品质"、"UI太模板化"、"让页面更有设计感" |

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
| 2026-05-14 | 🆕新增 | stop-slop（去除AI味·识别并清除AI slop模式） | 社区热门（Anthropic Marketplace viral） |
| 2026-05-14 | 🆕新增 | opinionated-engineer（工程化脚手架·强制TDD/生产级标准） | mattpocock/skills ⭐75K（Trending #1） |
| 2026-05-14 | 🆕新增 | beads-memory（编码Agent记忆升级·跨会话代码库上下文） | gastownhall/beads ⭐22.1K |
| 2026-05-14 | 🆕新增 | webapp-testing（Web应用自动化测试·Playwright侦察→行动） | 社区实践 |
| 2026-05-15 | 🔥蒸馏 | memory-hub（统一记忆中枢·自动路由四层记忆，6合1） | 蒸馏：claude-mem+supermemory+beads-memory+memory-bank+memory-system+hermes-experience |
| 2026-05-15 | 🔥蒸馏 | dev-flow（智能开发工作流·自动感知六阶段，5合1） | 蒸馏：bmad-method+ai-dlc+opinionated-engineer+prompt-driven-dev+openspec-sdd |
| 2026-05-15 | 🔥蒸馏 | quality-gate（代码质量门控·提交前五维检查，6合1） | 蒸馏：testing-patterns+webapp-testing+TDD+security-audit+confidence-check+opinionated-engineer |
| 2026-05-20 | 🆕新增 | create-pr（自动生成规范PR·分析git diff，169.7K流行度） | 社区热门（Anthropic Marketplace 2026最流行） |
| 2026-05-20 | 🆕新增 | frontend-code-review（前端代码结构化审查·React/TS/TSX） | 社区热门（Effeilo/claude-code-frontend-skills） |
| 2026-05-20 | 🆕新增 | cardiac-arrest-guide（心脏骤停科普与急救指南·起因/预后/CPR/AED） | 自建（整合AHA/ERC指南、中国心肺复苏指南） |
| 2026-05-22 | 🆕新增 | music-recommender（音乐推荐与歌单生成·情绪/场景/天气/流派多维度匹配） | 自建 |
| 2026-05-25 | 🆕新增 | backend-change-flow（后端需求驱动变更工作流·七阶段闭环/三一致校验） | 自建（蒸馏 dev-flow + systematic-debugging + quality-gate 后端变更场景） |
| 2026-05-25 | 🆕新增 | ai-collaboration-safety（AI协作安全指南·防幻觉/防逼疯/原子输出/熔断机制） | 自建（基于人机交互心理学 + 开发者真实崩溃案例） |
| 2026-05-25 | 🆕新增 | solo-parallel-dev（单人多分支并行开发·worktree隔离/分支看板/冲突预防） | 自建（基于 skills-ai 94个skill实战经验） |
| 2026-05-27 | 🆕新增 | qiaopi-style（侨批体书信生成·闽南番客家书/半文半白/见字如面/侨批文化） | 自建（参考闽南/潮汕侨批文化、电影《给阿嬷的情书》风格） |
| 2026-05-28 | 🆕新增 | mental-health-check（专业心理健康自评·PHQ-9/GAD-7/PSS-10/MBI职业倦怠） | 自建（整合PHQ-9/GAD-7/PSS-10/MBI-GS标准化临床量表） |
| 2026-05-28 | 🆕新增 | dev-toolkit-integrator（禅道·Jira·Wiki三工具集成·需求流转/Bug跟踪/迭代规划/发布版本） | 自建（基于国内开发团队禅道+Jira+Wiki真实工作流） |
| 2026-05-29 | 🆕新增 | web-artifacts-builder（复杂Web构件构建器·React+Tailwind+shadcn/ui） | Anthropic官方 ⭐114K |
| 2026-05-29 | 🆕新增 | remotion-video（Remotion React视频生成器·组件化视频/逐帧渲染/FFmpeg导出） | Remotion官方 |
| 2026-05-29 | 🆕新增 | algorithmic-art（算法艺术生成器·p5.js/Canvas/粒子系统/噪声纹理/种子可控） | Anthropic官方 ⭐114K |
| 2026-05-29 | 🆕新增 | cloudflare-worker（Cloudflare Worker边缘函数·Wrangler/TypeScript/KV/R2/D1） | Cloudflare官方+社区最佳实践 |
| 2026-06-04 | 🆕新增 | taste-skill（反平庸UI设计·去AI味UI/参数化设计控制/8大设计方向/anti-slop） | Leonxlnx ⭐32.7K（GitHub Trending 热门） |
| 2026-06-04 | 🆕新增 | cybersecurity-skills（网络安全分析师技能库·754技能/26领域/MITRE ATT&CK/威胁狩猎/事件响应） | mukul975 ⭐14K（GitHub Trending 热门） |
| 2026-06-04 | 🆕新增 | enterprise-crm-fullstack（企业级CRM全栈开发规范·Vue 2+Element UI+Java/配置式列表/详情页/国际化/权限） | 自建（基于企业级CRM项目实战经验） |
| 2026-06-04 | 🆕新增 | enterprise-iteration-agent（企业级全栈迭代工作流Agent·7阶段闭环/状态机/路径感知/子Skill编排） | 自建（串联105个Skill形成开发闭环） |
| 2026-08-26 | 🆕新增 | mcp-builder（MCP构建指南·Model Context Protocol / Tool / Resource / Prompt） | Anthropic官方+社区最佳实践（2026热门趋势） |
| 2026-08-26 | 🆕新增 | vibe-coding（Vibe Coding实战·自然语言驱动开发/护栏/重构固化） | 社区热门（2026 AI编程热词） |
| 2026-08-26 | 🆕新增 | repo-intelligence（仓库智能·代码库问答/变更影响分析/架构意图还原） | 自建（Repository Intelligence/RAG over Codebase） |

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
