---
name: "testing-patterns"
description: "全栈测试模式：覆盖单元测试、React组件测试、集成测试、E2E测试和Mock策略。当用户说'怎么写测试'、'测试最佳实践'、'React测试'、'E2E测试'、'Mock数据'、'测试覆盖率'、'测试模式'、'单元测试用例'时触发。核心特点：测试金字塔分层、框架无关模式、常见反模式识别、测试数据工厂。"
---

> **来源**: Anthropic Skills PR #723
>
> **发布时间**: 2026-05
>
> **理念**: "测试不是开发的附属品，是代码质量的保险单。"

# 🧪 Testing Patterns — 全栈测试模式

从单元测试到 E2E，覆盖全栈的测试模式与最佳实践。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **测试金字塔** | 按 70% 单元 / 20% 集成 / 10% E2E 分层指导 |
| **框架适配** | Jest/Vitest/Mocha + React Testing Library + Cypress/Playwright |
| **Mock 策略** | 何时 Mock、何时集成，避免过度/不足 Mock |
| **测试数据工厂** | 可复用的测试数据生成模式 |
| **快照测试** | 合理使用 UI 快照，避免脆弱测试 |
| **反模式识别** | 识别常见测试坏味道并给出修复方案 |

---

## 📐 测试金字塔

```
        ┌─────────┐
        │   E2E   │  ← 10%  端到端测试（用户旅程）
        │ Cypress │      慢、贵、覆盖面广
       ├─────────┤
       │ 集成测试 │  ← 20%  API/组件集成
       │  API层  │      中速、验证协作
      ├─────────┤
      │  单元测试  │  ← 70%  函数/组件逻辑
      │ Jest/Vitest│      快、便宜、隔离
      └─────────┘
```

---

## 🧩 测试模式速查

### 单元测试模式

| 场景 | 模式 | 示例 |
|------|------|------|
| 纯函数 | 输入→输出断言 | `expect(add(1,2)).toBe(3)` |
| 异步函数 | async/await + 断言 | `await expect(fetchUser()).resolves.toEqual({...})` |
| 异常处理 | throws 断言 | `expect(() => divide(1,0)).toThrow()` |
| 边界条件 | 等价类划分 | 空值、最大值、类型错误 |

### React 组件测试模式

| 场景 | 模式 | 工具 |
|------|------|------|
| 渲染验证 | render + screen 查询 | React Testing Library |
| 用户交互 | fireEvent / userEvent | `@testing-library/user-event` |
| 状态变化 | 等待异步更新 | `waitFor` + `findBy*` |
| Props 验证 | 不同 props 组合渲染 | 数据驱动测试 |
| 路由测试 | MemoryRouter 包裹 | `react-router-dom/testing` |

### Mock 策略决策树

```
是否需要 Mock?
    │
    ├─ 外部 HTTP 请求 → ✅ Mock（避免网络依赖）
    ├─ 数据库查询    → ✅ Mock / 内存数据库
    ├─ 当前模块依赖  → ❌ 不 Mock（真实调用）
    ├─ 第三方库      → ⚠️ 视情况（稳定库不 Mock）
    └─ 时间/随机数   → ✅ Mock（确定性测试）
```

### E2E 测试模式

| 模式 | 说明 |
|------|------|
| **Page Object** | 封装页面元素选择器，隔离 UI 变更影响 |
| **Given-When-Then** | BDD 风格描述用户旅程 |
| **Fixture 数据** | 预置测试数据，保证环境一致性 |
| **Visual Regression** | 截图对比，捕获 UI 意外变更 |

---

## 🚀 使用方式

### 方式一：请求测试方案

```
帮我写这个函数的单元测试
function calculateDiscount(price, userType) { ... }
```

### 方式二：审查现有测试

```
审查这段测试代码有什么问题
```

### 方式三：测试架构咨询

```
我们的项目应该用什么测试策略？
技术栈：React + Node.js + PostgreSQL
```

---

## 💡 最佳实践

### DO
- ✅ 每个 bugfix 先写失败的测试（回归保护）
- ✅ 测试描述写清楚"做什么"而非"怎么做"
- ✅ 使用工厂函数生成测试数据，避免硬编码
- ✅ 保持测试独立，不依赖执行顺序

### DON'T
- ❌ 测试私有方法（测试行为，非实现）
- ❌ 过度 Mock（失去测试价值）
- ❌ 在测试中写条件逻辑（测试应确定性）
- ❌ 忽略测试运行速度（慢测试 = 少运行）

---

## 🔗 与其他 Skill 的关系

| | testing-patterns | test-driven-development | systematic-debugging |
|---|---|---|---|
| **侧重** | 怎么写好测试 | 什么时候写测试 | 发现 Bug 后验证 |
| **最佳组合** | TDD 驱动开发 → testing-patterns 写高质量用例 → debugging 时补充回归测试 |

---

> "没有测试的代码是遗留代码——不管它昨天还是去年写的。"
