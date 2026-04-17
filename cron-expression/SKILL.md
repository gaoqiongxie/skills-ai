---
title: "最强Cron表达式"
description: "Cron表达式生成、解析、验证工具。触发词：cron、crontab、定时任务、任务调度、cron表达式、每分钟、每小时、每天、每周、每月、每年
---

# Cron表达式技能

## 快速生成

直接描述你的需求，我来生成Cron表达式！

| 场景 | 示例 | Cron |
|------|------|------|
| 每分钟 | 整分钟执行 | `0 * * * *` |
| 每小时 | 每小时整点 | `0 0 * * *` |
| 每天凌晨 | 每天3点 | `0 3 * * *` |
| 每天多次 | 9/14/19点 | `0 9,14,19 * * *` |
| 每周一 | 每周一9点 | `0 9 * * 1` |
| 每月1号 | 每月1号0点 | `0 0 1 * *` |
| 工作日 | 周一到周五9点 | `0 9 * * 1-5` |
| 每30分钟 | 半小时一次 | `0 */30 * * *` |
| 每2小时 | 每2小时执行 | `0 */2 * * *` |
| 每天区间 | 9-18点每时 | `0 9-18 * * *` |
| 每季度 | 每季度1号 | `0 0 1 1,4,7,10 *` |
| 每10秒 | 每10秒(特殊) | `*/10 * * * * *` |

---

## Cron表达式格式

### 标准格式（5位）
```
┌───────────── 分钟 (0-59)
│ ┌─────────── 小时 (0-23)
│ │ ┌───────── 日 (1-31)
│ │ │ ┌─────── 月 (1-12)
│ │ │ │ ┌───── 星期 (0-7, 0和7都是周日)
│ │ │ │ │
* * * * *
```

### Quartz格式（6-7位，多一秒字段）
```
┌───────────── 秒 (0-59)
│ ┌─────────── 分钟 (0-59)
│ │ ┌───────── 小时 (0-23)
│ │ │ ┌───────── 日 (1-31)
│ │ │ │ ┌─────── 月 (1-12)
│ │ │ │ │ ┌───── 星期 (0-7)
│ │ │ │ │ │ 
* * * * * *
```

---

## 特殊字符

| 字符 | 含义 | 示例 |
|------|------|------|
| `*` | 任意值 | `* * * * *` = 每分钟 |
| `,` | 列表值 | `0 9,12,18 * * *` = 9/12/18点 |
| `-` | 范围值 | `0 9-17 * * *` = 9点到17点 |
| `/` | 步长值 | `*/15 * * * *` = 每15分钟 |
| `?` | 不关心（日/月互斥） | Quartz用 |
| `L` | 最后 | `L * *` = 每月最后一天 |
| `W` | 最近工作日 | `15W * *` = 15号最近工作日 |
| `#` | 第N个 | `6#3 * *` = 每月第3个周六 |

---

## 常用表达式速查表

### 🔥 日常高频

| 场景 | Cron | 说明 |
|------|------|------|
| 每分钟 | `0 * * * *` | |
| 每5分钟 | `*/5 * * * *` | |
| 每15分钟 | `*/15 * * * *` | |
| 每30分钟 | `*/30 * * * *` | |
| 每小时 | `0 0 * * * *` | |
| 每2小时 | `0 */2 * * *` | |
| 每6小时 | `0 */6 * * *` | |
| 每12小时 | `0 */12 * * *` | |

### 📅 每日

| 场景 | Cron | 说明 |
|------|------|------|
| 每天凌晨0点 | `0 0 * * *` | |
| 每天凌晨1点 | `0 1 * * *` | |
| 每天2点 | `0 2 * * *` | 备份常用 |
| 每天3点 | `0 3 * * *` | 数据同步 |
| 每天6点 | `0 6 * * *` | 报表生成 |
| 每天8点 | `0 8 * * *` | 工作日开始 |
| 每天9点 | `0 9 * * *` | 提醒任务 |
| 每天12点 | `0 12 * * *` | 正午同步 |
| 每天18点 | `0 18 * * *` | 下班提醒 |
| 每天22点 | `0 22 * * *` | 日终处理 |
| 每天23点 | `0 23 * * *` | |

### 📆 每周

| 场景 | Cron | 说明 |
|------|------|------|
| 每周一9点 | `0 9 * * 1` | |
| 每周二9点 | `0 9 * * 2` | |
| 每周三9点 | `0 9 * * 3` | |
| 每周四9点 | `0 9 * * 4` | |
| 每周五9点 | `0 9 * * 5` | |
| 每周六10点 | `0 10 * * 6` | |
| 每周日10点 | `0 10 * * 0` | |

### 🗓️ 每月

| 场景 | Cron | 说明 |
|------|------|------|
| 每月1号0点 | `0 0 1 * *` | |
| 每月1号9点 | `0 9 1 * *` | |
| 每月15号0点 | `0 0 15 * *` | |
| 每月最后一天 | `0 0 L * *` | |
| 每月最后一天22点 | `0 22 L * *` | |
| 每月1/15号 | `0 0 1,15 * *` | |

### 💼 工作日模式

| 场景 | Cron | 说明 |
|------|------|------|
| 工作日9点 | `0 9 * * 1-5` | |
| 工作日18点 | `0 18 * * 1-5` | |
| 工作日9-18点整点 | `0 9-18 * * 1-5` | |
| 工作日每30分钟 | `0 */30 * * 1-5` | |
| 工作日每15分钟 | `0 */15 9-18 * 1-5` | 核心时段 |

### 🗓️ 季度/半年/年度

| 场景 | Cron | 说明 |
|------|------|------|
| 每季度 | `0 0 1 1,4,7,10 *` | 季度首月1号 |
| 每季度末 | `0 0 1 3,6,9,12 *` | |
| 每半年 | `0 0 1 1,7 *` | |
| 每年1月1号 | `0 0 1 1 *` | |
| 每年生日 | `0 0 15 6 *` | 6月15号 |

---

## Java/Spring Boot 实现

### 1. @Scheduled 注解（最简单）

```java
@SpringBootApplication
@EnableScheduling
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

@Component
public class ScheduledTasks {
    
    // 每5秒（注意：@Scheduled默认不支持秒，需要配置）
    @Scheduled(fixedRate = 5000)
    public void everyFiveSeconds() {}
    
    // 每分钟整点
    @Scheduled(cron = "0 * * * * *")
    public void everyMinute() {}
    
    // 每天凌晨3点
    @Scheduled(cron = "0 0 3 * * *")
    public void dailyAtThree() {}
    
    // 每周一9点
    @Scheduled(cron = "0 0 9 ? * MON")
    public void mondayAtNine() {}
    
    // 工作日每30分钟
    @Scheduled(cron = "0 0/30 9-18 ? * MON-FRI")
    public void workdayEvery30Min() {}
}
```

### 2. 配置秒级Cron（重要！）

```yaml
# application.yml
spring:
  task:
    scheduling:
      pool:
        size: 10
      thread-name-prefix: "scheduled-"
  cron:
    enabled: true
```

### 3. Cron表达式引号问题

```java
// ✅ 正确写法
@Scheduled(cron = "0 0 3 * * ?")  // Spring风格用?
@Scheduled(cron = "0 0 3 * * *")  // Quartz风格

// ⚠️ 星期几用?，日/月互斥
@Scheduled(cron = "0 0 9 ? * MON")  // ✅ 周一9点
@Scheduled(cron = "0 0 9 * * MON")  // ✅ 也行

// ⚠️ 年份最好不写
@Scheduled(cron = "0 0 9 * * ? 2026")  // ❌ 跨年不执行
```

---

## Spring Boot Dynamic Task

### 动态启停定时任务

```java
@Component
public class DynamicScheduler {
    
    private final Map<String, ScheduledTask> tasks = new ConcurrentHashMap<>();
    
    @Autowired
    private TaskScheduler taskScheduler;
    
    public void addTask(String name, String cron, Runnable action) {
        // 先取消已存在的
        tasks.get(name).cancel();
        
        // 解析Cron
        CronTrigger trigger = new CronTrigger(cron);
        ScheduledTask task = new ScheduledTask(
            taskScheduler.schedule(action, trigger)
        );
        tasks.put(name, task);
    }
    
    public void removeTask(String name) {
        tasks.get(name).cancel();
        tasks.remove(name);
    }
}
```

---

## MySQL Event Scheduler

```sql
-- 开启Event调度器
SET GLOBAL event_scheduler = ON;

-- 每天凌晨3点执行
CREATE EVENT daily_cleanup
ON SCHEDULE EVERY 1 DAY STARTS '2026-01-01 03:00:00'
DO
BEGIN
    -- 清理30天前的日志
    DELETE FROM operation_log 
    WHERE create_time < DATE_SUB(NOW(), INTERVAL 30 DAY);
END;

-- 每周一凌晨2点
CREATE EVENT weekly_backup
ON SCHEDULE EVERY 1 WEEK STARTS '2026-01-06 02:00:00'
DO
BEGIN
    CALL backup_procedure();
END;
```

---

## Linux Crontab

```bash
# 编辑crontab
crontab -e

# 格式：分 时 日 月 周 命令
# ┌────── 分 (0-59)
# │ ┌──── 时 (0-23)
# │ │ ┌── 日 (1-31)
# │ │ │ ┌─ 月 (1-12)
# │ │ │ │ ┌ 周 (0-7, 0和7是周日)
# │ │ │ │ │
# * * * * * command

# 常用示例
0 * * * *           # 每小时
0 0 * * *           # 每天午夜
0 9 * * 1           # 每周一9点
0 0 1 * *           # 每月1号
*/5 * * * *         # 每5分钟
0 */2 * * *         # 每2小时

# 查看crontab
crontab -l

# 查看日志
grep CRON /var/log/syslog
tail -f /var/log/cron.log
```

---

## 星期对照表

| 值 | 星期 |
|---|------|
| 0 | 周日 (SUN) |
| 1 | 周一 (MON) |
| 2 | 周二 (TUE) |
| 3 | 周三 (WED) |
| 4 | 周四 (THU) |
| 5 | 周五 (FRI) |
| 6 | 周六 (SAT) |
| 7 | 周日 (SUN) |

---

## 在线工具推荐

| 工具 | 链接 | 特点 |
|------|------|------|
| Cron Expression | cronexpression.cn | 中文友好 |
| Cron Guru | crontab.guru | 可视化强 |
| FreeFormatter | freeformatter.com/cron-expression-generator.html | 实时预览 |
| Cron Job API | www.cronmaker.com | 生成器 |

---

## Quartz 特殊字符

| 字符 | 含义 | 示例 |
|------|------|------|
| `L` | 最后 | `L-3` = 每月倒数第3天 |
| `W` | 工作日 | `15W` = 15号最近工作日 |
| `#` | 第N个 | `6#3` = 第3个周六 |
| `L` + 周 | 周最后 | `6L` = 周六最后 |

### Quartz示例
```java
// 每月最后一个周五
@Scheduled(cron = "0 0 10 ? * 6L")

// 每月第三个周三
@Scheduled(cron = "0 0 9 ? * 3#3")

// 每月15号最近工作日
@Scheduled(cron = "0 0 10 15W * ?")
```

---

## 踩坑经验

- **Spring默认不支持秒**：需配置或改用Quartz
- **? 和 * 的区别**：?表示不关心（日/月互斥），Spring推荐用?
- **星期跨年问题**：不要写死年份
- **时区问题**：服务器时区和业务时区要统一
- **集群问题**：多实例要用分布式锁，避免重复执行
