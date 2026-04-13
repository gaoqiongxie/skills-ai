# 🧠 记忆系统 Skill（Memory System）

> 快速为 Spring Boot 项目搭建多层次记忆系统
> 适用场景：缓存架构设计、Session共享、性能优化、分布式系统

---

## 📦 支持类型

### 1️⃣ 缓存系统（Cache）

| 方案 | 特点 | 适用场景 | 复杂度 |
|------|------|---------|--------|
| **Spring Cache + Redis** | 注解驱动，最常用 | 中大型项目，分布式缓存 | ⭐ |
| **Caffeine** | 本地极速，JVM内最强 | 高频读，低更新 | ⭐ |
| **多级缓存** | L1(Caffeine) + L2(Redis) | 高并发场景 | ⭐⭐ |

### 2️⃣ 分布式会话（Session）

| 方案 | 存储 | 适用场景 | 复杂度 |
|------|------|---------|--------|
| **Spring Session + Redis** | Redis | 微服务集群 | ⭐ |
| **JWT Token** | 无状态 | 无状态API服务 | ⭐ |
| **Token + Redis** | Redis | 需要主动失效的场景 | ⭐⭐ |

### 3️⃣ 消息队列（轻量级记忆）

| 方案 | 特点 | 适用场景 | 复杂度 |
|------|------|---------|--------|
| **Redis Stream** | 轻量，无需额外部件 | 异步任务、事件驱动 | ⭐ |
| **Redis Delayed Queue** | 延迟消息 | 定时任务、延迟处理 | ⭐ |

---

## 🚀 快速开始

### 场景一：我要快速集成 Redis 缓存

```
输入：Spring Boot 项目，想加 Redis 缓存
```

**所需依赖（pom.xml）：**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-pool2</artifactId>
</dependency>
```

**配置文件（application.yml）：**
```yaml
spring:
  redis:
    host: localhost
    port: 6379
    password: # 可选
    database: 0
    lettuce:
      pool:
        max-active: 8
        max-idle: 8
        min-idle: 0
```

**使用示例：**
```java
@Cacheable(value = "user", key = "#id")
public User getUserById(Long id) {
    return userMapper.selectById(id);
}

@CachePut(value = "user", key = "#user.id")
public User updateUser(User user) {
    userMapper.updateById(user);
    return user;
}

@CacheEvict(value = "user", key = "#id")
public void deleteUser(Long id) {
    userMapper.deleteById(id);
}
```

---

### 场景二：我要搭建多级缓存（L1本地 + L2 Redis）

**所需依赖：**
```xml
<!-- L1 本地缓存 -->
<dependency>
    <groupId>com.github.ben-manes.caffeine</groupId>
    <artifactId>caffeine</artifactId>
</dependency>

<!-- L2 分布式缓存 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

<!-- 缓存锁（防止击穿） -->
<dependency>
    <groupId>Redisson</groupId>
    <artifactId>redisson-spring-boot-starter</artifactId>
    <version>3.25.0</version>
</dependency>
```

**多级缓存配置类：**
```java
@Configuration
public class CacheConfig {

    @Bean
    public Cache<String, Object> caffeineCache() {
        return Caffeine.newBuilder()
                .maximumSize(10_000)      // 最大条目
                .expireAfterWrite(60)      // 写入后60秒过期
                .recordStats()             // 记录统计
                .build();
    }
}
```

**多级缓存服务：**
```java
@Service
@Slf4j
public class MultiLevelCacheService {

    @Autowired
    private Cache<String, Object> localCache;  // Caffeine L1

    @Autowired
    private StringRedisTemplate redisTemplate; // Redis L2

    private static final String CACHE_PREFIX = "mlc:";

    public <T> T get(String key, Class<T> clazz, Supplier<T> loader) {
        // L1 查询
        T value = (T) localCache.getIfPresent(key);
        if (value != null) {
            log.debug("L1缓存命中: {}", key);
            return value;
        }

        // L2 查询
        String redisKey = CACHE_PREFIX + key;
        value = redisTemplate.opsForValue().get(redisKey);
        if (value != null) {
            log.debug("L2缓存命中: {}", key);
            localCache.put(key, value); // 回填L1
            return value;
        }

        // 加载数据
        log.debug("缓存未命中，加载数据: {}", key);
        value = loader.get();

        // 写入L2 + L1
        redisTemplate.opsForValue().set(redisKey, value, 1, TimeUnit.HOURS);
        localCache.put(key, value);

        return value;
    }

    public void evict(String key) {
        String redisKey = CACHE_PREFIX + key;
        localCache.invalidate(key);
        redisTemplate.delete(redisKey);
    }
}
```

---

### 场景三：我要做分布式 Session

**依赖：**
```xml
<dependency>
    <groupId>org.springframework.session</groupId>
    <artifactId>spring-session-data-redis</artifactId>
</dependency>
```

**配置：**
```java
@Configuration
@EnableRedisHttpSession(maxInactiveIntervalInSeconds = 3600)
public class SessionConfig {
    // Redis存储Session，自动集群共享
}
```

**使用：**
```java
@RestController
public class AuthController {

    @PostMapping("/login")
    public Result login(HttpServletRequest request) {
        // Session自动存到Redis
        request.getSession().setAttribute("userId", userId);
        return Result.ok();
    }

    @GetMapping("/info")
    public Result getUserInfo(HttpServletRequest request) {
        Long userId = (Long) request.getSession().getAttribute("userId");
        return Result.ok(userService.getById(userId));
    }
}
```

---

### 场景四：我要用 JWT + Redis 实现 Token 存储

**Token 工具类：**
```java
@Component
public class JwtUtil {

    @Value("${jwt.secret:mySecret}")
    private String secret;

    @Autowired
    private StringRedisTemplate redisTemplate;

    public String generateToken(Long userId) {
        String token = Jwts.builder()
                .setSubject(String.valueOf(userId))
                .setIssuedAt(new Date())
                .signWith(Keys.hmacShaKeyFor(secret.getBytes()))
                .compact();

        // Token存储到Redis（支持主动失效）
        redisTemplate.opsForValue().set(
                "token:" + userId,
                token,
                7, TimeUnit.DAYS
        );
        return token;
    }

    public boolean validateToken(String token) {
        try {
            Long userId = Long.parseLong(getUserIdFromToken(token));
            String storedToken = redisTemplate.opsForValue().get("token:" + userId);
            return token.equals(storedToken);
        } catch (Exception e) {
            return false;
        }
    }

    public void logout(Long userId) {
        redisTemplate.delete("token:" + userId);
    }
}
```

---

### 场景五：我要用 Redis Stream 实现异步任务队列

**消息服务：**
```java
@Service
public class MessageQueueService {

    @Autowired
    private StringRedisTemplate redisTemplate;

    private static final String STREAM_KEY = "mq:tasks";

    // 生产消息
    public void sendTask(String type, Map<String, Object> data) {
        Map<String, String> fields = new HashMap<>();
        fields.put("type", type);
        fields.put("data", JSON.toJSONString(data));
        fields.put("timestamp", String.valueOf(System.currentTimeMillis()));

        redisTemplate.opsForStream().add(
                StreamRecords.newRecord()
                        .in(STREAM_KEY)
                        .ofMap(fields)
        );
    }

    // 消费消息
    @Scheduled(fixedDelay = 1000)
    public void consumeTasks() {
        List<MapRecord<String, Object, Object>> records = redisTemplate.opsForStream()
                .read(StreamReadOptions.empty().count(10),
                      StreamOffset.create(STREAM_KEY, ReadOffset.from("0")));

        if (records != null) {
            for (MapRecord<String, Object, Object> record : records) {
                Map<Object, Object> value = record.getValue();
                String type = (String) value.get("type");
                String data = (String) value.get("data");

                // 处理消息
                processTask(type, data);

                // ACK删除
                redisTemplate.opsForStream().delete(STREAM_KEY, record.getId());
            }
        }
    }
}
```

---

## 🛠️ 常用缓存策略

| 策略 | 配置 | 适用场景 |
|------|------|---------|
| **Cache-Aside** | 先查缓存，miss再查DB | 读多写少 |
| **Write-Through** | 同步写缓存和DB | 数据一致性要求高 |
| **Write-Behind** | 异步写DB | 高并发写入 |

### 缓存失效处理

```java
// 缓存击穿：加锁
public User getUserWithLock(Long id) {
    String key = "user:" + id;
    User user = cache.get(key);

    if (user == null) {
        RLock lock = redissonClient.getLock("lock:" + key);
        try {
            lock.lock(10, TimeUnit.SECONDS);
            user = cache.get(key);
            if (user == null) {
                user = userMapper.selectById(id);
                cache.put(key, user, 1, TimeUnit.HOURS);
            }
        } finally {
            lock.unlock();
        }
    }
    return user;
}

// 缓存穿透：布隆过滤器 / 空值缓存
public User getUserAvoid穿透(Long id) {
    String key = "user:" + id;
    User user = cache.get(key);

    if (user == null) {
        // 查DB
        user = userMapper.selectById(id);

        // 空值也缓存，防止穿透
        if (user == null) {
            cache.put(key, "NULL", 5, TimeUnit.MINUTES);
        } else {
            cache.put(key, user, 1, TimeUnit.HOURS);
        }
    }
    return user;
}
```

---

## 📊 技术选型建议

```
┌─────────────────────────────────────────────────────────┐
│                     项目规模                              │
├─────────────┬─────────────┬─────────────┬───────────────┤
│   小型项目  │   中型项目   │   大型项目   │   超大型项目   │
├─────────────┼─────────────┼─────────────┼───────────────┤
│ Caffeine   │ Spring Cache│  多级缓存   │  多级缓存     │
│ 本地缓存    │   + Redis   │ + 熔断降级  │ + 集群部署    │
├─────────────┼─────────────┼─────────────┼───────────────┤
│ Session    │ Redis Session│ JWT + Redis │ Spring Session│
│ 本地存储    │  集群共享    │ + Token黑名单│  + 多节点     │
└─────────────┴─────────────┴─────────────┴───────────────┘
```

---

## 🎯 快速诊断

| 问题 | 可能原因 | 解决方案 |
|------|---------|---------|
| 缓存没生效 | 没加@EnableCaching | 启动类加注解 |
| 序列化失败 | 对象没实现Serializable | 实现序列化接口 |
| 缓存穿透 | 空值没缓存 | 缓存NULL值 |
| 缓存雪崩 | 同时过期 | 随机TTL + 熔断 |
| 热点Key | 大V数据 | 多副本 + 本地缓存 |

---

## 🔗 相关资源

- [Spring Cache文档](https://docs.spring.io/spring-framework/docs/current/reference/html/integration.html#cache)
- [Redis中文文档](http://www.redis.cn/)
- [Caffeine GitHub](https://github.com/ben-manes/caffeine)
- [Redisson文档](https://github.com/redisson/redisson/wiki)

---

## 💬 使用方式

直接描述你的场景，我来帮你快速搭建：

- "我有Spring Boot项目，想加Redis缓存"
- "帮我设计一个多级缓存架构"
- "微服务Session共享怎么实现"
- "我要做接口限流和缓存"
- "高并发场景缓存怎么防击穿"
