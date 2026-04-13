# Memory Bank - 项目记忆系统

> 适用场景：新建项目时快速搭建记忆系统 / 现有项目补充文档结构
> 触发关键词：搭建记忆系统、创建项目文档、初始化项目知识库、memory-bank

---

## 📁 目录结构

```
项目名-memory-bank/
├── AGENTS.md           # 🔴 核心：项目全局上下文（必读）
├── INDEX.md            # 📖 文件导航
├── README.md           # 项目说明
├── templates/          # 📝 常用 Prompt 模板
│   ├── feature-prompt.md
│   ├── bugfix-prompt.md
│   ├── code-review-prompt.md
│   └── test-prompt.md
├── knowledge/          # 💡 技术决策记录（ADR）
│   ├── ADR-001-选择技术栈.md
│   └── ...
└── projects/           # 📚 各模块详细文档
    ├── module-a/
    ├── module-b/
    └── ...
```

---

## 📄 文件模板

### AGENTS.md（项目全局上下文）

```markdown
# AGENTS.md - 项目全局上下文

> ⚠️ 每个 AI Agent 启动项目时必读此文件

## 1. 项目概述

- **项目名称**：
- **项目类型**：Web应用 / API服务 / 微服务 / 移动端
- **核心功能**：
- **目标用户**：

## 2. 技术栈

| 类别 | 技术 | 版本 |
|------|------|------|
| 后端 | Java/Spring Boot | 2.7.x |
| 数据库 | MySQL | 8.0 |
| 缓存 | Redis | 6.x |
| 前端 | Vue3 | 3.x |
| ... | ... | ... |

## 3. 项目结构

```
src/
├── main/
│   ├── java/com/xxx/
│   │   ├── controller/   # 控制器层
│   │   ├── service/      # 服务层
│   │   ├── mapper/       # 数据访问层
│   │   ├── entity/       # 实体类
│   │   └── common/       # 公共组件
│   └── resources/
│       ├── mapper/       # MyBatis XML
│       └── config/       # 配置文件
└── test/
```

## 4. 代码规范

### 命名规范
- **类名**：大驼峰（UserService）
- **方法名**：小驼峰（getUserById）
- **常量**：全大写下划线（MAX_RETRY_COUNT）
- **数据库表**：小写下划线（sys_user）

### 分层规范
- Controller：参数校验、参数转换、调用Service
- Service：业务逻辑处理、事务管理
- Mapper：数据库操作（只做CRUD，不写业务）
- VO/DTO：数据传输对象

### API 规范
- 统一响应格式：`{"code": 200, "msg": "success", "data": {...}}`
- 分页格式：`{"total": 100, "list": [...]}`
- HTTP状态码：200成功 / 400参数错误 / 401未认证 / 403无权限 / 500系统错误

## 5. Git 规范

### 分支策略
- `main`：主分支，仅通过 PR 合并
- `develop`：开发分支
- `feature/xxx`：功能分支
- `bugfix/xxx`：修复分支

### Commit 规范
```
<type>: <subject>

type: feat | fix | docs | style | refactor | test | chore
example: feat: 新增用户登录功能
```

## 6. 数据库规范

- 表名、字段名使用小写下划线
- 必须有 `id`（主键）、`create_time`、`update_time`
- 逻辑删除用 `deleted` 字段
- 敏感字段加密存储

## 7. 安全规范

- 禁止硬编码密钥/密码
- 用户密码必须 BCrypt 加密
- SQL 参数化查询，禁止字符串拼接
- 接口需权限校验

## 8. 常用命令

```bash
# 启动项目
mvn spring-boot:run

# 运行测试
mvn test

# 构建打包
mvn clean package -DskipTests

# 数据库迁移
mvn flyway:migrate
```

## 9. 环境信息

| 环境 | URL | 说明 |
|------|-----|------|
| 开发 | http://localhost:8080 | 本地开发 |
| 测试 | https://test.xxx.com | 测试环境 |
| 生产 | https://api.xxx.com | 正式环境 |

## 10. 注意事项

- ⚠️ 第三方支付接口需加密处理
- ⚠️ 生产环境禁止开启 debug 日志
- ⚠️ 大数据量操作需分批处理
```

---

### INDEX.md（文件导航）

```markdown
# INDEX.md - 文件导航

> 本文件提供项目文档的快速索引

## 📂 文档目录

### 核心文档
- [AGENTS.md](./AGENTS.md) - 项目全局上下文 ⭐必读
- [README.md](./README.md) - 项目说明

### 模板库
- [功能开发模板](./templates/feature-prompt.md)
- [Bug修复模板](./templates/bugfix-prompt.md)
- [代码审查模板](./templates/code-review-prompt.md)
- [测试用例模板](./templates/test-prompt.md)

### 技术决策
- [ADR-001-选择技术栈](./knowledge/ADR-001-选择技术栈.md)

### 模块文档
- [用户模块](./projects/user/)
- [订单模块](./projects/order/)

## 🔍 快速链接

| 需求 | 查看 |
|------|------|
| 了解项目结构 | AGENTS.md |
| 新功能开发 | templates/feature-prompt.md |
| Bug修复 | templates/bugfix-prompt.md |
| 技术选型 | knowledge/ |
```

---

### templates/feature-prompt.md（功能开发模板）

```markdown
# 功能开发 Prompt 模板

## 📋 需求描述

**功能名称**：
**需求来源**：
**优先级**：P0/P1/P2/P3
**截止日期**：

### 功能描述
（详细描述要实现的功能）

### 用户故事
As a [用户角色], I want [功能], so that [价值]

### 验收标准
- [ ] 标准1
- [ ] 标准2
- [ ] 标准3

---

## 🏗️ 技术方案

### 接口设计
```
POST /api/v1/xxx
Request: {...}
Response: {...}
```

### 数据结构
```java
// 实体类
public class Xxx {
    // 字段说明
}
```

### 业务流程
（流程图或文字描述）

### 数据库变更
```sql
-- 如有DDL变更
```

---

## 📝 开发记录

| 日期 | 开发者 | 内容 | 状态 |
|------|--------|------|------|
| 2024-01-01 | 张三 | 完成基础功能 | ✅ |
| 2024-01-02 | 张三 | 补充异常处理 | ✅ |
```

---

### templates/bugfix-prompt.md（Bug修复模板）

```markdown
# Bug修复 Prompt 模板

## 🐛 Bug信息

**Bug编号**：BUG-001
**严重程度**：P0(致命)/P1(严重)/P2(一般)/P3(轻微)
**发现日期**：
**发现人**：

### 问题描述
（详细描述Bug现象）

### 复现步骤
1. 步骤1
2. 步骤2
3. 步骤3

### 预期行为
（正常应该怎样）

### 实际行为
（实际怎样）

---

## 🔍 根因分析

### 错误日志
```
（粘贴错误日志）
```

### 代码位置
- 文件：
- 方法：
- 行号：

### 根因
（分析为什么会出Bug）

---

## ✅ 修复方案

### 修复代码
```java
// 修改前
xxx

// 修改后
xxx
```

### 验证结果
- [ ] 本地测试通过
- [ ] 单元测试通过
- [ ] 回归测试通过

---

## 📝 修复记录

| 日期 | 修复人 | 内容 |
|------|--------|------|
| 2024-01-01 | 张三 | 修复xxx问题 |
```

---

### templates/code-review-prompt.md（代码审查模板）

```markdown
# Code Review Prompt 模板

## 📦 PR信息

**PR编号**：#123
**分支**：feature/xxx -> develop
**作者**：
**审查人**：

---

## 📝 改动概述

### 改动文件
- `src/main/java/.../UserService.java`
- `src/main/java/.../UserController.java`

### 改动内容
（简要说明改动点）

---

## 🔍 审查要点

### 1. 代码规范
- [ ] 命名是否符合规范
- [ ] 是否有多余的注释或缺失必要注释
- [ ] 代码格式是否统一

### 2. 业务逻辑
- [ ] 逻辑是否正确
- [ ] 边界条件是否处理
- [ ] 异常情况是否处理

### 3. 安全性
- [ ] 是否有SQL注入风险
- [ ] 是否有XSS风险
- [ ] 敏感信息是否泄露

### 4. 性能
- [ ] 是否有N+1查询问题
- [ ] 是否有不必要的循环
- [ ] 大数据量是否有分页

### 5. 可维护性
- [ ] 是否符合分层规范
- [ ] 是否易于扩展
- [ ] 是否有重复代码

---

## 💬 审查意见

### 必须修改 🔴
（严重问题，必须修改后再合并）

### 建议修改 🟡
（建议修改，但不是强制）

### 可以通过 🟢
（没有问题，可以合并）

---

## ✅ 审查结论

- [ ] **通过** - 可以合并
- [ ] **需修改** - 需要修改后再审
- [ ] **拒绝** - 不允许合并
```

---

### templates/test-prompt.md（测试用例模板）

```markdown
# 测试用例 Prompt 模板

## 📋 测试范围

**模块**：
**测试类型**：单元测试/集成测试/系统测试
**关联需求**：

---

## 🧪 用例设计

### 用例1：正常流程
| 字段 | 内容 |
|------|------|
| 用例ID | TC-001 |
| 用例名称 | xxx正常操作 |
| 前置条件 | 用户已登录 |
| 测试步骤 | 1. xxx 2. xxx 3. xxx |
| 预期结果 | 显示xxx |

### 用例2：异常流程
| 字段 | 内容 |
|------|------|
| 用例ID | TC-002 |
| 用例名称 | xxx异常情况 |
| 前置条件 | xxx |
| 测试步骤 | 1. xxx |
| 预期结果 | 提示xxx |

---

## 📊 测试结果

| 用例ID | 执行结果 | 执行人 | 日期 |
|--------|----------|--------|------|
| TC-001 | ✅通过 | 张三 | 2024-01-01 |
| TC-002 | ❌失败 | 张三 | 2024-01-01 |

### 缺陷记录
| 缺陷ID | 描述 | 严重程度 | 状态 |
|--------|------|----------|------|
| BUG-001 | xxx | P1 | 已修复 |
```

---

### knowledge/ADR-001-xxx.md（技术决策记录模板）

```markdown
# ADR-001 - 技术决策记录

> ADR = Architecture Decision Record

## 状态
**提议中** / **已接受** / **已废弃** / **已被替代**

## 背景
（描述做出这个决策的背景）

## 决策
（描述做出的决策）

## 方案对比

### 方案A
- 优点：xxx
- 缺点：xxx

### 方案B
- 优点：xxx
- 缺点：xxx

### 方案C（最终选择）
- 优点：xxx
- 缺点：xxx

## 后果
- **正面**：xxx
- **负面**：xxx
- **风险**：xxx

## 相关文档
- 参考链接1
- 参考链接2
```

---

## 🚀 使用方式

### 1. 新项目初始化
```
用户：帮我搭建项目记忆系统
助手：请告诉我项目名称和技术栈，我来帮你生成完整的 memory-bank 目录结构
```

### 2. 增量补充
```
用户：现有项目想加一个bug修复模板
助手：直接生成 templates/bugfix-prompt.md 并告诉你怎么用
```

### 3. 自定义修改
```
用户：需要加一个部署文档模板
助手：生成 templates/deploy-prompt.md 并集成到 INDEX.md
```

---

## ⚙️ 自定义选项

| 选项 | 说明 | 默认值 |
|------|------|--------|
| 项目名 | memory-bank 父目录名 | {项目名}-memory-bank |
| 语言 | 注释和文档语言 | 中文 |
| 技术栈 | 决定目录结构和模板内容 | Java/Spring Boot |

---

> 💡 **提示**：AGENTS.md 是核心，其他都是配套。按需启用，不必一次性创建所有文件。
