---
name: "frontend-design"
description: "前端设计规范技能：拒绝'AI slop'式平庸UI，强制做出大胆、有辨识度的设计决策。适用于React/Tailwind/原生HTML项目。当用户说'帮我设计一个页面'、'做个前端界面'、'设计一个UI'、'帮我写个网页'、'设计个组件'、'帮我设计'、'前端开发'、'UI设计'时触发此Skill。核心特点：禁止过度使用的字体（如Inter/Poppins）、强制 distinctive 视觉方向（粗野主义/编辑风/复古未来主义等）、强调排版层级、色彩系统和微动效。"
---

> **来源**: Anthropic 官方 Skills (anthropics/skills) — 100K+ weekly installs
>
> **发布时间**: 2026-04-29
>
> **理念**: "AI slop 是设计的天敌。Generic 就是垃圾。"

# 🎨 前端设计规范 Skill

拒绝平庸，做出有辨识度的前端设计。不是又一个 Bootstrap 风，而是让人记住的界面。

---

## 🚫 禁止清单（AI Slop 特征）

| 禁止项 | 原因 | 替代方案 |
|--------|------|---------|
| Inter / Poppins / Roboto | 被用烂了，毫无辨识度 | 选择有性格的字族 |
| 纯白背景 + 灰边框卡片 | 默认即平庸 | 用色块、纹理、负空间区分 |
| 圆角 8px 按钮 | 模板味太重 | 根据风格选 0px（粗野）/ 999px（活泼）/ 4px（克制） |
| 渐变色背景 | 2018 年的审美 | 纯色 + 纹理 / 双色调 / 插画 |
| 居中 Hero + 3栏特性 | 千篇一律 | 不对称布局 / 编辑式排版 |
| 无意义的图标 | 装饰性垃圾 | 要么不用，要么用有风格的插画/手绘 |

---

## 🎯 6 大视觉方向

每次设计前，先选定一个主方向：

| 方向 | 特征 | 适用场景 |
|------|------|---------|
| **Brutalist 粗野主义** | 大字号、无修饰、高对比、Helvetica/系统字体 | 创意机构、个人站、作品集 |
| **Editorial 编辑风** | 衬线标题、大量留白、图片主导、杂志感 | 内容平台、博客、品牌站 |
| **Retro-Futurism 复古未来** | 像素字体、霓虹色、CRT 效果、网格线 | 游戏、科技产品、活动页 |
| **Organic 有机自然** | 圆润形态、大地色、手绘插画、柔和阴影 | 健康、生活方式、教育 |
| **Neo-Minimal 新极简** | 极少元素、超大留白、精选用色、克制动画 | SaaS、工具产品、高端服务 |
| **Maximalist 极繁主义** | 高饱和、多层叠、动画密集、打破网格 | 创意项目、活动、品牌表达 |

---

## 🧩 设计决策框架

每次生成设计时，按以下顺序做决策：

### Step 1：选定视觉方向
从上面 6 个方向中选一个，或混合 2 个。

### Step 2：字体搭配
| 层级 | 策略 |
|------|------|
| Display / Hero | 有性格的字族（衬线/等宽/手写/像素） |
| Body / 正文 | 可读性优先，但不要默认用 Inter |
| 中文场景 | 思源宋体/思源黑体/站酷系列/得意黑 |

### Step 3：色彩系统
- **主色**：1-2 个，足够鲜明
- **辅色**：1 个 accent，用于 CTA 和重点
- **中性色**：不要只用 #333 和 #999，带一点色相
- **背景色**：考虑深色/浅色/有纹理

### Step 4：布局策略
- 打破默认网格
- 尝试不对称
- 图片和文字的关系：叠压 / 穿插 / 出血

### Step 5：动效哲学
- 每个动效都要有目的
- 入场：从下方淡入 + 轻微位移
- 交互：Hover 不是变颜色，而是有物理感
- 滚动：视差、pin、元素渐显

---

## 💻 代码风格（Tailwind / React）

```jsx
// ❌ 不要这样
<div className="bg-white rounded-lg shadow-md p-6">
  <h2 className="text-2xl font-bold text-gray-800">标题</h2>
</div>

// ✅ 要这样（Brutalist 示例）
<div className="bg-black p-8 border-b-4 border-yellow-400">
  <h2 className="text-5xl font-black text-white uppercase tracking-tighter">
    标题
  </h2>
</div>

// ✅ 要这样（Editorial 示例）
<div className="bg-stone-50 px-12 py-20">
  <h2 className="text-6xl font-serif text-stone-900 leading-none">
    标题
  </h2>
</div>
```

---

## 🎨 使用示例

### 示例1：粗野主义 landing page
```
用户：帮我设计一个设计工作室的官网

助手：→ 方向：Brutalist 粗野主义
     字体：系统字体 + 超大字号
     色彩：黑底白字 + 荧光绿 accent
     布局：全出血图片 + 文字叠压 + 无圆角
     动效：滚动时文字横向移动
```

### 示例2：编辑风博客
```
用户：帮我做一个技术博客首页

助手：→ 方向：Editorial 编辑风
     字体：思源宋体标题 + 系统黑体正文
     色彩：米白背景 + 深褐文字 + 赭红 accent
     布局：杂志式网格、文章卡片大小不一
     动效：图片 hover 轻微放大 + 标题下划线展开
```

### 示例3：复古未来科技感
```
用户：做一个 AI 工具产品页

助手：→ 方向：Retro-Futurism
     字体：像素字体标题 + 等宽字体正文
     色彩：深蓝底 + 霓虹青/洋红
     布局：终端式分区、网格背景线
     动效：打字机效果、扫描线、闪烁光标
```

---

## 📐 组件设计原则

| 组件 | 原则 |
|------|------|
| **按钮** | 不要默认圆角，根据风格选形状。Hover 有物理反馈（位移/缩放） |
| **卡片** | 不要统一 padding。尝试出血、叠压、不规则间距 |
| **导航** | 隐藏或极简。全屏菜单 / 侧边栏 / 底部栏 |
| **表单** | 大输入框、粗边框、清晰标签。不要用 placeholder 代替 label |
| **图片** | 考虑黑白/双色调/遮罩。不要直接丢一张图上去 |

---

## 🆚 与其他设计 Skill 的关系

| | frontend-design | huashu-design | diagram-design |
|--|-----------------|---------------|----------------|
| 用途 | 前端界面设计 | HTML 原生设计作品 | 图表/架构图 |
| 输出 | React/Tailwind/JSX | 纯 HTML + CSS | HTML + SVG |
| 核心 | 拒绝平庸，大胆决策 | 20种设计哲学全覆盖 | 13种专业图表 |
| 触发 | 前端开发、UI设计 | 做网页、做设计 | 画架构图、流程图 |

**最佳实践**：复杂数据可视化用 `diagram-design`，品牌/创意网页用 `huashu-design`，前端组件/产品界面用 `frontend-design`。

---

> "Good design is obvious. Great design is transparent. But distinctive design is remembered."
