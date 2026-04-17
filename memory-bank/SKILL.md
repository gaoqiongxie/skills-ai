# Memory Bank - 项目记忆系统

> 适用场景：新建项目时快速搭建记忆系统 / 现有项目补充文档结构
> 触发关键词：搭建记忆系统、创建项目文档、初始化项目知识库、memory-bank

---

## 🎯 核心理念

**让 AI 从"陌生人"变成"老员工"**

每次启动新项目或接手旧项目，AI 需要大量时间了解背景。Memory Bank 把这些信息结构化存档，AI 读一遍就能上手。

---

## 📁 目录结构

```
项目名-memory-bank/
├── AGENTS.md           # 🔴 核心：AI必读的项目全局上下文
├── INDEX.md            # 文件导航
├── README.md           # 项目说明
├── templates/          # 开发模板库
│   ├── 01-project-profile.md     # 项目概况模板
│   ├── 07-coding-standards.md    # 编码规范模板
│   ├── 09-todo-tracker.md        # TODO追踪模板
│   ├── 10-snippets.md            # 代码片段模板
│   ├── 11-feign-guide.md         # Feign调用指南
│   ├── 12-mq-guide.md           # MQ使用指南
│   ├── feature-prompt.md         # 功能开发模板
│   ├── bugfix-prompt.md          # Bug修复模板
│   ├── code-review-prompt.md    # 代码审查模板
│   └── test-prompt.md            # 测试用例模板
├── knowledge/          # ADR技术决策记录
│   ├── ADR-001-选择技术栈.md
│   └── ...
├── rules/              # 📋 项目规则（hermes-experience配套）
│   ├── shared-rules.md          # 共享规则
│   └── <助手名>-助手.md          # 助手配置
└── projects/           # 各模块详细文档
```

---

## 📄 AGENTS.md（项目全局上下文）

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
| 后端 | Java/Spring Boot | 3.x |
| 数据库 | MySQL | 8.0 |
| 缓存 | Redis | 6.x |
| 消息队列 | RabbitMQ / RocketMQ | - |
| ORM | MyBatis Plus | 3.5.x |
| 前端 | Vue3 | 3.x |
| ... | ... | ... |

## 3. 项目结构

```
src/
├── main/
│   ├── java/com/xxx/
│   │   ├── controller/   # 控制器层
│   │   ├── service/     # 服务层
│   │   ├── mapper/      # 数据访问层
│   │   ├── entity/      # 实体类
│   │   ├── vo/          # 视图对象
│   │   ├── dto/         # 数据传输对象
│   │   ├── req/         # 请求对象
│   │   ├── resp/        # 响应对象
│   │   └── common/      # 公共组件
│   └── resources/
│       ├── mapper/      # MyBatis XML
│       └── config/      # 配置文件
└── test/
```

## 4. 代码规范

### 命名规范
- **类名**：大驼峰（UserService）
- **方法名**：小驼峰（getUserById）
- **常量**：全大写下划线（MAX_RETRY_COUNT）
- **数据库表**：小写下划线（sys_user）
- **包名**：全小写（com.xxx.crm）

### 分层规范
- Controller：参数校验、参数转换、调用Service
- Service/ServiceImpl：业务逻辑处理、事务管理
- Mapper：数据库操作（只做CRUD，不写业务）
- VO/DTO/Req/Resp：数据传输对象

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
<type>: story#<禅道编号> <需求名称> <具体改动>

type: feat | fix | docs | style | refactor | test | chore
example: feat: story#12345 用户登录接口实现
```

## 6. 数据库规范

- 表名、字段名使用小写下划线
- 必须有 `id`（主键）、`create_time`、`update_time`
- 逻辑删除用 `deleted` 字段
- 金额用 DECIMAL，日期用 DATETIME
- 敏感字段加密存储

## 7. 安全规范

- 禁止硬编码密钥/密码
- 用户密码必须 BCrypt 加密
- SQL 参数化查询，禁止字符串拼接
- 接口需权限校验
- 禁止使用 `System.out.println()`，统一用 `@Slf4j` 的 `log`

## 8. 常用命令

```bash
# 启动项目
mvn spring-boot:run

# 运行测试
mvn test

# 构建打包
mvn clean package -DskipTests

# 更新代码
git pull
```

## 9. 环境信息

| 环境 | URL | 说明 |
|------|-----|------|
| 开发 | http://localhost:8080 | 本地开发 |
| 测试 | https://test.xxx.com | 测试环境 |
| 生产 | https://api.xxx.com | 正式环境 |

## 10. 注意事项

- ⚠️ 涉及跨项目调用（Feign）时，变更需同步通知对方
- ⚠️ 金额计算统一用 BigDecimal
- ⚠️ 日期时间统一用 LocalDateTime
- ⚠️ 生产环境禁止开启 debug 日志
```

---

## 📝 初始化流程（新项目）

当用户说"帮我初始化XXX项目的记忆库"时，执行以下步骤：

### 第一步：收集项目信息

| 信息项 | 示例 | 说明 |
|--------|------|------|
| 项目名称 | `fss` | 英文缩写，用于目录命名 |
| 项目中文名 | 财务共享服务 | 用于规则文件和日志 |
| 代码路径 | `D:\fehorizon\crm\fss` | 项目根目录 |
| 技术栈 | Spring Boot + Vue 3 | 主要技术栈 |
| 项目说明 | 财务共享服务平台 | 一句话描述 |

### 第二步：创建记忆库目录

```
项目记忆库路径：D:\xgq\kimi\memory-bank\<项目名>\
├── 01-project-profile.md     # 项目概况
├── 07-coding-standards.md    # 编码规范
├── 09-todo-tracker.md        # TODO追踪
├── 10-snippets.md            # 代码片段
├── 11-feign-guide.md         # Feign调用指南
├── 12-mq-guide.md           # MQ使用指南
└── 99-dialogue-logs/         # 对话日志目录
```

### 第三步：创建项目规则文件

在项目 `.trae/rules/` 目录下创建：

#### 1. `<项目名>-shared-rules.md` — 项目共享规则

```markdown
# <项目中文全称> 项目共享规则

> 本文件是项目规则的单一事实来源，供 AI 助手共同引用。

---

## 项目清单

| 项目 | 代码路径 | 说明 |
|------|----------|------|
| <项目中文全称> | <代码路径> | <项目说明> |

---

## 技术栈

<技术栈>

---

## 编码规范

- 遵循项目现有代码风格
- 新增方法必须有 Javadoc
- 复杂逻辑加行注释
- 金额用 BigDecimal，日期用 LocalDateTime
- 禁止使用 `System.out.println()`，统一用 `@Slf4j` 的 `log`

---

## Git 规范

提交格式：`feat: story#<禅道编号> <需求名称> <具体改动>`

---

## 禁止行为

- 禁止执行 `git reset --hard`、`git rebase` 等改写历史的操作
- 禁止修改无关文件和测试逻辑
- 禁止在 memory-bank 目录存放非 .md 文件
```

#### 2. `<助手名>-助手.md` — 助手配置

```markdown
# <助手名> — 项目专属配置

你是「<助手名>」，<项目中文全称>的专属开发助手。

## 工作路径

- 代码路径：`<代码路径>`
- 记忆库：`D:\xgq\kimi\memory-bank\<项目名>\`
- 规则文件：`.trae/rules/<项目名>-shared-rules.md`

## 工作流程

1. 编码前先看同模块已有文件的写法，遵循现有代码风格
2. 产生有价值信息时写入对话日志
3. 涉及新需求/Bug 时，读取 `09-todo-tracker.md`
```

### 第四步：更新项目清单

将新项目追加到本 Skill 的「项目清单」中。

---

## 🔄 共享记忆库（多项目协同）

```
D:\xgq\kimi\memory-bank\shared\           # 所有项目共享
├── 01-cross-project-map.md    # 跨项目依赖关系图
├── 02-shared-constants.md     # 共享常量与枚举映射
├── 03-api-contracts.md        # 跨项目API契约（Feign接口）
├── 04-db-shared-tables.md     # 共享数据库表说明
└── 99-dialogue-logs/          # 跨项目对话日志
```

### 共享规则
- API契约变更：同步更新 model 模块的 DTO/Req/Resp
- 共享枚举变更：所有相关项目的规则文件同步更新
- 共享表结构变更：评估对所有相关项目的影响

---

## 📝 模板文件

### 01-project-profile.md 模板

```markdown
# <项目中文全称> — 项目概况

## 基本信息

| 项目 | 值 |
|------|-----|
| 项目名称 | <项目中文全称> |
| 英文缩写 | <项目名> |
| 代码路径 | <代码路径> |
| 技术栈 | <技术栈> |
| 初始化日期 | <YYYY-MM-DD> |

## 项目结构

（待补充：扫描项目目录后自动生成）

## 核心模块

（待补充：了解业务后逐步完善）

## 负责人

| 模块 | 负责人 | 联系方式 |
|------|--------|----------|
| - | - | - |
```

### 09-todo-tracker.md 模板

```markdown
# <项目中文全称> — TODO追踪

## 进行中

| 编号 | 需求/Bug | 禅道编号 | 状态 | 备注 |
|------|---------|---------|------|------|
| - | - | - | - | - |

## 已完成

| 编号 | 需求/Bug | 禅道编号 | 完成日期 | 备注 |
|------|---------|---------|---------|------|
| - | - | - | - | - |
```

### 10-snippets.md 模板

```markdown
# <项目中文全称> — 代码片段

## 常用工具类

### 分页封装
```java
// 代码示例
```

### 统一响应封装
```java
// 代码示例
```

## 业务模板

### 标准的CRUD
```java
// 代码示例
```

### Feign调用
```java
// 代码示例
```
```

### 11-feign-guide.md 模板

```markdown
# <项目中文全称> — Feign调用指南

## 调用方配置

### Maven依赖
```xml
<dependency>
    <groupId>com.xxx</groupId>
    <artifactId>xxx-api</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Feign Client声明
```java
@FeignClient(name = "xxx-service", url = "${feign.xxx.url}")
public interface XxxClient {
    // 接口方法
}
```

## 被调用方接口

（待补充）

## 注意事项

- 变更接口需同步通知调用方
```

### 12-mq-guide.md 模板

```markdown
# <项目中文全称> — MQ使用指南

## 交换机/队列配置

| 交换机 | 类型 | 队列 | RoutingKey |
|--------|------|------|------------|
| - | - | - | - |

## 消息格式

```json
{
  "eventType": "xxx",
  "data": {}
}
```

## 消费者示例

```java
@RabbitListener(queues = "xxx-queue")
public void handleXxx(Message message) {
    // 处理逻辑
}
```

## 注意事项

- 消费幂等性处理
- 失败重试机制
```

---

## 🚀 快速开始

```
用户：帮我搭建项目记忆系统
AI：请告诉我项目名称和技术栈

用户：CRM系统，Java Spring Boot + MySQL
AI：【生成完整的 memory-bank 目录结构 + 所有模板】
```

---

## ⚙️ 自定义选项

| 选项 | 说明 | 默认值 |
|------|------|--------|
| 项目名 | memory-bank 父目录名 | {项目名}-memory-bank |
| 记忆库路径 | 项目记忆库存放位置 | D:\xgq\kimi\memory-bank\{项目名} |
| 助手名 | AI助手名称 | 挖挖 |
| 语言 | 注释和文档语言 | 中文 |
