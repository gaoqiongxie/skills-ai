---
name: "webapp-testing"
description: "Web应用自动化测试：Playwright侦察→行动工作流。当用户说'测试这个网页'、'写E2E测试'、'测一下前端'、'Playwright测试'、'自动化测试网页'、'UI测试'、'端到端测试'时触发。核心特点：先侦察DOM结构再生成测试，支持表单验证/导航流程/API Mock/截图对比/性能指标，输出可运行的Playwright测试代码。"
---

> **来源**: 社区实践（Anthropic Skills Marketplace 2026 实用技能）
>
> **发布时间**: 2026-05-14
>
> **理念**: "先侦察，再行动。不知道页面结构就写测试，等于蒙眼开车。"

# 🧪 WebApp Testing — Web 应用自动化测试

用 Playwright 侦察 → 行动工作流，为网页生成可运行的端到端测试。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **页面侦察** | 分析目标网页的 DOM 结构、交互元素、路由 |
| **测试生成** | 根据侦察结果生成 Playwright 测试代码 |
| **表单测试** | 自动识别表单字段，生成填写+提交+校验测试 |
| **导航测试** | 页面跳转、面包屑、返回、深链接 |
| **API Mock** | 拦截 API 请求，Mock 响应数据 |
| **截图对比** | 视觉回归测试，对比基线和当前截图 |
| **性能指标** | 测量 LCP、FID、CLS 等 Core Web Vitals |
| **无障碍测试** | 检查 ARIA 标签、键盘导航、颜色对比度 |

---

## 🏗️ 侦察 → 行动 工作流

### 第一步：侦察 (Reconnaissance)

访问目标页面，收集信息：

```
侦察清单：
□ 页面标题和 URL
□ 所有可交互元素（按钮/链接/输入框）
□ 表单结构（字段名/类型/校验规则）
□ 导航结构（菜单/面包屑/页脚）
□ API 调用（XHR/Fetch 请求）
□ 关键数据展示（表格/列表/卡片）
□ 加载状态（骨架屏/Loading/空状态）
□ 错误状态（404/500/空数据）
```

### 第二步：规划 (Planning)

根据侦察结果，规划测试策略：

```
测试策略：
1. 冒烟测试（核心流程通不通）
2. 功能测试（每个交互点）
3. 边界测试（极端输入/空数据）
4. 错误测试（网络异常/权限不足）
5. 视觉测试（响应式/截图对比）
```

### 第三步：生成 (Generation)

输出可运行的 Playwright 测试代码：

```typescript
// 示例结构
import { test, expect } from '@playwright/test';

test.describe('登录流程', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/login');
  });

  test('正常登录', async ({ page }) => {
    // 侦察到的字段
    await page.fill('[data-testid="username"]', 'testuser');
    await page.fill('[data-testid="password"]', 'correct_password');
    await page.click('button[type="submit"]');
    
    // 断言
    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('[data-testid="welcome"]')).toContainText('欢迎');
  });

  test('密码错误', async ({ page }) => {
    await page.fill('[data-testid="username"]', 'testuser');
    await page.fill('[data-testid="password"]', 'wrong_password');
    await page.click('button[type="submit"]');
    
    await expect(page.locator('.error-message')).toContainText('密码错误');
    await expect(page).toHaveURL('/login'); // 停留在登录页
  });
});
```

### 第四步：验证 (Validation)

运行测试，确保通过：

```bash
npx playwright test
```

---

## 🧩 测试类型模板

### 模板1：表单测试

```typescript
test('表单提交与校验', async ({ page }) => {
  // 1. 访问页面
  await page.goto('/contact');
  
  // 2. 留空提交 → 应显示必填错误
  await page.click('button[type="submit"]');
  await expect(page.locator('[data-testid="name-error"]')).toBeVisible();
  await expect(page.locator('[data-testid="email-error"]')).toBeVisible();
  
  // 3. 填无效邮箱 → 应显示格式错误
  await page.fill('[name="email"]', 'invalid-email');
  await page.click('button[type="submit"]');
  await expect(page.locator('[data-testid="email-error"]')).toContainText('邮箱格式不正确');
  
  // 4. 正确填写 → 提交成功
  await page.fill('[name="name"]', '张三');
  await page.fill('[name="email"]', 'zhangsan@example.com');
  await page.fill('[name="message"]', '这是一条测试消息');
  
  // Mock API 响应
  await page.route('**/api/contact', route => {
    route.fulfill({ status: 200, body: JSON.stringify({ success: true }) });
  });
  
  await page.click('button[type="submit"]');
  await expect(page.locator('.success-message')).toContainText('提交成功');
});
```

### 模板2：导航测试

```typescript
test('主导航流程', async ({ page }) => {
  await page.goto('/');
  
  // 点击导航项
  await page.click('nav >> text=产品');
  await expect(page).toHaveURL('/products');
  await expect(page.locator('h1')).toContainText('产品中心');
  
  // 点击子菜单
  await page.click('text=企业版');
  await expect(page).toHaveURL('/products/enterprise');
  
  // 面包屑返回
  await page.click('.breadcrumb >> text=产品中心');
  await expect(page).toHaveURL('/products');
});
```

### 模板3：表格测试

```typescript
test('表格分页与排序', async ({ page }) => {
  await page.goto('/orders');
  
  // Mock 列表数据
  await page.route('**/api/orders*', route => {
    route.fulfill({ 
      status: 200, 
      body: JSON.stringify({
        data: Array.from({ length: 25 }, (_, i) => ({
          id: i + 1,
          amount: (i + 1) * 100,
          status: i % 2 === 0 ? 'completed' : 'pending'
        })),
        total: 25
      })
    });
  });
  
  // 验证第一页数据
  await expect(page.locator('tbody tr')).toHaveCount(10);
  
  // 点击排序
  await page.click('th >> text=金额');
  const firstAmount = await page.locator('tbody tr:first-child td:nth-child(2)').textContent();
  expect(firstAmount).toContain('2500'); // 最大金额
  
  // 分页
  await page.click('text=下一页');
  await expect(page.locator('tbody tr')).toHaveCount(10);
  
  await page.click('text=下一页');
  await expect(page.locator('tbody tr')).toHaveCount(5); // 最后一页
});
```

### 模板4：截图对比（视觉回归）

```typescript
test('首页视觉回归', async ({ page }) => {
  await page.goto('/');
  await page.waitForLoadState('networkidle');
  
  // 全页截图对比
  expect(await page.screenshot({ fullPage: true })).toMatchSnapshot('homepage.png');
  
  // 特定组件截图
  expect(await page.locator('.hero-section').screenshot()).toMatchSnapshot('hero.png');
});
```

### 模板5：性能测试

```typescript
test('首页性能指标', async ({ page }) => {
  await page.goto('/');
  
  // 收集 Performance Timing
  const timing = await page.evaluate(() => {
    const t = performance.timing;
    return {
      domContentLoaded: t.domContentLoadedEventEnd - t.navigationStart,
      loadComplete: t.loadEventEnd - t.navigationStart,
    };
  });
  
  expect(timing.domContentLoaded).toBeLessThan(2000);
  expect(timing.loadComplete).toBeLessThan(3000);
  
  // Core Web Vitals (如果可用)
  const lcp = await page.evaluate(() => {
    return new Promise((resolve) => {
      new PerformanceObserver((list) => {
        const entries = list.getEntries();
        resolve(entries[entries.length - 1]?.startTime);
      }).observe({ entryTypes: ['largest-contentful-paint'] });
    });
  });
  
  expect(lcp).toBeLessThan(2500); // LCP < 2.5s
});
```

---

## 💡 使用示例

### 示例1：测试电商购买流程

```
用户：帮我写个测试，测一下从首页到下单的完整流程

AI：
1. 侦察目标页面（用户提供URL）
2. 识别关键路径：首页 → 商品列表 → 商品详情 → 购物车 → 结算 → 支付 → 成功页
3. 生成测试代码：

```typescript
test('完整购买流程', async ({ page }) => {
  // 首页
  await page.goto('https://example-shop.com');
  await expect(page.locator('.banner')).toBeVisible();
  
  // 点击商品
  await page.click('.product-card:first-child');
  await expect(page).toHaveURL(/\/product\//);
  
  // 选择规格
  await page.click('text=黑色');
  await page.click('text=L');
  
  // 加入购物车
  await page.click('text=加入购物车');
  await expect(page.locator('.toast')).toContainText('已添加');
  
  // 去购物车
  await page.click('.cart-icon');
  await expect(page).toHaveURL('/cart');
  await expect(page.locator('.cart-item')).toHaveCount(1);
  
  // 结算
  await page.click('text=去结算');
  await page.fill('[name="address"]', '测试地址');
  await page.fill('[name="phone"]', '13800138000');
  
  // Mock 支付
  await page.route('**/api/payment', route => {
    route.fulfill({ status: 200, body: JSON.stringify({ orderId: 'TEST-001' }) });
  });
  
  await page.click('text=提交订单');
  
  // 验证成功页
  await expect(page).toHaveURL(/\/order-success/);
  await expect(page.locator('.order-id')).toContainText('TEST-001');
});
```

4. 输出测试文件 + 运行说明
```

---

### 示例2：测试管理后台表格

```
用户：我们后台有个用户管理表格，帮我写测试

AI：
1. 侦察表格结构：搜索/筛选/分页/批量操作
2. 生成测试：
   - 搜索过滤
   - 列排序
   - 分页跳转
   - 批量删除
   - 行内编辑
```

---

## 🆚 与其他测试 Skill 的关系

| Skill | 定位 | 何时使用 |
|-------|------|---------|
| **webapp-testing** | E2E 网页测试 | 测试前端页面交互 |
| **testing-patterns** | 全栈测试模式 | 规划整体测试策略 |
| **test-driven-development** | TDD 方法论 | 编码前先写测试 |
| **browser-use** | 浏览器自动化 | 数据抓取/填表 |

**最佳实践链**：
```
开发前：testing-patterns（规划测试策略）
  → test-driven-development（单元测试）
  → webapp-testing（E2E 测试）
```

---

## 🚀 快速开始

```
用户：测试这个网页 [URL]

AI：
1. 侦察页面结构（DOM/交互/API）
2. 规划测试策略（冒烟/功能/边界/错误）
3. 生成 Playwright 测试代码
4. 输出运行命令：npx playwright test
```

---

> "测试不是写完就完，是跑了才算。webapp-testing 让你从侦察到运行，一步到位。"
