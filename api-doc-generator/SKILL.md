---
name: "api-doc-generator"
description: >
  API 文档生成器：根据 Java 代码（Controller/Service/Entity）自动生成 Swagger/OpenAPI 注解和文档。
  适用于写接口文档、生成 @Api/@ApiOperation 注解、完善 Knife4j 配置、输出接口说明等场景。
  触发词：写接口文档、生成Swagger、@Api注解、API文档、OpenAPI、Knife4j、写接口说明
---

# 📄 API 文档生成器

> 根据 Java 代码，自动生成规范的 Swagger/OpenAPI 注解和文档说明。

---

## 核心能力

| 能力 | 说明 |
|------|------|
| Controller 注解生成 | 自动添加 @Api/@ApiOperation |
| Entity 字段注解 | 自动添加 @ApiModelProperty |
| 参数说明补充 | 对 RequestBody/PathVar/RequestParam 补中文说明 |
| 接口分组文档 | 按模块/功能分组接口文档 |
| OpenAPI 配置 | 完善 Knife4j/SpringDoc 配置 |

---

## 工作流程

### Step 1：分析目标代码

识别以下内容：
- Controller 类名、方法名、请求路径
- 参数类型（实体类/基本类型/List）
- 返回值类型
- 业务含义（从注释/命名推断）

### Step 2：生成注解

```java
// 原始代码
@PostMapping("/user")
public User saveUser(@RequestBody User user) {
    return userService.save(user);
}

// 生成的注解
@Api(tags = "用户管理")
@RestController
@RequestMapping("/api/user")
public class UserController {

    @ApiOperation(value = "保存用户", notes = "接收用户信息并持久化")
    @PostMapping("/save")
    public Result<User> saveUser(
            @ApiParam(value = "用户信息", required = true) @RequestBody UserDTO user) {
        return Result.success(userService.save(user));
    }
}
```

### Step 3：补充字段说明

```java
// Entity 字段
@Data
public class UserDTO {
    @ApiModelProperty(value = "用户名", example = "张三", required = true)
    private String username;

    @ApiModelProperty(value = "手机号", example = "13800138000")
    private String phone;
}
```

---

## 常用模板

### 增删改查标准注解

```
GET    /list        → @ApiOperation("查询列表")
GET    /{id}        → @ApiOperation("根据ID查询")
POST   /save        → @ApiOperation("新增")
PUT    /update      → @ApiOperation("更新")
DELETE /{id}        → @ApiOperation("删除")
```

### 分页查询

```java
@ApiOperation(value = "分页查询", notes = "支持按姓名/状态筛选，默认分页")
@ApiImplicitParams({
    @ApiImplicitParam(name = "page", value = "页码", dataType = "int"),
    @ApiImplicitParam(name = "size", value = "每页条数", dataType = "int"),
    @ApiImplicitParam(name = "name", value = "姓名模糊搜索", dataType = "String")
})
@GetMapping("/page")
public Result<Page<User>> page(
        @RequestParam(defaultValue = "1") Integer page,
        @RequestParam(defaultValue = "10") Integer size,
        @RequestParam(required = false) String name) {
    return Result.success(userService.page(page, size, name));
}
```

---

## 输出格式

提供两种文档格式：

### 1. 注解代码（直接贴入项目）

### 2. Markdown 接口文档

```markdown
## 用户管理 /api/user

### 1. 保存用户
- **接口**: `POST /api/user/save`
- **描述**: 接收用户信息并持久化
- **请求参数**:
  | 参数名 | 类型 | 必填 | 说明 |
  |--------|------|------|------|
  | username | String | 是 | 用户名 |
  | phone | String | 否 | 手机号 |
- **响应**: `Result<User>`
```

---

## 使用提示

- 直接粘贴 Controller 代码，让 AI 帮你生成注解
- 可以指定风格：SpringDoc（Java 8+）或 Knife4j
- 可以指定分组：按模块或按接口类型分组
- 生成的注解需要手动复制到代码中

---

## 一句话原则

> 文档是给调用方看的，注解是给工具看的——两者同样重要。
