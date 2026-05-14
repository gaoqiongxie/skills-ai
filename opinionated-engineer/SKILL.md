---
name: "opinionated-engineer"
description: "工程化脚手架：为AI编码提供有主见的最佳实践约束，拒绝'随便写写'。当用户说'按工程标准来'、'production ready'、'工业级代码'、'不要胡写'、'严肃工程'、'上强度'、'像 senior 写的'时触发。核心特点：强制TDD/类型安全/错误处理/日志规范，禁止TODO和伪代码，要求可测试可部署，不符合标准直接打回重写。"
---

> **来源**: mattpocock/skills ⭐75K（2026年5月 GitHub Trending #1）
>
> **发布时间**: 2026-05-14
>
> **理念**: "AI 不应该'帮忙写代码'，而应该'像 Senior Engineer 一样交付代码'。"

# 🏗️ Opinionated Engineer — 有主见的工程脚手架

给 AI 编码加上工程纪律，让输出从"能跑"升级为"能上线"。

---

## 🎯 核心约束

### 必须遵守（硬性规则）

| # | 规则 | 违反后果 |
|---|------|---------|
| 1 | **禁止 TODO / FIXME / 伪代码** | 打回重写 |
| 2 | **所有函数必须有单元测试** | 打回重写 |
| 3 | **所有错误必须处理** | 打回重写 |
| 4 | **必须记录日志（含 context）** | 打回重写 |
| 5 | **类型必须完整（TypeScript/Python类型注解）** | 打回重写 |
| 6 | **禁止魔法数字，必须命名常量** | 打回重写 |
| 7 | **API 必须校验输入（validate first）** | 打回重写 |
| 8 | **数据库操作必须有事务** | 打回重写 |
| 9 | **敏感操作必须可审计（who/when/what）** | 打回重写 |
| 10 | **代码必须可回滚（feature flag / 版本兼容）** | 打回重写 |

### 强烈建议（软性规则）

| # | 规则 | 理由 |
|---|------|------|
| 11 | 函数长度 < 30 行 | 可读性 |
| 12 | 圈复杂度 < 10 | 可维护性 |
| 13 | 依赖注入 > new 实例 | 可测试性 |
| 14 | 返回值用 Result/Option 而非 null | 类型安全 |
| 15 | 并发代码必须有超时和熔断 | 稳定性 |

---

## 🛠️ 工作流程

### Step 1：需求分析

```
用户：帮我写一个用户登录接口

AI（内部检查）：
- 是否涉及密码？→ 需要加密 + 安全审计
- 是否涉及会话？→ 需要 JWT / Session 管理
- 是否涉及数据库？→ 需要事务 + 防注入
- 是否需要限流？→ 需要防暴力破解
```

### Step 2：强制 TDD

```
先写测试 → 再写实现 → 重构

红色阶段：测试失败
  └─ 定义接口契约
  └─ 定义错误场景
  └─ 定义边界条件

绿色阶段：测试通过
  └─ 最小实现
  └─ 硬编码返回 OK

重构阶段：优化代码
  └─ 提取函数
  └─ 消除重复
  └─ 添加类型
```

### Step 3：代码审查清单

每行代码必须通过：

```
□ 是否有测试覆盖？
□ 错误路径是否处理？
□ 是否有日志记录？
□ 类型是否完整？
□ 是否有安全漏洞？
□ 是否可回滚？
□ 性能是否可接受？
```

### Step 4：交付物

不是一段代码，而是一个**可部署单元**：

```
feature-login/
├── src/
│   ├── index.ts          # 入口
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   └── auth.dto.ts
├── tests/
│   ├── auth.unit.test.ts
│   ├── auth.integration.test.ts
│   └── auth.e2e.test.ts
├── docs/
│   └── api-contract.md   # API 契约文档
└── README.md             # 部署说明
```

---

## 💡 使用示例

### 示例1：用户登录接口

**用户：** 帮我写一个用户登录接口

**AI：**

1. **分析需求**
   - 输入：用户名/密码
   - 输出：JWT Token / 错误信息
   - 约束：防暴力破解、密码加密、审计日志

2. **先写测试**

```typescript
// tests/auth.unit.test.ts
describe('AuthService.login', () => {
  it('should return JWT for valid credentials', async () => {
    // given
    const username = 'testuser';
    const password = 'correct_password';
    // when
    const result = await authService.login({ username, password });
    // then
    expect(result.isOk()).toBe(true);
    expect(result.value.token).toBeDefined();
  });

  it('should return error for wrong password', async () => {
    const result = await authService.login({ username: 'testuser', password: 'wrong' });
    expect(result.isErr()).toBe(true);
    expect(result.error.code).toBe('INVALID_CREDENTIALS');
  });

  it('should rate limit after 5 failed attempts', async () => {
    // 5次失败
    for (let i = 0; i < 5; i++) {
      await authService.login({ username: 'testuser', password: 'wrong' });
    }
    // 第6次应该被限流
    const result = await authService.login({ username: 'testuser', password: 'wrong' });
    expect(result.error.code).toBe('RATE_LIMITED');
  });
});
```

3. **再写实现**

```typescript
// src/auth.service.ts
import { Result, ok, err } from 'neverthrow';
import { Logger } from './logger';
import { RateLimiter } from './rate-limiter';
import { PasswordHasher } from './password-hasher';
import { JwtIssuer } from './jwt-issuer';
import { AuditLog } from './audit-log';

interface LoginInput {
  username: string;
  password: string;
  ipAddress: string;
  userAgent: string;
}

interface LoginSuccess {
  token: string;
  expiresAt: Date;
}

interface LoginError {
  code: 'INVALID_CREDENTIALS' | 'RATE_LIMITED' | 'USER_LOCKED';
  message: string;
}

const MAX_FAILED_ATTEMPTS = 5;
const RATE_LIMIT_WINDOW_MS = 15 * 60 * 1000; // 15分钟

export class AuthService {
  constructor(
    private readonly userRepo: UserRepository,
    private readonly rateLimiter: RateLimiter,
    private readonly passwordHasher: PasswordHasher,
    private readonly jwtIssuer: JwtIssuer,
    private readonly auditLog: AuditLog,
    private readonly logger: Logger,
  ) {}

  async login(input: LoginInput): Promise<Result<LoginSuccess, LoginError>> {
    this.logger.info('Login attempt', { username: input.username, ip: input.ipAddress });

    // 1. 限流检查
    const rateLimitKey = `login:${input.username}:${input.ipAddress}`;
    const isRateLimited = await this.rateLimiter.isLimited(rateLimitKey, MAX_FAILED_ATTEMPTS, RATE_LIMIT_WINDOW_MS);
    if (isRateLimited) {
      this.auditLog.record('LOGIN_RATE_LIMITED', input);
      return err({ code: 'RATE_LIMITED', message: 'Too many failed attempts. Try again in 15 minutes.' });
    }

    // 2. 查询用户
    const user = await this.userRepo.findByUsername(input.username);
    if (!user) {
      this.auditLog.record('LOGIN_FAILED', input);
      return err({ code: 'INVALID_CREDENTIALS', message: 'Invalid username or password' });
    }

    // 3. 密码校验
    const isPasswordValid = await this.passwordHasher.verify(input.password, user.passwordHash);
    if (!isPasswordValid) {
      await this.rateLimiter.increment(rateLimitKey);
      this.auditLog.record('LOGIN_FAILED', input);
      return err({ code: 'INVALID_CREDENTIALS', message: 'Invalid username or password' });
    }

    // 4. 签发 Token
    const token = await this.jwtIssuer.issue({ userId: user.id, username: user.username });
    this.auditLog.record('LOGIN_SUCCESS', input);
    this.logger.info('Login successful', { userId: user.id, username: user.username });

    return ok({ token, expiresAt: new Date(Date.now() + 24 * 60 * 60 * 1000) });
  }
}
```

4. **交付**
   - ✅ 测试覆盖正常/错误/边界路径
   - ✅ 限流防暴力破解
   - ✅ 审计日志记录所有尝试
   - ✅ 类型完整
   - ✅ 无 TODO
   - ✅ 可回滚（JWT 可独立撤销）

---

## 🆚 与其他开发 Skill 的关系

| Skill | 定位 | 何时使用 |
|-------|------|---------|
| **opinionated-engineer** | 编码纪律 | 写任何生产代码时 |
| **bmad-method** | 项目管理 | 从零做完整产品 |
| **ai-dlc** | 生命周期 | 需要质量门控和阶段管理 |
| **test-driven-development** | 测试方法 | 专注红绿重构循环 |
| **systematic-debugging** | 调试 | 遇到 Bug 时 |

**最佳实践链**：
```
需求 → bmad-method（规划）→ opinionated-engineer（编码标准）
    → test-driven-development（测试）→ systematic-debugging（排查）
```

---

## 🚀 快速开始

```
用户：按工程标准写一个 [功能描述]

AI：
1. 需求分析（识别约束）
2. 先写测试（定义契约）
3. 再写实现（通过测试）
4. 自检清单（10条硬性规则）
5. 交付完整单元（代码+测试+文档）
```

---

> "代码能跑只是起点，代码能上线才是终点。opinionated-engineer 不让 AI 偷懒。"
