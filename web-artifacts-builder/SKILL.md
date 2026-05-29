---
name: "web-artifacts-builder"
description: "复杂Web构件构建器：用React+Tailwind CSS+shadcn/ui构建多组件、带状态管理和路由的交互式Web应用。当用户说'做个复杂网页'、'带筛选的数据看板'、'交互式配置页面'、'React组件页面'、'多页面artifact'、'shadcn界面'时触发。核心特点：组件化架构、状态管理、Tailwind样式、shadcn/ui组件库、路由切换。"
---

> **来源**: 改编自 Anthropic 官方 skill（github.com/anthropics/skills/web-artifacts-builder）
>
> **发布时间**: 2026-05-29
>
> **理念**: "单文件 HTML 做原型，React+shadcn 做产品。"

# 🏗️ Web Artifacts Builder — 复杂 Web 构件构建器

用 **React + Tailwind CSS + shadcn/ui** 构建生产级复杂交互界面，支持多组件、状态管理、路由切换。

---

## 🎯 和简单 HTML 的区别

| 维度 | 简单 HTML（html-ppt-skill） | Web Artifacts Builder |
|------|---------------------------|----------------------|
| **技术栈** | 原生 HTML + CSS + JS | React + Tailwind + shadcn/ui |
| **组件化** | ❌ 单文件 | ✅ 多组件拆分 |
| **状态管理** | ❌ 无 | ✅ useState / useReducer |
| **路由** | ❌ 单页面 | ✅ 多页面/Tab 切换 |
| **UI 组件库** | ❌ 手写 | ✅ shadcn/ui（Button/Card/Table/Dialog...） |
| **适用场景** | 原型、演示文稿、静态页面 | 数据看板、管理后台、配置页面 |

---

## 🛠️ 技术栈规范

### 核心依赖

```
React 18+      # 组件框架
Tailwind CSS   # 原子化样式
shadcn/ui      # 无头 UI 组件库
Lucide React   # 图标库
```

### shadcn/ui 常用组件速查

| 组件 | 用途 | 引入方式 |
|------|------|---------|
| `Button` | 按钮 | `import { Button } from "@/components/ui/button"` |
| `Card` | 卡片容器 | `import { Card, CardHeader, CardContent } from "@/components/ui/card"` |
| `Table` | 数据表格 | `import { Table, TableHeader, TableRow, TableCell } from "@/components/ui/table"` |
| `Dialog` | 弹窗/模态框 | `import { Dialog, DialogContent, DialogTrigger } from "@/components/ui/dialog"` |
| `Input` | 输入框 | `import { Input } from "@/components/ui/input"` |
| `Select` | 下拉选择 | `import { Select, SelectItem } from "@/components/ui/select"` |
| `Tabs` | 标签页切换 | `import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs"` |
| `Badge` | 状态标签 | `import { Badge } from "@/components/ui/badge"` |
| `Skeleton` | 加载骨架屏 | `import { Skeleton } from "@/components/ui/skeleton"` |

### Tailwind 常用类

```
布局: flex, grid, grid-cols-3, gap-4, p-4, m-2
响应式: md:grid-cols-2, lg:grid-cols-4
颜色: bg-slate-50, text-red-500, border-gray-200
阴影: shadow-sm, shadow-md, rounded-lg
尺寸: w-full, h-screen, max-w-4xl, min-h-[200px]
```

---

## 📁 项目结构模板

```
my-web-app/
├── src/
│   ├── components/
│   │   ├── ui/           # shadcn/ui 组件（自动生成）
│   │   ├── Header.tsx    # 顶部导航
│   │   ├── Sidebar.tsx   # 侧边栏
│   │   └── DataTable.tsx # 数据表格组件
│   ├── pages/
│   │   ├── Dashboard.tsx # 首页看板
│   │   ├── Settings.tsx  # 配置页
│   │   └── Profile.tsx   # 详情页
│   ├── hooks/
│   │   └── useData.ts    # 自定义 Hook
│   ├── lib/
│   │   └── utils.ts      # 工具函数
│   ├── App.tsx           # 根组件+路由
│   └── main.tsx          # 入口
├── public/
├── index.html
├── package.json
├── tailwind.config.js
└── tsconfig.json
```

---

## 💡 使用示例

### 示例 1：数据看板 Dashboard

**用户**：帮我做一个销售数据看板，带筛选和图表

**AI 输出**：

```tsx
// App.tsx
import { useState } from "react";
import { Card, CardHeader, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Select, SelectItem } from "@/components/ui/select";
import { Badge } from "@/components/ui/badge";
import { LineChart, BarChart } from "@/components/charts"; // 假设

export default function Dashboard() {
  const [period, setPeriod] = useState("month");
  const [region, setRegion] = useState("all");
  
  const data = useSalesData({ period, region });
  
  return (
    <div className="min-h-screen bg-slate-50 p-6">
      <div className="max-w-7xl mx-auto">
        {/* 筛选栏 */}
        <div className="flex gap-4 mb-6">
          <Select value={period} onValueChange={setPeriod}>
            <SelectItem value="week">本周</SelectItem>
            <SelectItem value="month">本月</SelectItem>
            <SelectItem value="year">本年</SelectItem>
          </Select>
          <Select value={region} onValueChange={setRegion}>
            <SelectItem value="all">全部区域</SelectItem>
            <SelectItem value="north">华北</SelectItem>
            <SelectItem value="south">华南</SelectItem>
          </Select>
          <Button onClick={() => exportData(data)}>导出报表</Button>
        </div>
        
        {/* KPI 卡片 */}
        <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-6">
          <KpiCard title="总销售额" value={data.total} trend="+12%" />
          <KpiCard title="订单数" value={data.orders} trend="+5%" />
          <KpiCard title="客单价" value={data.avgPrice} trend="-2%" />
          <KpiCard title="转化率" value={data.rate} trend="+8%" />
        </div>
        
        {/* 图表区 */}
        <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
          <Card>
            <CardHeader>销售趋势</CardHeader>
            <CardContent>
              <LineChart data={data.trend} />
            </CardContent>
          </Card>
          <Card>
            <CardHeader>品类占比</CardHeader>
            <CardContent>
              <BarChart data={data.category} />
            </CardContent>
          </Card>
        </div>
      </div>
    </div>
  );
}
```

---

### 示例 2：多 Tab 配置页面

**用户**：做一个用户配置页面，分基本信息、安全设置、通知偏好三个 Tab

**AI 输出**：

```tsx
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Switch } from "@/components/ui/switch";

export default function SettingsPage() {
  return (
    <div className="max-w-3xl mx-auto p-6">
      <h1 className="text-2xl font-bold mb-6">系统配置</h1>
      
      <Tabs defaultValue="basic">
        <TabsList className="mb-4">
          <TabsTrigger value="basic">基本信息</TabsTrigger>
          <TabsTrigger value="security">安全设置</TabsTrigger>
          <TabsTrigger value="notification">通知偏好</TabsTrigger>
        </TabsList>
        
        <TabsContent value="basic">
          <Card>
            <CardContent className="space-y-4 pt-4">
              <div>
                <label className="text-sm font-medium">用户名</label>
                <Input placeholder="请输入用户名" />
              </div>
              <div>
                <label className="text-sm font-medium">邮箱</label>
                <Input type="email" placeholder="your@email.com" />
              </div>
              <Button>保存</Button>
            </CardContent>
          </Card>
        </TabsContent>
        
        <TabsContent value="security">
          <Card>
            <CardContent className="space-y-4 pt-4">
              <div className="flex items-center justify-between">
                <span>两步验证</span>
                <Switch />
              </div>
              <div className="flex items-center justify-between">
                <span>登录通知</span>
                <Switch defaultChecked />
              </div>
            </CardContent>
          </Card>
        </TabsContent>
        
        <TabsContent value="notification">
          <Card>
            <CardContent className="space-y-4 pt-4">
              <div className="flex items-center justify-between">
                <span>邮件通知</span>
                <Switch defaultChecked />
              </div>
              <div className="flex items-center justify-between">
                <span>短信通知</span>
                <Switch />
              </div>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>
    </div>
  );
}
```

---

### 示例 3：Dialog 弹窗 + 表单验证

```tsx
import { Dialog, DialogContent, DialogHeader, DialogTrigger } from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

export function CreateOrderDialog() {
  const [open, setOpen] = useState(false);
  
  return (
    <Dialog open={open} onOpenChange={setOpen}>
      <DialogTrigger asChild>
        <Button>新建订单</Button>
      </DialogTrigger>
      <DialogContent className="sm:max-w-[500px]">
        <DialogHeader>新建订单</DialogHeader>
        <div className="space-y-4 py-4">
          <Input placeholder="客户名称" />
          <Input placeholder="订单金额" type="number" />
          <Select>
            <SelectItem value="pending">待处理</SelectItem>
            <SelectItem value="paid">已付款</SelectItem>
          </Select>
        </div>
        <div className="flex justify-end gap-2">
          <Button variant="outline" onClick={() => setOpen(false)}>取消</Button>
          <Button onClick={handleSubmit}>确认</Button>
        </div>
      </DialogContent>
    </Dialog>
  );
}
```

---

## 🚀 快速入口

```
"帮我做个复杂网页" → React + Tailwind + shadcn 多组件架构
"带筛选的数据看板" → Dashboard + KPI卡片 + 图表 + 筛选栏
"交互式配置页面" → Tabs切换 + Form表单 + 状态管理
"多页面artifact" → 路由/Tab切换 + 页面组件拆分
"React组件页面" → 组件化架构 + hooks + props传递
"shadcn界面" → shadcn/ui组件库 + Tailwind样式系统
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 场景对比 |
|-------|------|---------|
| **prd-to-demo** | 互补 | `prd-to-demo` 生成快速原型（单文件HTML），`web-artifacts-builder` 生成生产级复杂界面 |
| **screenshot-to-prototype** | 互补 | 截图还原用 `screenshot-to-prototype`（快速），复杂交互用本 Skill |
| **html-ppt-skill** | 互补 | `html-ppt` 是演示文稿，本 Skill 是 Web 应用 |
| **frontend-design** | 前置 | `frontend-design` 定视觉方向，本 Skill 执行代码构建 |
| **frontend-code-review** | 后置 | 本 Skill 编码完成后，用 `frontend-code-review` 审查质量 |

**最佳实践链**：
```
需求 → prd-to-demo（快速原型验证）→ web-artifacts-builder（生产级实现）
  → frontend-code-review（代码审查）→ quality-gate（质量检查）
```

---

> "单文件 HTML 是草图，React + shadcn 是建筑。两者都有价值，看你要什么。"
