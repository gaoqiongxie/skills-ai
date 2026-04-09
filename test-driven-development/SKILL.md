---
name: "test-driven-development"
description: "测试驱动开发(TDD)方法论，严格执行'红-绿-重构'循环进行新功能开发和Bug修复。当用户开始新功能、修复Bug、或者需要添加测试用例时使用。"
---

# Test-Driven Development - 测试驱动开发

> **来源**: obra/superpowers (142K⭐) - AI辅助开发方法论框架
> 
> **参考**: TDD (Test-Driven Development) 最佳实践

## 核心理念

> "写测试不是为了证明代码正确，而是为了发现代码可能存在的错误。" —— 测试即文档

**TDD三定律**：
1. 除非是为了让一个失败的单元测试通过，否则不允许编写任何产品代码
2. 允许编写任何能够确保失败但无法编译的程序代码（逐步完善）
3. 允许编写刚好能够使失败测试通过的产品代码（不再多写）

## 红-绿-重构循环

```
    ┌─────────────────────────────────────┐
    │                                     │
    ▼                                     │
┌─────────┐   Write   ┌─────────┐   Fix   │
│  RED    │ ────────▶ │  GREEN  │ ───────▶│
│  失败   │   测试    │  通过   │   代码  │
└─────────┘           └─────────┘          │
    ▲                                        │
    │                                        │
    └──────────── Refactor ─────────────────┘
                  重构改进
```

### 🔴 RED 阶段：写一个会失败的测试

**目标**：描述期望的行为

**操作**：
1. 理解需求，写出期望的测试用例
2. 测试要尽可能小，只测一个方面
3. 运行测试，确认失败（这是预期的）

**示例**：
```java
// ❌ 这会编译失败或测试失败
@Test
void shouldReturnEmptyListWhenNoData() {
    // 假设我们要实现：没有数据时返回空列表
    List<User> users = userService.findAll();
    assertTrue(users.isEmpty());
}
```

### 🟢 GREEN 阶段：写能让测试通过的最少代码

**目标**：快速让测试通过

**操作**：
1. 写最简单能通过的实现
2. **不要优化、不要完善**——后续重构阶段再做
3. 测试通过即可停止

**示例**：
```java
// ✅ 最简单的实现
public List<User> findAll() {
    return new ArrayList<>(); // 直接返回空列表
}
```

### 🔵 REFACTOR 阶段：重构改进

**目标**：消除重复、提升代码质量

**操作**：
1. 审视代码，寻找坏味道
2. 逐步重构，每次确保测试通过
3. 重构后测试仍要全部通过

**示例**：
```java
// 重构：移除重复，改进设计
public List<User> findAll() {
    return userRepository.findAll(); // 真实实现
}
```

## 适用场景

| 场景 | 使用方式 |
|-----|---------|
| 新功能开发 | 先写测试，再实现 |
| Bug修复 | 先写测试复现Bug，再修复 |
| 遗留代码 | 添加测试覆盖，再修改 |
| 重构 | 先写测试，再重构 |

## 测试用例设计

### 好的测试特点 (F.I.R.S.T)

| 原则 | 说明 | 示例 |
|-----|------|------|
| **F**ast | 快速 | 避免I/O、网络 |
| **I**ndependent | 独立 | 不依赖其他测试 |
| **R**epeatable | 可重复 | 结果确定 |
| **S**elf-validating | 自验证 | 断言明确 |
| **T**imely | 及时 | 先写测试 |

### 测试命名规范

```java
// 格式：[方法]_[场景]_[期望结果]
@Test
void shouldReturnEmptyListWhenNoDataExists()

@Test  
void shouldThrowExceptionWhenUserNotFound()

@Test
void shouldCalculateTotalPriceWithDiscount()
```

### 测试结构 (AAA模式)

```java
@Test
void shouldProcessOrderCorrectly() {
    // Arrange - 准备测试数据
    Order order = new Order();
    order.addItem(new Item("Product", 100));
    
    // Act - 执行被测操作
    double total = orderProcessor.calculateTotal(order);
    
    // Assert - 验证结果
    assertEquals(100, total, 0.01);
}
```

### 常见测试覆盖点

| 类别 | 测试用例 |
|-----|---------|
| 正常流程 | 正确输入，正常返回 |
| 边界条件 | 0、空、最大值 |
| 异常处理 | null、非法输入 |
| 边界值 | -1、0、1、最大值+1 |
| 特殊值 | 空字符串、空集合 |

## 测试金字塔

```
           ┌─────────┐
           │   E2E   │   ← 少量，端到端
          ┌─────────┐
         │集成测试 │   ← 中量，按模块
        ┌─────────┐
       │ 单元测试 │   ← 大量，最快最便宜
      └─────────┘
```

| 层级 | 数量 | 执行速度 | 覆盖范围 |
|-----|------|---------|---------|
| E2E | 10-20 | 慢(分钟) | 关键路径 |
| 集成 | 50-100 | 中(秒) | 模块交互 |
| 单元 | 100+ | 快(毫秒) | 函数/类 |

## 回归测试策略

修改代码后，确保：
1. 所有现有测试仍然通过
2. 新功能有测试覆盖
3. Bug修复有测试防止复现

```bash
# 运行所有测试
npm test

# 运行特定测试
npm test -- --grep "UserService"

# 生成覆盖率报告
npm test -- --coverage
```

## 输出模板

```markdown
## TDD开发记录

### 功能：[功能名称]

#### 🔴 RED - 失败的测试
```java
[测试代码]
```

#### 🟢 GREEN - 通过的实现
```java
[实现代码]
```

#### 🔵 REFACTOR - 重构
```java
[重构后的代码]
```

### 测试覆盖
| 场景 | 测试 | 状态 |
|-----|------|------|
| 正常流程 | testXXX_Normal | ✅ |
| 空输入 | testXXX_Empty | ✅ |
| 异常输入 | testXXX_Exception | ✅ |

### 运行结果
```
✅ 12 tests passed
⏱️ 0.5s
📊 85% coverage
```
```

## 反模式警示

❌ **不要**：
- 先写代码后写测试（事后诸葛亮）
- 测试覆盖所有路径（聚焦关键逻辑）
- 测试依赖实现细节（测试行为非实现）
- 测试之间互相依赖（保持独立）
- 忽略失败的测试（失败即停）

✅ **应该**：
- 测试业务价值，而非技术细节
- 最小化设置代码
- 一个测试一个断言
- 让测试描述文档化
