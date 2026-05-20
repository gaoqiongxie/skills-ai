---
name: "frontend-code-review"
description: "前端代码结构化审查：React/TS/TSX 安全重构建议，性能优化，可访问性检查。当用户说'审查这段代码'、'前端代码 review'、'React代码有问题吗'、'这段TSX怎么样'、'优化这个组件'、'代码质量检查'时触发。核心特点：结构化检查清单（性能/可维护性/可访问性/类型安全）、安全重构建议（不破坏现有功能）、重渲染检测、组合优化、与frontend-design互补。"
---

> **来源**: 社区热门（Effeilo/claude-code-frontend-skills，Anthropic Marketplace 2026）
>
> **发布时间**: 2026-05-20
>
> **理念**: "Code Review 不是找茬，是让代码活得更久。"

# 🔍 Frontend Code Review — 前端代码结构化审查

React / TypeScript / TSX 代码的系统性审查，输出可执行的重构建议。

---

## 🎯 审查维度

```
Frontend Code Review
├── ⚡ 性能 (Performance)
│   ├── 不必要的重渲染
│   ├── Memoization 缺失
│   ├── 懒加载机会
│   └── Bundle 体积
├── 🧩 可维护性 (Maintainability)
│   ├── 组件职责单一
│   ├── Props 复杂度
│   ├── 状态管理
│   └── 重复逻辑
├── ♿ 可访问性 (Accessibility)
│   ├── ARIA 标签
│   ├── 键盘导航
│   ├── 颜色对比度
│   └── 焦点管理
├── 🔒 类型安全 (Type Safety)
│   ├── any 类型滥用
│   ├── 可选链使用
│   ├── 泛型完整性
│   └── 事件类型
└── 🎨 代码规范 (Style)
    ├── 命名规范
    ├── 文件组织
    ├── 注释完整性
    └── 导入排序
```

---

## 🛠️ 审查流程

### Step 1: 静态扫描

```
扫描清单：
□ 组件是否超过 200 行？（建议拆分）
□ Props 是否超过 7 个？（建议组合或拆分）
□ 是否有内联样式？（建议提取到 CSS 模块）
□ 是否有 console.log？（生产代码应移除）
□ 是否有死代码？（未使用的导入/变量/函数）
□ 是否有魔法数字？（建议命名常量）
```

### Step 2: 性能分析

```
检查项：
□ 子组件是否不必要的重渲染？（useMemo/useCallback）
□ 列表是否使用 key？（key 是否稳定）
□ 大列表是否虚拟化？（react-window）
□ 图片是否懒加载？（loading="lazy"）
□ 是否有昂贵的计算在 render 中？（useMemo）
□ 是否有循环依赖？（import 循环）
```

### Step 3: 可访问性检查

```
检查项：
□ 图片是否有 alt？
□ 表单字段是否有 label？
□ 按钮是否是真正的 button？（不是 div 模拟）
□ 颜色对比度是否 ≥ 4.5:1？
□ 是否有键盘可操作的焦点？
□ 动态内容是否有 aria-live？
```

### Step 4: 生成报告

```
审查报告结构：
1. 总体评分（1-10）
2. 🔴 阻塞项（必须修复）
3. 🟡 警告项（建议修复）
4. 🟢 建议项（可选优化）
5. 重构方案（Before / After 对比）
```

---

## 💡 审查示例

### 示例1：组件重渲染问题

**输入代码**：
```tsx
function ProductList({ products, onAddToCart }) {
  return (
    <div>
      {products.map(product => (
        <ProductCard
          key={product.id}
          product={product}
          onAddToCart={onAddToCart}
        />
      ))}
    </div>
  );
}

function ProductCard({ product, onAddToCart }) {
  const [isHovered, setIsHovered] = useState(false);

  return (
    <div
      onMouseEnter={() => setIsHovered(true)}
      onMouseLeave={() => setIsHovered(false)}
    >
      <img src={product.image} />
      <h3>{product.name}</h3>
      <button onClick={() => onAddToCart(product.id)}>
        加入购物车
      </button>
    </div>
  );
}
```

**审查报告**：

```
总体评分: 6.5 / 10

🔴 阻塞项:
1. ProductCard 缺少 key 稳定性检查
   如果 product.id 可能重复，会导致渲染异常
   建议: 确保 id 唯一，或使用 index 作为后备

🟡 警告项:
2. ProductCard 组件每次父组件渲染都会重新创建
   ProductList 重新渲染时，所有 ProductCard 都会重渲染
   建议: 使用 React.memo 包裹 ProductCard

   Before:
   function ProductCard({ product, onAddToCart }) { ... }

   After:
   const ProductCard = memo(function ProductCard({ product, onAddToCart }) {
     ...
   });

3. onAddToCart 回调引用不稳定
   如果父组件的 onAddToCart 没有用 useCallback，会导致 memo 失效
   建议: 确保 onAddToCart 使用 useCallback

4. 图片缺少 alt 属性
   建议: <img src={product.image} alt={product.name} />

🟢 建议项:
5. 内联事件处理可以提取
6. 缺少 loading 状态处理
```

### 示例2：类型安全问题

**输入代码**：
```tsx
function UserProfile(props: any) {
  const user = props.user;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.bio}</p>
    </div>
  );
}
```

**审查报告**：

```
总体评分: 4 / 10

🔴 阻塞项:
1. Props 使用 any 类型
   完全丧失类型安全，编译器无法检查

   Before:
   function UserProfile(props: any) { ... }

   After:
   interface UserProfileProps {
     user: {
       name: string;
       bio?: string;
     };
   }

   function UserProfile({ user }: UserProfileProps) { ... }

2. 未处理 user 为 undefined 的情况
   如果 user 未传入或正在加载，会抛出运行时错误

   After:
   function UserProfile({ user }: UserProfileProps) {
     if (!user) return <Skeleton />;
     return (...);
   }

🟡 警告项:
3. 缺少加载状态/错误状态
4. 组件未导出类型定义
```

### 示例3：可访问性问题

**输入代码**：
```tsx
function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return (
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content">
        {children}
      </div>
    </div>
  );
}
```

**审查报告**：

```
总体评分: 5 / 10

🔴 阻塞项:
1. 模态框缺少 ARIA 属性
   屏幕阅读器无法识别这是模态框

   After:
   <div
     role="dialog"
     aria-modal="true"
     aria-labelledby="modal-title"
     className="modal-overlay"
     onClick={onClose}
   >

2. 点击遮罩关闭时，焦点没有回到触发按钮
   键盘用户会迷失焦点位置

   After:
   useEffect(() => {
     const trigger = document.activeElement;
     return () => trigger?.focus();
   }, []);

3. 缺少 ESC 键关闭
   After:
   useEffect(() => {
     const handleKeyDown = (e: KeyboardEvent) => {
       if (e.key === 'Escape') onClose();
     };
     document.addEventListener('keydown', handleKeyDown);
     return () => document.removeEventListener('keydown', handleKeyDown);
   }, [onClose]);

🟡 警告项:
4. 内容区域点击会冒泡到遮罩导致意外关闭
   After:
   <div className="modal-content" onClick={e => e.stopPropagation()}>

5. 缺少焦点陷阱（Focus Trap）
   Tab 键会跳出模态框
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 |
|-------|------|
| **frontend-design** | 互补：frontend-design 管视觉设计，frontend-code-review 管代码质量 |
| **stop-slop** | 互补：stop-slop 去 AI 文字味，frontend-code-review 去代码坏味道 |
| **testing-patterns** | 配合：审查后应补充对应测试 |
| **component-refactoring** | 进阶：审查发现问题后，可用 refactoring 执行重构 |

**最佳实践链**：
```
编码 → frontend-design（定视觉方向）→ frontend-code-review（代码审查）
   → testing-patterns（补测试）→ quality-gate（质量门控）
```

---

## 🚀 快速开始

```
用户：审查这段前端代码 / React 代码 review

AI：
1. 静态扫描（行数/Props/样式/死代码）
2. 性能分析（重渲染/Memo/懒加载）
3. 可访问性检查（ARIA/键盘/对比度）
4. 类型安全检查（any/可选链/泛型）
5. 生成评分 + 🔴阻塞项 + 🟡警告项 + 🟢建议项
6. 提供 Before / After 重构方案
```

---

> "好的 Code Review 不是证明代码有多差，而是证明它可以有多好。"
