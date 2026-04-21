---
name: "git-commit"
description: >
  Git 提交信息生成器：根据代码变更自动生成规范化的 Git commit message。
  支持 Conventional Commits 格式（feat/fix/docs/style/refactor/test/chore 等）。
  触发词：写git提交信息、commit信息、git message、规范提交、提交说明、git commit
---

# 📝 Git Commit 规范生成器

> 根据代码变更，生成规范的 commit message，告别 "fix bug" 和 "update"

---

## 支持的 Commit 类型

| 类型 | 含义 | 使用场景 |
|------|------|---------|
| **feat** | 新功能 | 新增接口/页面/模块 |
| **fix** | 修复bug | 修复生产问题/逻辑错误 |
| **docs** | 文档更新 | README/注释/接口文档 |
| **style** | 代码格式 | 格式化、空格、换行（不影响逻辑） |
| **refactor** | 重构 | 优化代码结构但不改变功能 |
| **perf** | 性能优化 | SQL优化/缓存/算法改进 |
| **test** | 测试相关 | 新增测试用例 |
| **chore** | 构建/工具 | 依赖更新/配置文件 |
| **ci** | CI/CD | GitHub Actions/Dockerfile |
| **merge** | 合并分支 | 分支合并 |

---

## 工作流程

### Step 1：获取变更内容

使用以下方式之一：

```
# 查看暂存区变更
git diff --cached

# 查看工作区变更
git diff

# 查看最近提交
git log -3 --oneline
```

### Step 2：分析变更类型

识别本次变更的核心内容：
- 改了哪些文件？
- 核心改动是什么（新增/修复/重构）？
- 涉及哪个模块？

### Step 3：生成 Commit Message

---

## 输出格式

### 格式一：Conventional Commits（推荐团队使用）

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

**示例：**
```
feat(crm): 新增客户跟进记录查询接口

支持按跟进时间/跟进人筛选，返回完整的跟进记录列表。
关联工单：PROJ-123
```

### 格式二：简洁单行（日常小改动）

```
<type>: <简短描述>
```

**示例：**
```
fix(mmp): 修复订单状态枚举值错误

fix(user): 修正用户头像URL为空时报错
docs(readme): 更新部署文档
```

---

## 常见场景模板

### 🐛 修复生产问题

```
fix(<模块>): 修复<问题描述>

问题原因：<根因>
修复方案：<解决方式>
影响范围：<涉及的接口/页面>
```

### ✨ 新增功能

```
feat(<模块>): 新增<功能名称>

功能说明：
- <子功能点1>
- <子功能点2>

关联需求：<需求编号>
```

### 🔄 代码重构

```
refactor(<模块>): 重构<原有逻辑>为<新实现>

改动原因：<为什么要改>
改动范围：<涉及的文件>
注意事项：<兼容性问题等>
```

### 📝 文档更新

```
docs(<模块>): 更新<文档名称>

更新内容：
- <更新点1>
- <更新点2>
```

---

## 分支命名规范

配合 Commit Type，建议分支命名：

```
feature/模块-功能名        # 新功能
bugfix/模块-问题简述        # 修复bug
hotfix/问题简述             # 紧急修复
refactor/模块-重构内容       # 重构
docs/文档内容               # 文档
```

---

## 使用提示

- 直接粘贴 `git diff` 输出，AI 自动分析并生成规范 commit
- 可以指定团队规范（如公司内部格式要求）
- 大改动建议用多行格式，小改动用单行
- **推荐**：在 commit 前使用，帮助组织提交粒度

---

## 一句话原则

> 一个好的 commit message = 标题说明**做了什么**，正文说明**为什么做**。
> 未来回溯时，你会感谢写 commit 的自己。
