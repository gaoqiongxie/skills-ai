---
name: "enterprise-iteration-agent"
description: "企业级全栈迭代工作流Agent：当用户说'开始开发这个需求'、'处理本次迭代'、'全栈开发闭环'、'跑一个迭代'、'enterprise iteration'、'迭代开发'、'需求交付'、'开发闭环'时触发。自动按需求→设计→开发→测试→Review→部署→记忆7阶段推进，维护迭代状态机，路径感知（自动读取需求目录与代码目录），协调多个子Skill协作完成企业级CRM全栈需求交付。支持状态回退、并行分支、上下文继承。"
---

# Enterprise Iteration Agent — 企业级全栈迭代工作流

> **理念**: 一个迭代就是一个闭环。从需求理解到记忆沉淀，Agent 维护完整的状态机，确保每个阶段都有产出、每个决策都有记录、每段经验都能复用。

---

## 核心能力

1. **状态机驱动**: 7阶段自动推进，支持前进/回退/跳过
2. **路径感知**: 自动读取需求目录与代码目录，减少人工指定路径
3. **子Skill编排**: 按需调用现有111个Skill中的相关能力
4. **上下文继承**: 前一阶段的产出自动注入下一阶段
5. **并行加速**: DEV阶段可拆分为前后端并行工作流

---

## 迭代状态机

```
INIT → REQ → DES → DEV → TST → REV → DEP → MEM → END
 │      │     │     │     │     │     │     │
 └──────┴─────┴─────┴─────┴─────┴─────┴─────┘
              ↑ 支持任意回退
```

| 状态 | 阶段 | 核心产出物 | 主要调用Skill |
|------|------|-----------|-------------|
| `INIT` | 启动 | 迭代看板初始化 | 自身 |
| `REQ` | 需求理解 | PRD摘要/验收场景/原型 | `openspec-sdd`, `prd-to-demo`, `brainstorming`, `dev-toolkit-integrator` |
| `DES` | 架构设计 | ERD/API文档/接口契约 | `database-designer`, `erd-document`, `api-doc-generator`, `diagram-design`, `frontend-design` |
| `DEV` | 编码开发 | 前后端代码/脚本 | `enterprise-crm-fullstack`, `backend-change-flow`, `web-artifacts-builder`, `karpathy-skills`, `opinionated-engineer`, `stop-slop` |
| `TST` | 测试验证 | 测试用例/安全报告 | `testing-patterns`, `webapp-testing`, `security-audit`, `test-driven-development` |
| `REV` | 质量审查 | PR描述/Review记录 | `quality-gate`, `create-pr`, `frontend-code-review`, `confidence-check` |
| `DEP` | 部署交付 | 提交记录/合并日志 | `git-commit`, `solo-parallel-dev`, `multi-agent-orchestration` |
| `MEM` | 记忆沉淀 | ADR/经验卡片/模式库 | `memory-hub`, `hermes-experience`, `beads-memory`, `claude-mem` |
| `END` | 完成 | 迭代总结报告 | 自身 |

---

## 路径感知配置（用户可自定义）

Agent 启动时会尝试读取以下路径（用户首次使用时确认或修正）：

| 类型 | 默认路径示例 | 说明 |
|------|-------------|------|
| 需求目录 | `D:\需求\客户\` | 存放 PRD/需求文档的根目录 |
| 前端代码 | `D:\项目\crm-pc\src\views\` | Vue 2 前端项目 |
| 后端代码 | `D:\项目\mmp\mmp-service\` | Java Spring Boot 后端 |
| 数据库文档 | `D:\项目\docs\database\` | 表结构/ERD 存放地 |
| API文档 | `D:\项目\docs\api\` | Swagger/OpenAPI 存放地 |

> 路径仅作示例，首次触发时 Agent 会询问用户确认实际路径。

---

## 各阶段详细工作流

### 阶段一：INIT → 启动

**触发语**: "开始开发【xxx】需求" / "跑一个迭代" / "处理本次迭代"

**动作**:
1. 询问用户迭代名称与需求文件路径
2. 初始化迭代看板（Markdown 表格）
3. 读取需求文档，提取：
   - 需求背景与目标
   - 涉及的业务模块
   - 验收标准（如有Gherkin则直接提取）
   - 预计改动范围（前端页面/后端接口/数据库表）
4. 输出**迭代计划书**：
   - 阶段拆分建议
   - 风险评估（如涉及公共组件改造、接口兼容性）
   - 并行机会识别（前后端是否可解耦）

**状态转换**:
- 用户确认 → 推进到 `REQ`
- 用户要求补充信息 → 停留在 `INIT`

---

### 阶段二：REQ → 需求理解

**核心目标**: 把模糊的需求变成结构化的开发输入

**动作**:
1. 调用 `openspec-sdd` 能力：
   - 输出 OpenSpec 规范文档（6阶段）
   - 提取 Gherkin 验收场景
   - 生成开发任务分解表
2. 如需原型验证 → 调用 `prd-to-demo` 生成可交互 HTML 原型
3. 如需需求流转 → 调用 `dev-toolkit-integrator` 检查禅道/Jira 状态
4. 输出**需求确认清单**：
   - 功能列表（必须/应该/可以）
   - 边界条件与异常场景
   - 数据权限与按钮权限要求
   - 涉及的现有模块与接口

**回退条件**: 需求不清晰（无验收标准、无原型、无字段定义）→ 退回 `INIT` 要求补充

---

### 阶段三：DES → 架构设计

**核心目标**: 产出可执行的工程方案

**动作**:
1. **数据库设计**（如需新建/改表）:
   - 调用 `database-designer`：ERD + MySQL DDL + Java Entity
   - 调用 `erd-document`：完整数据库设计文档（11章节）
   - 确保包含标准字段：`remark`, `create_time`, `edit_time`, `delete_flag`
2. **API设计**:
   - 调用 `api-doc-generator`：Swagger/OpenAPI 注解 + 字段说明
   - 明确接口前缀：`/api/`（前端）、`/feign/`（内部）、`/open-api/`（第三方）
3. **UI设计**（如需新页面）:
   - 调用 `frontend-design` 或 `huashu-design` 确定视觉方向
   - 调用 `taste-skill` 去除AI味，提升设计品质
   - 调用 `diagram-design` 输出页面信息架构图
4. 输出**设计决策记录（ADR）**:
   - 技术选型理由
   - 表结构设计依据
   - 接口边界划分
   - 潜在风险与回滚方案

**状态转换**:
- 设计通过 → `DEV`
- 设计有争议 → 停留在 `DES`，调用 `brainstorming` 辅助决策
- 发现需求遗漏 → 回退 `REQ`

---

### 阶段四：DEV → 编码开发

**核心目标**: 高质量代码产出，支持前后端并行

**动作**:
1. **环境确认**:
   - 确认当前分支（基于 `solo-parallel-dev` 检查分支状态）
   - 确认 worktree 隔离（如使用 `multi-agent-orchestration`）
2. **前端开发**（调用 `enterprise-crm-fullstack`）:
   - 配置式列表页：`SearchListPage` / `ele-list-page`
   - 详情页：表单 + 内联编辑表格 + 附件上传
   - 国际化：`$i18n()` 替换
   - 权限：`v-btn-permission` 指令
   - 路由：hash 模式，按模块懒加载
3. **后端开发**（调用 `backend-change-flow`）:
   - 七阶段变更流：读代码 → 析需求 → 影响分析 → 三对齐 → 编码 → 循环Review → 一致性确认
   - Controller / Service / Mapper / Entity 四层架构
   - 符合 Java 开发规范（K&R括号、4空格、120字符、Javadoc）
4. **代码质量**:
   - 调用 `stop-slop` 去除代码中的AI生成痕迹
   - 调用 `karpathy-skills` 规避LLM编程常见陷阱
   - 调用 `opinionated-engineer` 确保工程化标准（类型安全、错误处理、无TODO）
5. **验证先于完成**（借鉴 superpowers verification-before-completion）:
   - 宣称任何文件/接口/切片"完成"前，必须实际运行编译、lint 或测试命令并记录真实输出
   - 修复类任务必须先复现原始缺陷场景，再验证修复后场景，两轮证据都写入上下文
   - 禁止用"应该没问题""已自测"作为完成依据，无证据的完成声明不得计入产出清单
6. 输出**开发产出清单**:
   - 新增/修改的文件列表
   - 接口变更清单
   - 数据库变更脚本

**并行模式**（大需求时推荐）:
```
Orchestrator (你)
   ├── Agent-A: 前端开发 (worktree-A)
   └── Agent-B: 后端开发 (worktree-B)
        └── 每30分钟同步接口契约
```

---

### 阶段五：TST → 测试验证

**核心目标**: 不带着明显缺陷进入Review

**动作**:
1. **单元测试**（调用 `testing-patterns`）:
   - Service层核心业务逻辑测试
   - 工具类/纯函数测试
   - 边界条件与异常分支覆盖
2. **集成/E2E测试**（调用 `webapp-testing`）:
   - Playwright 侦察→行动：表单提交、列表查询、详情查看
   - 截图对比（UI回归）
3. **安全审计**（调用 `security-audit`）:
   - SQL注入检查（参数化查询验证）
   - XSS检查（输入输出编码）
   - 越权访问检查（按钮权限、数据权限）
4. **TDD回检**（调用 `test-driven-development`）:
   - 红-绿-重构循环是否完成
   - 测试覆盖率是否达标（建议核心模块≥70%）
5. 输出**测试报告**:
   - 通过/失败用例统计
   - 发现的缺陷与修复建议
   - 安全扫描结果

**阻断条件**: 安全高危漏洞未修复 → 禁止推进到 `REV`

---

### 阶段六：REV → 质量审查

**核心目标**: 让Review成为质量提升而非形式主义

**动作**:
1. **提交前检查**（调用 `quality-gate`）:
   - 五维检查：测试通过 / 安全无高危 / 规范符合 / 逻辑正确 / 性能可接受
   - 不通过则退回 `DEV`
2. **PR生成**（调用 `create-pr`）:
   - 分析 git diff，自动输出：
     - PR标题（Conventional Commits格式）
     - 摘要（What + Why）
     - 测试计划
     - 影响范围与回滚方案
     - 标签（feature/fix/refactor）
3. **两阶段代码审查**（借鉴 superpowers two-phase review，两个阶段独立出具结论）:
   - **阶段一：规格符合性** — 对照 DES 阶段产出的 ERD / 接口契约 / ADR / 验收场景逐项核对实现；字段、动作、状态机、错误码、权限点是否兑现规范；验收场景（AC）逐条回放。critical 问题退回 `DEV`，不得用"代码质量好"为由绕过规格偏离
   - **阶段二：代码质量**（调用 `frontend-code-review`）:
     - React/Vue组件检查（如适用）
     - 性能检查（不必要的渲染、大数据量处理）
     - 可维护性检查（圈复杂度、重复代码）
4. **置信度自检**（调用 `confidence-check`）:
   - Agent 自我评估本次迭代的置信度（1-10）
   - 低置信度时标记风险点，建议人工复核
5. 输出**审查报告**:
   - PR链接/编号
   - 两阶段审查结论（规格符合性 / 代码质量，分别列出）
   - 发现的代码异味与建议
   - Agent置信度评分

---

### 阶段七：DEP → 部署交付

**核心目标**: 平稳合并，不影响主干

**动作**:
1. **提交规范**（调用 `git-commit`）:
   - 检查提交信息是否符合 Conventional Commits
   - 多提交整理（rebase/squash建议）
2. **冲突预防**（调用 `solo-parallel-dev`）:
   - 检查目标分支是否有新提交
   - 评估合并冲突风险
   - 提供冲突预演方案
3. **多Agent部署**（调用 `multi-agent-orchestration`）:
   - 如需多服务同时发布，编排发布顺序
   - 数据库脚本先行 → 后端服务 → 前端页面
4. 输出**部署记录**:
   - 合并提交哈希
   - 发布版本号
   - 回滚指令

---

### 阶段八：MEM → 记忆沉淀

**核心目标**: 让经验成为资产，而非一次性消耗品

**动作**:
1. **项目记忆归档**（调用 `memory-hub`）:
   - 归档本次迭代的 ADR 到 `docs/adr/`
   - 更新项目 INDEX（模块地图、关键决策、技术债务）
2. **经验模式提取**（调用 `hermes-experience`）:
   - 提取可复用的代码片段（Snippet）
   - 记录踩坑记录与解决方案（Rule）
   - 总结本次迭代的最佳实践（Pattern）
3. **代码库上下文更新**（调用 `beads-memory` / `claude-mem`）:
   - 压缩本次变更的核心上下文
   - 更新跨会话记忆文件
   - 确保下次迭代能继承本次上下文
4. 输出**迭代总结**:
   - 时间线（各阶段耗时）
   - 关键决策与理由
   - 技术债务清单（待重构点）
   - 经验卡片（3个以内，方便下次复用）

---

## 用户控制指令

在迭代过程中，用户可以随时发出以下指令控制流程：

| 指令 | 作用 |
|------|------|
| `"下一步"` / `"next"` | 推进到下一阶段 |
| `"回退到xx"` / `"back to REQ"` | 回退到指定阶段 |
| `"跳过xx"` / `"skip TST"` | 跳过当前阶段（需确认风险） |
| `"并行开发"` / `"parallel"` | DEV阶段拆分为前后端并行Agent |
| `"当前状态"` / `"status"` | 输出当前迭代看板 |
| `"产出物清单"` / `"artifacts"` | 列出当前已产出的所有文档/代码 |
| `"风险检查"` / `"risk"` | 扫描当前阶段潜在风险 |
| `"结束迭代"` / `"abort"` | 提前终止，输出已产出物清单 |

---

## 上下文维护机制

Agent 在迭代过程中维护以下上下文，确保跨阶段信息不丢失：

```
Iteration Context
├── meta/
│   ├── name: 迭代名称
│   ├── start_time: 开始时间
│   ├── current_stage: 当前阶段
│   └── status: running/paused/aborted/completed
├── req/
│   ├── prd_path: 需求文件路径
│   ├── scope: 功能范围
│   └── acceptance_criteria: 验收场景[]
├── des/
│   ├── erd: 表结构设计
│   ├── api_contract: 接口契约
│   └── adr: 架构决策记录[]
├── dev/
│   ├── frontend_files: 前端文件[]
│   ├── backend_files: 后端文件[]
│   └── db_migration: 数据库脚本
├── tst/
│   ├── test_report: 测试报告
│   └── security_scan: 安全扫描结果
├── rev/
│   ├── pr_info: PR信息
│   └── review_comments: Review意见[]
├── dep/
│   ├── commit_hash: 提交哈希
│   └── release_version: 发布版本
└── mem/
    ├── snippets: 代码片段[]
    ├── rules: 经验规则[]
    └── patterns: 设计模式[]
```

---

## 与其他Skill的关系

```
enterprise-iteration-agent (总控)
    ├── 编排: dev-flow (方法论参考)
    ├── 编排: multi-agent-orchestration (并行执行框架)
    ├── 编排: skill-orchestrator (Skill匹配导航)
    │
    ├── REQ阶段: openspec-sdd, prd-to-demo, brainstorming
    ├── DES阶段: database-designer, api-doc-generator, frontend-design, taste-skill
    ├── DEV阶段: enterprise-crm-fullstack, backend-change-flow, opinionated-engineer
    ├── TST阶段: testing-patterns, webapp-testing, security-audit
    ├── REV阶段: quality-gate, create-pr, frontend-code-review, confidence-check
    ├── DEP阶段: git-commit, solo-parallel-dev
    └── MEM阶段: memory-hub, hermes-experience, beads-memory
```

---

## 使用示例

### 示例一：标准单线迭代

```
用户: 开始开发【客户标签管理】需求，PRD在 D:\需求\客户\标签管理.md

Agent:
  [INIT] 已初始化迭代看板。读取 PRD 后识别到：
        - 新建表：customer_tag, customer_tag_rel
        - 前端页面：标签列表、标签分配弹窗
        - 后端接口：CRUD + 批量绑定
        - 预计阶段：REQ → DES → DEV → TST → REV → DEP → MEM

用户: 下一步

Agent: [REQ→DES] 进入架构设计...
  → 调用 database-designer 输出 ERD
  → 调用 api-doc-generator 输出接口契约
  → 产出 ADR-001: 标签表设计决策

用户: 下一步

Agent: [DES→DEV] 进入编码开发...
  → 前端：调用 enterprise-crm-fullstack 生成配置式列表页
  → 后端：调用 backend-change-flow 生成 Controller/Service/Mapper
  → 产出：新增6个文件，修改2个文件

...（持续推进至 END）
```

### 示例二：前后端并行迭代（大需求）

```
用户: 处理【沉默客户运营】大需求，前后端并行

Agent:
  [DEV] 启动并行模式：
        - Agent-A (worktree-frontend): 开发 Vue 2 页面
        - Agent-B (worktree-backend): 开发 Java 接口
        - Orchestrator: 每30分钟同步接口契约

  [30分钟后同步]
        - Agent-A 已完成列表页框架，等待接口字段确认
        - Agent-B 已定义 DTO，确认字段与前端一致
        - 继续并行...
```

### 示例三：回退与修正

```
用户: 当前状态

Agent: [DEV] 编码开发阶段，已完成前端页面，后端Service层编写中。
        发现风险：需求中"批量导入"功能未在设计阶段明确接口格式。

用户: 回退到DES

Agent: [DEV→DES] 回退到架构设计阶段。
        → 补充 api-doc-generator：批量导入接口（MultipartFile + 模板下载）
        → 更新 ADR-002：导入处理策略（异步+进度回调）

用户: 下一步

Agent: [DES→DEV] 重新进入开发，已继承更新后的接口契约...
```

---

## 风险熔断机制

当检测到以下情况时，Agent 自动暂停并请求人工确认：

| 熔断条件 | 触发阶段 | 建议动作 |
|---------|---------|---------|
| 需求文件不存在或为空 | INIT/REQ | 确认路径，补充PRD |
| 涉及公共组件改造且无回归方案 | DES | 要求补充兼容性测试计划 |
| 安全扫描发现高危漏洞（SQL注入/RCE） | TST | 强制退回DEV修复 |
| 代码覆盖率低于阈值（核心模块<50%） | TST | 建议补充测试用例 |
| 与主干分支冲突文件>10个 | DEP | 建议先rebase或分批发版 |
| 置信度评分<5 | REV | 建议人工全面Review |
| 数据库DDL未评审 | DES/DEV | 要求DBA或架构师确认 |

---

> "迭代不是代码的堆砌，而是认知的闭环。每一个结束都是下一次开始的前置条件。"
