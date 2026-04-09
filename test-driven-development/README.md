# Test-Driven Development - 测试驱动开发

> **来源**: obra/superpowers (142K⭐) - AI辅助开发方法论框架
> 
> **参考**: TDD (Test-Driven Development) 红-绿-重构循环

---

## 🎯 什么是TDD？

**Test-Driven Development (TDD)** = 测试驱动开发

核心理念：**先写测试，再写实现**

> "写测试不是为了证明代码正确，而是为了发现代码可能存在的错误。"

---

## 🔄 红-绿-重构循环

```
    ┌─────────────────────────────────────┐
    │  🔴 先写测试（RED）                  │
    │  ↓  写一个会失败的测试               │
    │  🟢 写实现（GREEN）                  │
    │  ↓  写能通过的最少代码               │
    │  🔵 重构（REFACTOR）                 │
    │  ↓  改进代码质量                     │
    │  ← 循环直到完成                      │
    └─────────────────────────────────────┘
```

---

## 📝 使用示例

### 用户说："实现用户登录功能"

### AI按TDD流程执行：

**步骤1：写一个失败的测试 🔴**
```java
@Test
void shouldReturnUserWhenCredentialsValid() {
    // 准备测试数据
    String username = "test";
    String password = "password123";
    
    // 调用登录
    User user = authService.login(username, password);
    
    // 断言
    assertNotNull(user);
    assertEquals("test", user.getUsername());
}
```

**步骤2：写最简单的实现 🟢**
```java
public User login(String username, String password) {
    // 最简单实现：直接返回用户
    return new User(username);
}
```

**步骤3：测试通过后继续 🔴**
```java
@Test
void shouldThrowExceptionWhenCredentialsInvalid() {
    assertThrows(AuthException.class, () -> {
        authService.login("wrong", "wrong");
    });
}
```

**步骤4：实现错误处理 🟢**
```java
public User login(String username, String password) {
    User user = userRepository.findByUsername(username);
    if (user == null || !user.checkPassword(password)) {
        throw new AuthException("Invalid credentials");
    }
    return user;
}
```

**步骤5：重构 🔵**
```java
// 优化：提取验证逻辑
public User login(String username, String password) {
    User user = findUserOrThrow(username);
    validatePassword(user, password);
    return user;
}
```

---

## 📊 测试金字塔

```
              /\
             /  \
            / E2E \      ← 少量（5-10个）
           /────────\
          / 集成测试  \   ← 中量（20-50个）
         /────────────\
        /   单元测试    \  ← 大量（100+个）
       /────────────────\
```

| 层级 | 速度 | 成本 | 数量 |
|-----|------|-----|------|
| E2E | 分钟 | 最高 | 5-10 |
| 集成 | 秒 | 中 | 20-50 |
| 单元 | 毫秒 | 低 | 100+ |

---

## ✅ 好测试的特点 (F.I.R.S.T)

| 字母 | 原则 | 解释 |
|-----|------|------|
| **F**ast | 快速 | 避免数据库、网络 |
| **I**ndependent | 独立 | 不依赖其他测试 |
| **R**epeatable | 可重复 | 每次结果一致 |
| **S**elf-validating | 自验证 | 断言自动判断 |
| **T**imely | 及时 | 先写测试 |

---

## 🎨 测试命名规范

```java
// 推荐：描述性的测试名
@Test
void shouldReturnEmptyListWhenNoUsersExist()

@Test
void shouldThrowNullPointerExceptionWhenInputIsNull()

@Test
void shouldCalculateDiscountCorrectlyForVIPCustomers()

// ❌ 避免：模糊的测试名
@Test
void test1()

@Test
void testLogin()
```

---

## 📦 测试结构 (AAA模式)

```java
@Test
void shouldProcessOrderSuccessfully() {
    // ===== Arrange - 准备 =====
    Order order = new Order();
    order.addItem(new Item("Book", 100));
    order.addItem(new Item("Pen", 10));
    
    // ===== Act - 执行 =====
    double total = orderService.calculateTotal(order);
    
    // ===== Assert - 断言 =====
    assertEquals(110.0, total, 0.01);
}
```

---

## 🔍 常见测试场景

### 边界值测试
```java
@Test
void shouldHandleEmptyString() {
    assertEquals("", stringUtils.trim(""));
}

@Test
void shouldHandleNull() {
    assertNull(stringUtils.trim(null));
}

@Test
void shouldHandleSingleCharacter() {
    assertEquals("x", stringUtils.trim(" x "));
}
```

### 异常测试
```java
@Test
void shouldThrowExceptionWhenUserNotFound() {
    assertThrows(UserNotFoundException.class, () -> {
        userService.getUserById(999);
    });
}
```

### 集合测试
```java
@Test
void shouldReturnEmptyListWhenNoResults() {
    List<User> users = userService.searchByName("NotExist");
    assertTrue(users.isEmpty());
}

@Test
void shouldReturnMultipleResults() {
    List<User> users = userService.searchByName("张");
    assertEquals(3, users.size());
}
```

---

## 🚀 运行测试

### Java/Maven
```bash
# 运行所有测试
mvn test

# 运行特定测试类
mvn test -Dtest=UserServiceTest

# 生成覆盖率报告
mvn test jacoco:report
```

### JavaScript/Node
```bash
# 运行所有测试
npm test

# 监视模式
npm run test:watch

# 覆盖率
npm run test:coverage
```

### Python
```bash
# 运行所有测试
pytest

# 运行特定文件
pytest tests/test_user.py

# 详细输出
pytest -v
```

---

## ⚠️ TDD常见误区

| ❌ 错误做法 | ✅ 正确做法 |
|-----------|------------|
| 先写代码后补测试 | 先写测试再写实现 |
| 测试所有细节 | 测试关键行为 |
| 测试依赖实现 | 测试输入输出 |
| 测试之间互相依赖 | 保持测试独立 |
| 忽略失败的测试 | 失败=停止 |

---

## 📚 相关资源

- **Superpowers**: github.com/obra/superpowers
- **系统化调试**: systematic-debugging skill
- **代码审查**: github-code-review skill
