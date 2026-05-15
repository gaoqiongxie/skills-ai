---
name: "dev-flow"
description: "智能开发工作流：自动感知项目阶段，调用最合适的开发方法论。当用户说'从零开发'、'帮我实现'、'进入开发'、'审查代码'、'准备上线'、'怎么开发'、'完整流程'时触发。核心特点：自动识别当前阶段（需求→设计→编码→测试→上线→复盘），阶段内自动编排方法论（OpenSpec规范→BMAD协作→PDD提示词版本化→OpinionatedEngineer工程标准→AI-DLC质量门控），用户只说'开发'，AI自动走完整流程。"
---

> **来源**: 蒸馏（融合 bmad-method + ai-dlc + opinionated-engineer + prompt-driven-dev + openspec-sdd）
>
> **发布时间**: 2026-05-15
>
> **理念**: "开发不应该纠结用哪个方法论——AI 应该自动知道现在该做什么。"

# 🚀 Dev Flow — 智能开发工作流

你说"开发"，AI 自动感知阶段、编排方法论、交付代码。

---

## 🎯 六阶段自动感知

```
需求探索期 → 架构设计期 → 编码实现期 → 质量验证期 → 部署上线期 → 复盘沉淀期
    ↓              ↓              ↓              ↓              ↓              ↓
OpenSpec      BMAD多角色     PDD + OE       AI-DLC         自动化部署    Hermes
规范驱动      协作设计      提示词版本化    质量门控        + 监控       经验沉淀
   + SDD        + 文档分片    + 工程标准                                    + 复盘
```

---

## 🛠️ 阶段自动切换

### Stage 1: 需求探索期（Discovery）

**识别信号**：
- 用户说"我想做..."、"需要实现..."、"有个需求..."
- 只有模糊想法，没有具体方案

**自动调用**：`openspec-sdd`

**输出**：
- ✅ 需求澄清清单（5W1H）
- ✅ 用户故事 + 验收标准（Gherkin）
- ✅ 功能清单（Must/Should/Could/Won't）
- ✅ 技术约束识别

```
用户：我想做一个任务管理工具

AI（进入需求探索期）：
1. 澄清需求：
   - 是个人用还是团队用？
   - 需要协作功能吗？
   - 数据存储在哪里？
   - 需要移动端吗？

2. 输出规范文档：
   - Feature: 任务创建
     Given 用户在首页
     When 点击"新建任务"
     Then 出现任务表单
     And 提交后任务出现在列表顶部

3. 判定：需求已清晰 → 进入 Stage 2
```

---

### Stage 2: 架构设计期（Design）

**识别信号**：
- 需求已明确
- 用户说"怎么设计..."、"技术方案..."

**自动调用**：`bmad-method`

**输出**：
- ✅ 技术选型 + 理由
- ✅ 系统架构图
- ✅ 数据库设计（ERD）
- ✅ API 契约（OpenAPI）
- ✅ 文档分片清单（上下文工程）

```
AI（进入架构设计期）：
1. 技术选型：
   - 前端: Next.js 14 (App Router)
   - 后端: tRPC + Prisma
   - 数据库: PostgreSQL
   - 部署: Vercel + Railway

2. 架构决策：
   - ADR-001: 使用 Next.js SSR 提升首屏
   - ADR-002: tRPC 替代 REST，类型安全端到端

3. 数据库设计：
   - Task 表: id, title, status, priority, dueDate, userId
   - User 表: id, email, name

4. 判定：设计完成 → 进入 Stage 3
```

---

### Stage 3: 编码实现期（Implementation）

**识别信号**：
- 架构已确定
- 用户说"开始写代码"、"实现..."、"写功能"

**自动调用**：`prompt-driven-dev` + `opinionated-engineer`

**输出**：
- ✅ PDD 提示词分层（System/Context/Task/Template）
- ✅ 测试先行（TDD 红绿重构）
- ✅ 生产级代码（10条硬性规则）
- ✅ 类型完整 + 错误处理 + 日志 + 审计

```
AI（进入编码实现期）：

Step 1: PDD 提示词分层
├── system/backend-developer.md    # 后端开发角色
├── context/task-management.md     # 项目架构上下文
├── tasks/feature-001-auth.md      # 认证功能任务
└── templates/api-endpoint.md      # API 模板复用

Step 2: 先写测试
```typescript
// tests/task.test.ts
describe('TaskService.create', () => {
  it('should create task with valid input', async () => {
    const result = await taskService.create({
      title: 'Test Task',
      priority: 'high'
    });
    expect(result.isOk()).toBe(true);
    expect(result.value.title).toBe('Test Task');
  });

  it('should reject empty title', async () => {
    const result = await taskService.create({ title: '' });
    expect(result.isErr()).toBe(true);
    expect(result.error.code).toBe('VALIDATION_ERROR');
  });
});
```

Step 3: 实现代码（通过 Opinionated Engineer 规则检查）
```typescript
// src/task.service.ts
export class TaskService {
  constructor(
    private readonly taskRepo: TaskRepository,
    private readonly auditLog: AuditLog,
    private readonly logger: Logger,
  ) {}

  async create(input: CreateTaskInput): Promise<Result<Task, TaskError>> {
    this.logger.info('Creating task', { title: input.title });

    // 1. 输入校验
    const validated = createTaskSchema.safeParse(input);
    if (!validated.success) {
      return err({
        code: 'VALIDATION_ERROR',
        message: validated.error.message
      });
    }

    // 2. 业务逻辑
    const task = await this.taskRepo.create({
      ...validated.data,
      status: 'todo',
      createdAt: new Date()
    });

    // 3. 审计日志
    this.auditLog.record('TASK_CREATED', { taskId: task.id });

    return ok(task);
  }
}
```

规则检查：
□ 禁止 TODO - ✅
□ 所有函数有单元测试 - ✅
□ 所有错误已处理 - ✅
□ 已记录日志 - ✅
□ 类型完整 - ✅
□ 无魔法数字 - ✅
□ API 输入已校验 - ✅
□ 数据库操作有事务 - ✅
□ 敏感操作可审计 - ✅
□ 代码可回滚 - ✅

判定：编码完成 → 进入 Stage 4
```

---

### Stage 4: 质量验证期（Quality）

**识别信号**：
- 代码已写完
- 用户说"测试一下"、"审查代码"、"能跑吗"

**自动调用**：`ai-dlc`（Backpressure Gate）+ `quality-gate`

**输出**：
- ✅ 单元测试通过率
- ✅ E2E 场景验证
- ✅ 安全漏洞扫描
- ✅ AI 置信度评估
- ✅ 代码 Review 清单

```
AI（进入质量验证期）：

Backpressure Gate 检查：
┌─────────────────────────────────────────┐
│ Gate 1: 单元测试          ✅ 42/42 通过 │
│ Gate 2: 类型检查            ✅ 0 错误   │
│ Gate 3: Lint               ✅ 0 警告   │
│ Gate 4: 安全扫描            ✅ 0 高危   │
│ Gate 5: AI 置信度           8.5/10     │
└─────────────────────────────────────────┘

Confidence Check:
- 对认证逻辑的信心: 9/10（标准 JWT 实现）
- 对数据库设计的信心: 8/10（需要压测验证索引）
- 对错误处理的信心: 9/10（覆盖了所有边界）

判定：质量通过 → 进入 Stage 5
```

---

### Stage 5: 部署上线期（Deploy）

**识别信号**：
- 代码已通过验证
- 用户说"上线"、"部署"、"发布"

**输出**：
- ✅ 部署脚本（Docker/K8s/Serverless）
- ✅ 环境变量清单
- ✅ 数据库迁移脚本
- ✅ 监控告警配置
- ✅ 回滚方案

```
AI（进入部署上线期）：

部署清单：
□ Docker 镜像构建
□ 数据库迁移（零停机）
□ 环境变量注入
□ 健康检查端点
□ 日志采集配置
□ 告警规则（P99 < 200ms, 错误率 < 0.1%）
□ 回滚脚本（一键回滚到 v1.2.0）
```

---

### Stage 6: 复盘沉淀期（Retrospective）

**识别信号**：
- 项目已上线
- 用户说"总结一下"、"复盘"、"经验教训"

**自动调用**：`hermes-experience`

**输出**：
- ✅ 项目总结（成功/失败因素）
- ✅ 可复用模式（沉淀为经验）
- ✅ 技术债务清单
- ✅ 改进建议

---

## 🔄 阶段跳转控制

用户可以随时干预：

| 用户说 | 行为 |
|--------|------|
| "回到需求" | 回退到 Stage 1 |
| "重新设计" | 回退到 Stage 2 |
| "跳过测试" | 警告风险，可选择跳过 Stage 4 |
| "直接上线" | 快速通道：Stage 3 → Stage 5（跳过详细验证） |
| "只写代码" | 进入 Stage 3，不触发其他阶段 |

---

## 🆚 与被蒸馏 Skill 的关系

| 被蒸馏 Skill | 在 Dev Flow 中的角色 | 何时单独使用 |
|-------------|-------------------|-------------|
| **openspec-sdd** | Stage 1 核心 | 不需要，dev-flow 自动调用 |
| **bmad-method** | Stage 2 核心 | 不需要，dev-flow 自动调用 |
| **prompt-driven-dev** | Stage 3 提示词管理 | 不需要，dev-flow 自动调用 |
| **opinionated-engineer** | Stage 3 编码标准 | 不需要，dev-flow 自动调用 |
| **ai-dlc** | Stage 4 质量门控 | 不需要，dev-flow 自动调用 |

**迁移建议**：新用户直接使用 dev-flow，老用户可按需单独调用底层 Skill（高级场景）。

---

## 🚀 快速开始

```
用户：从零开发一个任务管理工具

AI（自动感知 Stage 1）：
"进入需求探索期...
1. 需求澄清（5W1H）
2. 用户故事 + 验收标准
3. 功能优先级
[完成后自动进入 Stage 2]"

AI（自动进入 Stage 2）：
"进入架构设计期...
1. 技术选型
2. 数据库设计
3. API 契约
[完成后自动进入 Stage 3]"

AI（自动进入 Stage 3）：
"进入编码实现期...
1. 提示词分层（PDD）
2. 先写测试（TDD）
3. 生产级代码（OE 标准）
[完成后自动进入 Stage 4]"

...直到 Stage 6 完成
```

---

> "开发就像开车——你只需要说目的地，Dev Flow 负责换挡。"
