---
name: "create-pr"
description: "自动生成规范的GitHub Pull Request：分析代码变更，输出格式化标题/摘要/测试计划/影响范围。当用户说'生成PR'、'写PR描述'、'提个PR'、'创建合并请求'、'准备代码审查'、'提交变更'时触发。核心特点：自动分析git diff生成PR内容、Conventional Commits格式、影响范围评估、测试计划自动生成、CI状态检查、标签自动推荐。"
---

> **来源**: 社区热门（Anthropic Skills Marketplace 2026 最流行技能，169.7K）
>
> **发布时间**: 2026-05-20
>
> **理念**: "好的 PR 不是写完后才想起来的，是代码变更的自然延伸。"

# 🔀 Create PR — 自动生成规范 Pull Request

分析代码变更，自动生成格式规范、信息完整的 PR 描述。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **Diff 分析** | 自动读取 `git diff`，识别变更类型和范围 |
| **标题生成** | Conventional Commits 格式，清晰表达变更意图 |
| **摘要生成** | 变更概述、动机、实现方式 |
| **影响评估** | 识别破坏性变更、依赖影响、回滚风险 |
| **测试计划** | 根据变更类型自动生成测试清单 |
| **CI 检查** | 验证测试/构建/检查是否通过 |
| **标签推荐** | 自动推荐 bug/feature/docs/refactor 等标签 |
| **Reviewers 推荐** | 根据代码路径推荐审阅人 |

---

## 🛠️ 工作流程

### Step 1: 收集变更信息

```bash
git diff --stat          # 变更概览
git diff                 # 详细 diff
git log --oneline -5     # 最近提交
git branch --show-current # 当前分支
```

### Step 2: 分析变更

```
分析维度：
□ 变更类型：feat / fix / docs / refactor / test / chore
□ 变更范围：哪些模块/文件受影响
□ 变更规模：新增/删除/修改行数
□ 是否有破坏性变更（BREAKING CHANGE）
□ 是否涉及数据库迁移
□ 是否涉及 API 变更
□ 是否涉及配置变更
```

### Step 3: 生成 PR 内容

---

## 📝 PR 模板

### 标题格式

```
<type>(<scope>): <简短描述>

示例：
feat(auth): 添加 JWT 刷新令牌机制
fix(payment): 修复重复支付回调问题
docs(api): 补充订单接口字段说明
refactor(user): 拆分用户服务为领域模块
```

### 描述模板

```markdown
## 变更概述
<!-- 一句话说明这个 PR 做了什么 -->

## 变更动机
<!-- 为什么要做这个变更？解决了什么问题？ -->

## 实现方式
<!-- 关键实现思路，复杂逻辑需要说明 -->

## 影响范围
- [ ] 涉及 API 变更
- [ ] 涉及数据库迁移
- [ ] 涉及配置变更
- [ ] 存在破坏性变更（BREAKING CHANGE）

## 测试计划
- [ ] 单元测试已更新
- [ ] 集成测试已更新
- [ ] E2E 测试已更新
- [ ] 手动验证通过

## 检查清单
- [ ] 代码遵循团队规范
- [ ] 所有测试通过
- [ ] 文档已更新
- [ ] 无安全漏洞
```

---

## 💡 使用示例

### 示例1：新功能 PR

**变更**：添加了用户密码重置功能

**生成的 PR**：

```markdown
feat(auth): 添加密码重置功能

## 变更概述
实现完整的密码重置流程：请求重置 → 发送邮件 → 验证令牌 → 设置新密码。

## 变更动机
用户目前无法自助找回密码，需要管理员手动重置，效率低。

## 实现方式
- 新增 `/api/auth/forgot-password` 接口：生成重置令牌并发送邮件
- 新增 `/api/auth/reset-password` 接口：验证令牌并更新密码
- 使用 Redis 存储重置令牌（TTL 30 分钟）
- 邮件模板使用 Handlebars 渲染

## 影响范围
- [x] 涉及 API 变更（新增 2 个接口）
- [ ] 涉及数据库迁移
- [ ] 涉及配置变更（需配置 SMTP）
- [ ] 存在破坏性变更

## 测试计划
- [x] 单元测试已更新（覆盖率 92%）
- [x] 集成测试已更新（邮件发送 Mock）
- [ ] E2E 测试已更新
- [x] 手动验证通过（本地测试邮件接收）

## 检查清单
- [x] 代码遵循团队规范
- [x] 所有测试通过
- [x] API 文档已更新
- [x] 无安全漏洞（令牌使用加密随机数）

---

**标签**: `feature`, `auth`, `security`
**Reviewers**: @后端负责人
```

### 示例2：Bug 修复 PR

**变更**：修复订单金额计算精度丢失

**生成的 PR**：

```markdown
fix(order): 修复金额计算浮点数精度丢失

## 变更概述
将订单金额计算从 Number 改为 Decimal.js，避免 0.1 + 0.2 !== 0.3 问题。

## 变更动机
生产环境出现订单金额偏差：¥99.90 显示为 ¥99.89999999999999。

## 实现方式
- 引入 decimal.js 处理所有金额运算
- 数据库层面使用 DECIMAL(10,2) 存储
- 序列化时统一格式化为 2 位小数

## 影响范围
- [ ] 涉及 API 变更（返回格式不变）
- [ ] 涉及数据库迁移
- [ ] 涉及配置变更
- [x] 存在破坏性变更：内部计算逻辑变更，需回归测试所有金额场景

## 测试计划
- [x] 单元测试已更新（新增 15 个边界用例）
- [x] 集成测试已更新
- [x] 手动验证通过（对比修复前后 100 笔订单数据）

## 检查清单
- [x] 代码遵循团队规范
- [x] 所有测试通过
- [x] 无安全漏洞

---

**标签**: `bug`, `order`, `high-priority`
**Reviewers**: @财务模块负责人
```

### 示例3：重构 PR

**变更**：拆分单体用户服务

**生成的 PR**：

```markdown
refactor(user): 拆分单体用户服务为领域模块

## 变更概述
将 2000+ 行的 UserService 拆分为 AuthenticationService、ProfileService、PreferenceService 三个领域模块。

## 变更动机
UserService 职责过重，修改任意功能都需要测试整个文件，维护成本高。

## 实现方式
- 按领域拆分：认证/资料/偏好设置
- 提取共享的 UserRepository 和 UserValidator
- 使用依赖注入解耦
- 保持原有 API 契约不变（兼容层适配）

## 影响范围
- [ ] 涉及 API 变更（保持兼容）
- [ ] 涉及数据库迁移
- [ ] 涉及配置变更
- [ ] 存在破坏性变更（内部重构，API 不变）

## 测试计划
- [x] 单元测试已更新（按新模块拆分）
- [x] 集成测试已更新
- [x] E2E 测试已通过
- [x] 手动验证通过（对比 API 响应完全一致）

## 检查清单
- [x] 代码遵循团队规范
- [x] 所有测试通过
- [x] 文档已更新（架构图已更新）

---

**标签**: `refactor`, `user`, `architecture`
**Reviewers**: @架构组
```

---

## 🏷️ 自动标签规则

| 条件 | 标签 |
|------|------|
| `type === 'fix'` | `bug` |
| `type === 'feat'` | `feature` |
| `type === 'docs'` | `documentation` |
| `type === 'refactor'` | `refactor` |
| 修改 `auth/**` | `security` |
| 修改 `payment/**` | `financial` |
| 修改 `db/migration/**` | `database` |
| 新增 API | `api-change` |
| BREAKING CHANGE | `breaking-change` |
| 测试文件 > 50% | `test-heavy` |

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 |
|-------|------|
| **git-commit** | create-pr 是 git-commit 的自然延伸：commit 规范 → PR 规范 |
| **quality-gate** | PR 生成后应触发 quality-gate 检查 |
| **systematic-debugging** | fix 类型的 PR 可关联调试记录 |

**最佳实践链**：
```
code change → git-commit（规范提交）→ create-pr（生成 PR）→ quality-gate（质量检查）→ review → merge
```

---

## 🚀 快速开始

```
用户：生成 PR / 提个 PR

AI：
1. 读取 git diff 和提交历史
2. 分析变更类型和范围
3. 生成 Conventional Commits 标题
4. 生成完整 PR 描述（概述/动机/实现/影响/测试）
5. 推荐标签和 Reviewers
6. 输出可直接复制到 GitHub 的内容
```

---

> "PR 是代码的简历——第一印象决定审查效率。"
