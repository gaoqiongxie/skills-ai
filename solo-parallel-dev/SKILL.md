---
name: "solo-parallel-dev"
description: "单人多分支并行开发工作流：一个人同时开发多个feature/fix/docs时，如何管理分支、预防冲突、恢复上下文、有序合并。当用户说'同时开发几个功能'、'多分支并行'、'分支管理'、'切来切去忘了进度'、'README冲突'、'一个人怎么并行开发'时触发。核心特点：worktree物理隔离、分支状态看板、冲突预防策略、上下文恢复协议、合并排序算法。"
---

> **来源**: 自建（基于 skills-ai 仓库 94 个 skill 的实战经验）
>
> **发布时间**: 2026-05-25
>
> **理念**: "一个人开 5 个分支，不等于 5 倍效率——等于 5 倍混乱。"

# 🌿 Solo Parallel Dev — 单人多分支并行开发工作流

**你既是产品经理，也是开发，也是 QA，也是运维。**

这个 Skill 教你如何在**不把自己逼疯**的前提下，一个人并行推进多个 feature。

---

## 🎯 核心原则

```
原则1: 并行 ≠ 同时写代码
  真正的并行是"A 在等反馈时做 B"，不是"A 写到一半切去做 B"

原则2: 同时活跃的分支 ≤ 3 个
  人脑上下文切换的成本极高，超过 3 个必烂尾

原则3: main 分支永远可部署
  你自己就是唯一的 gatekeeper，不要骗自己

原则4: 用 worktree 物理隔离，不用 stash  mentally 隔离
  stash 会让你忘记，worktree 让你打开文件夹就回到上下文
```

---

## 🏗️ 分支策略

### 分支命名规范

```
feat/<skill-name>-<简短描述>     # 新功能
fix/<bug-desc>                    # 修复
docs/<doc-update>                 # 文档更新
refactor/<scope>                  # 重构
chore/<maintenance>               # 维护性工作

示例：
  feat/backend-change-flow-upgrade
  feat/ai-collaboration-safety
  fix/readme-typo
  docs/cross-platform-guide
```

### 分支生命周期状态

```
🌱 新建    → 刚创建，还没写代码
🌿 开发中  → 正在编码，有未提交变更
🍃 暂存中  → 开发中断，已 stash / 已提交但未完
🌳 待合并  → 代码完成，等待合入 main
🍂 已归档  → 已合并到 main，可删除
```

---

## 🛠️ 工作流：worktree 物理隔离法（推荐）

**为什么用 worktree 而不是 stash / 反复 checkout？**

| 方式 | 切换成本 | 上下文保留 | 同时查看多个分支 |
|------|---------|-----------|-----------------|
| `git checkout` | 中 | 差（靠记忆） | ❌ 不能 |
| `git stash` | 低 | 极差（经常忘） | ❌ 不能 |
| **git worktree** | 低 | **极好**（物理隔离） | ✅ 可以 |

### worktree 设置

```bash
# 主仓库（main 分支）
cd /d/xgq/work/skills-ai

# 为每个 feature 创建独立工作目录
git worktree add ../skills-ai-feat-backend-flow feat/backend-change-flow-upgrade
git worktree add ../skills-ai-feat-ai-safety feat/ai-collaboration-safety
git worktree add ../skills-ai-fix-readme fix/readme-typo

# 查看所有 worktree
git worktree list

# 输出：
# D:/xgq/work/skills-ai            main       [main]
# D:/xgq/work/skills-ai-feat-backend-flow  feat/backend-change-flow-upgrade  [feat/backend-change-flow-upgrade]
# D:/xgq/work/skills-ai-feat-ai-safety     feat/ai-collaboration-safety      [feat/ai-collaboration-safety]
```

**目录结构**：
```
D:\xgq\work\
├── skills-ai/                    # main 分支，稳定版本
├── skills-ai-feat-backend-flow/  # feat/backend-change-flow-upgrade
├── skills-ai-feat-ai-safety/     # feat/ai-collaboration-safety
└── skills-ai-fix-readme/         # fix/readme-typo
```

**切换上下文 = 打开另一个 VS Code 窗口**，不需要 stash，不需要记 stash 里是什么。

---

## 📋 分支状态看板（Branch Kanban）

**你自己维护一个看板文件**，防止遗忘。

### 看板位置

```
skills-ai/
├── .solo-dev/                    # 新建这个目录
│   └── BRANCH_KANBAN.md          # 分支状态看板
```

> 这个文件只在 main 分支维护，每个 feature 分支不修改它。

### 看板模板

```markdown
# 🌿 单人并行开发看板

## 当前活跃分支（最多 3 个）

| 分支 | 状态 | 目标 | 进度 | 阻塞点 | 下一步 |
|------|------|------|------|--------|--------|
| feat/backend-change-flow-upgrade | 🌿 开发中 | 升级七阶段闭环 + AI安全机制 | 阶段⑤编码中 | 等用户确认原子输出规则 | 完成编码，提PR |
| feat/ai-collaboration-safety | 🌳 待合并 | 新建防逼疯Skill | 100% | 无 | 提PR → 合并 |
| fix/readme-typo | 🌳 待合并 | 修复README格式错误 | 100% | 无 | 随时可合 |

## 待开始（Backlog）

| 分支 | 优先级 | 预估工作量 | 依赖 |
|------|--------|-----------|------|
| feat/weather-skill-v2 | P1 | 2天 | 无 |
| feat/frontend-code-review-v2 | P2 | 1天 | 等设计稿 |

## 已归档

| 分支 | 合并日期 | 说明 |
|------|---------|------|
| feat/music-recommender | 2026-05-22 | 音乐推荐Skill |
| feat/cardiac-arrest-guide | 2026-05-20 | 心脏骤停急救指南 |
```

**更新时机**：
- 每次切换分支前 → 更新当前分支的"进度"和"阻塞点"
- 每次合并后 → 移动到"已归档"
- 每周一 → 审视看板，清理烂尾分支

---

## 🔄 上下文恢复协议（Context Recovery）

**场景**：你三天前在分支 A 写了一半，今天切回来，完全不记得当时在想什么。

### 恢复三步法

#### Step 1: 读取分支看板

```bash
cat .solo-dev/BRANCH_KANBAN.md
# 找到分支 A 的"进度"和"阻塞点"
```

#### Step 2: 读取分支内的进度笔记

**每个 feature 分支根目录下放一个 `BRANCH_NOTES.md`**：

```markdown
# 分支笔记：feat/backend-change-flow-upgrade

## 当前焦点
- 正在写阶段⑤的"原子输出协议"部分
- M03 修改点已完成，M04 写到一半

## 关键决策记录
- 2026-05-25: 决定原子输出每次只输出一个方法，而非一个文件
- 2026-05-25: 熔断阈值定为"同一修改点错3次"

## 待确认问题
- [ ] 阶段⑦的"AI盲区清单"格式是否合适？
- [ ] 是否需要和 ai-collaboration-safety 交叉引用？

## 上次离开时的状态
- git status: 有 2 个未暂存文件（backend-change-flow/SKILL.md 修改中）
- 未解决：README.md 还没更新
```

#### Step 3: 查看代码状态

```bash
git status
git diff          # 看看上次改到哪了
git log --oneline -3  # 看看上次提交是什么
```

**如果用了 worktree**：
- 打开对应文件夹 → 文件就躺在那里
- VS Code 的未保存标签页还在（如果你没关窗口）
- 终端历史记录还在（`history | tail -20`）

---

## ⚔️ 冲突预防策略

**单人并行最恶心的冲突：自己改 A 分支的 README，同时改 B 分支的 README，合并时自己和自己冲突。**

### 策略 1：公共文件延迟修改

```
❌ 错误：每个 feature 分支都改 README.md
  → feat/A 改了技能数 93→94
  → feat/B 改了技能数 93→95
  → 合并冲突，自己打自己

✅ 正确：feature 分支里 README.md 要么不改，要么只改目录结构树（不碰统计数字）
  → feat/A 的 README 保持 93 个
  → feat/B 的 README 保持 93 个
  → 合并到 main 后，统一改一次 93→95
```

**具体规则**：
| 文件 | feature 分支能否改 | 处理方式 |
|------|-------------------|---------|
| `SKILL.md`（本分支的） | ✅ 必须改 | 正常开发 |
| `README.md` 目录结构树 | ⚠️ 谨慎改 | 只添加本分支的目录行，不改其他行 |
| `README.md` 技能总数统计 | ❌ 不改 | 留到合并后再改 |
| `README.md` 分类表格 | ⚠️ 谨慎改 | 只添加本分支的行，不改表头 |
| `README.md` 维护记录 | ❌ 不改 | 留到合并后再追加 |

### 策略 2：合并前统一刷新（Reconciliation）

**所有 feature 开发完成后，创建一个 `chore/reconcile-readme` 分支**：

```bash
# 1. 从最新 main 切出
git checkout main
git pull origin main
git checkout -b chore/reconcile-readme

# 2. 统一修改 README 的所有统计数字
# 3. 统一整理目录结构树
# 4. 统一追加维护记录

# 5. 提一个单独的 PR："docs: 统一更新 README 统计信息"
```

### 策略 3：先合小的，后合大的

**合并顺序影响冲突量**：

```
推荐顺序：
1. fix/* 分支（改动小，先合，减少后续冲突面）
2. docs/* 分支（改动中，无逻辑变更）
3. feat/* 分支（按改动量从小到大）
   → feat/小功能（改 2 个文件）
   → feat/中功能（改 5 个文件）
   → feat/大功能（改 10+ 个文件，重构级）
```

**原因**：
- 小分支先合入 main → main 更新 → 大分支 rebase 到最新 main → 大分支解决冲突
- 如果大分支先合 → 小分支 rebase 时要解决大分支引入的冲突，亏死

---

## 📦 合并策略

### 单人推荐：Rebase + Fast-forward（保持线性历史）

```bash
# 假设要合并 feat/ai-collaboration-safety

# 1. 确保 main 最新
git checkout main
git pull origin main

# 2. 切到 feature 分支，rebase 到最新 main
git checkout feat/ai-collaboration-safety
git rebase main
# （如有冲突，在本分支解决，不污染 main）

# 3. 切回 main，快进合并
git checkout main
git merge feat/ai-collaboration-safety --ff-only

# 4. 推送
git push origin main

# 5. 清理
git branch -d feat/ai-collaboration-safety
git push origin --delete feat/ai-collaboration-safety
```

### 如果 feature 分支已经 push 到远程（有 PR）

```bash
# 用 squash 合并，保持 main 历史干净
git checkout main
git merge feat/xxx --squash
# 生成一个干净的提交

git commit -m "feat: xxx

- 功能点1
- 功能点2

Closes #PR编号"
```

---

## 🧹 防烂尾机制

**一个人最容易犯的错误：开了 5 个分支，3 个烂尾。**

### 烂尾识别信号

| 信号 | 说明 | 处理 |
|------|------|------|
| 分支超过 7 天无提交 | 大概率已忘记上下文 | 要么强制恢复，要么删除 |
| 分支看板状态为"暂存中"超过 3 天 | 阻塞点没解决 | 评估是否值得继续，或降级为 backlog |
| 分支里有大量 WIP 提交 | "save point"式提交 | rebase -i 整理提交历史再合 |
| 分支目标变得不清晰 | 做着做着忘了初衷 | 回看最初的 issue / 需求描述 |

### 每周清理仪式（Monday Cleanup）

```bash
# 1. 列出所有本地分支
git branch -v

# 2. 识别烂尾分支
#    - 超过 7 天未动
#    - 最后一次提交是 WIP / save / temp

# 3. 对每个烂尾分支做决策：
#    A. 继续 → 执行上下文恢复协议
#    B. 废弃 → git branch -D <branch>
#    C. 降级 → 移动到 backlog，不活跃处理

# 4. 更新 BRANCH_KANBAN.md
```

---

## 🚀 完整工作流示例

### 场景：你要同时开发 3 个 feature

```
Feature A: 升级 backend-change-flow（大，2天）
Feature B: 新建 ai-collaboration-safety（中，1天）
Feature C: 修复 README typo（小，10分钟）
```

**Day 1 上午**：
```bash
# 创建 worktree
git worktree add ../skills-ai-feat-a feat/backend-change-flow-upgrade
git worktree add ../skills-ai-feat-b feat/ai-collaboration-safety
git worktree add ../skills-ai-feat-c fix/readme-typo

# 更新 BRANCH_KANBAN.md
# 状态：A-开发中，B-新建，C-新建
```

**Day 1 上午-下午**：在 `skills-ai-feat-c` 里修 typo
```bash
cd /d/xgq/work/skills-ai-feat-c
# 改代码 → git commit → push
# 状态更新：C-待合并
```

**Day 1 下午**：合入 C，开始 B
```bash
# 合入 C
cd /d/xgq/work/skills-ai
git checkout main && git pull
git merge fix/readme-typo --ff-only && git push

# 开始 B
cd /d/xgq/work/skills-ai-feat-b
# 开发 ai-collaboration-safety
# 状态更新：C-已归档，B-开发中
```

**Day 1 晚上**：B 完成，A 开了个头
```bash
# B 完成
cd /d/xgq/work/skills-ai-feat-b
git commit → push
# 状态更新：B-待合并

# A 写了 BRANCH_NOTES.md，完成了阶段①②③
cd /d/xgq/work/skills-ai-feat-a
# 写笔记 → commit
# 状态更新：A-开发中（阶段④）
```

**Day 2 上午**：合入 B
```bash
cd /d/xgq/work/skills-ai
git merge feat/ai-collaboration-safety --ff-only && git push
# 状态更新：B-已归档
```

**Day 2 全天**：专注 A
```bash
cd /d/xgq/work/skills-ai-feat-a
# 用 backend-change-flow 完成阶段④⑤⑥⑦
# 状态更新：A-待合并
```

**Day 3 上午**：合入 A，创建 reconcile 分支刷新 README
```bash
cd /d/xgq/work/skills-ai
git merge feat/backend-change-flow-upgrade --ff-only && git push

git checkout -b chore/reconcile-readme
# 统一改 README 统计数字
# 提 PR → 自审 → 合并
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 如何使用 |
|-------|------|---------|
| **backend-change-flow** | 每个 feature 的执行器 | 在每个 worktree 里独立跑七阶段闭环 |
| **ai-collaboration-safety** | 情绪保险 | 当某个 feature 被 AI 逼疯时，切换到这里恢复 |
| **create-pr** | 合并前检查 | 每个 feature 合入 main 前，生成规范 PR 描述（即使自己合） |
| **quality-gate** | 合并前检查 | 每个 feature 分支提交前跑五维检查 |
| **multi-agent-orchestration** | 进阶并行 | 如果 feature 完全独立，可用多个 Agent 并行工作（worktree 隔离） |
| **git-commit** | 规范提交 | 每个 commit 用 Conventional Commits 格式 |

**最佳实践链**：
```
solo-parallel-dev（分支规划 + worktree 隔离）
     ↓
backend-change-flow（每个 feature 的开发闭环）
     ↓
ai-collaboration-safety（被 AI 逼疯时恢复）
     ↓
quality-gate（提交前检查）
     ↓
create-pr（生成 PR，留记录）
     ↓
solo-parallel-dev（合并 + 归档 + 清理）
```

---

## 🚀 快速入口

```
"我要同时开发几个功能" → 分支规划 + worktree 设置
"分支管理" → 分支状态看板 + 命名规范
"切来切去忘了进度" → 上下文恢复协议
"README冲突" → 冲突预防策略（公共文件延迟修改）
"一个人怎么并行开发" → 完整工作流 + 防烂尾机制
```

---

> "一个人并行开发的关键不是技术——是自律。worktree 帮你物理隔离，看板帮你对抗遗忘，延迟修改 README 帮你避免自己打自己。"
