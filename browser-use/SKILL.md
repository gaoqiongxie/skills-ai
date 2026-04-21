---
name: "browser-use"
description: >
  浏览器自动化技能：AI 控制浏览器执行网页操作（截图、表单填写、点击、数据抓取等）。
  基于 Playwright/MCP 实现，适用于网页测试、数据采集、表单自动填写、网页截图等场景。
  触发词：浏览器自动化、网页截图、自动填表、抓取网页、Playwright、浏览器操作、网页抓取
---

# 🌐 浏览器自动化

> 让 AI 直接操作你的浏览器，完成网页上的各种任务。

---

## 核心场景

| 场景 | 说明 |
|------|------|
| 📸 网页截图 | 截取整个页面或指定区域 |
| 📝 自动填表 | 自动填写网页表单（登录/注册/调查问卷） |
| 🔍 数据抓取 | 从网页提取结构化数据 |
| 🖱️ 点击操作 | 点击按钮/链接/元素 |
| 🔄 登录操作 | 自动登录网站并保持会话 |
| 📊 批量操作 | 重复性网页操作自动化 |

---

## 工作流程

### Step 1：加载浏览器自动化 Skill

调用 `use_skill("playwright-cli")` 或 `use_skill("agent-browser")` 加载浏览器能力。

### Step 2：描述任务

用自然语言描述你要做什么：

```
"帮我打开这个网页，截图保存"
"登录这个网站，然后把所有订单数据导出来"
"填写这个表单，点击提交"
"把这个页面里所有商品名称和价格抓下来"
```

### Step 3：AI 执行

AI 会：
1. 打开目标网页
2. 分析页面结构
3. 执行对应操作
4. 保存结果或截图

---

## 常用操作示例

### 截图

```python
# 整页截图
page.screenshot(path="screenshot.png", full_page=True)

# 指定元素截图
page.locator("#main-content").screenshot()
```

### 填表

```python
# 填写输入框
page.fill("#username", "my_user")
page.fill("#password", "my_pass")

# 点击提交
page.click("button[type='submit']")

# 等待响应
page.wait_for_response("**/api/**")
```

### 数据抓取

```python
# 提取文本内容
titles = page.locator(".article-title").all_text_contents()

# 提取结构化数据
products = page.locator(".product-card").all([
    lambda card: {
        "name": card.locator(".name").inner_text(),
        "price": card.locator(".price").inner_text()
    }
])
```

### 等待页面加载

```python
# 等待元素出现
page.wait_for_selector("#result", state="visible", timeout=10000)

# 等待网络请求
page.wait_for_response("**/api/search**")
```

---

## 安全注意事项

⚠️ **重要提示：**

| ✅ 可以做 | ❌ 不要做 |
|---------|---------|
| 测试自己的网页 | 自动化登录他人账号 |
| 抓取公开网页数据 | 爬取需要登录的隐私数据 |
| 截图保存分析 | 批量注册账号 |
| 表单自动填写 | 绕过验证码牟利 |
| 自动化测试 | 攻击网站或绕过人机验证 |

---

## 使用提示

- 触发：`"帮我截图"` / `"打开这个网页"` / `"自动填表"`
- 可以指定浏览器：Chromium（默认）/ Firefox / WebKit
- 大页面截图建议加 `full_page=True`
- 有反爬的网站可能需要额外处理（UA/代理/延迟）

---

## 一句话原则

> 浏览器是互联网的入口，自动化就是让 AI 替你上网做事。
> 用来提效，不用来作恶。
