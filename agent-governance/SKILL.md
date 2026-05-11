---
name: "agent-governance"
description: "AI Agent治理框架：为AI Agent系统建立安全策略、信任评分、行为审计和威胁检测机制。当用户说'Agent安全'、'AI治理'、'Agent监控'、'AI策略'、'Agent审计'、'信任评分'、'AI威胁检测'、'Agent行为规范'时触发。核心特点：策略执行、信任评分、审计追踪、威胁检测。"
---

> **来源**: Anthropic Skills Issue #412
>
> **发布时间**: 2026-05
>
> **理念**: "没有治理的 Agent，就像没有刹车的跑车——快，但危险。"

# 🛡️ Agent Governance — AI Agent 治理框架

为 AI Agent 系统建立安全边界和行为规范。

---

## 🎯 核心概念

AI Agent 的治理需求：
- **权限失控** — Agent 执行了超出授权的操作
- **行为不可预测** — 相同输入产生不同输出
- **责任归属不清** — Agent 犯错谁负责
- **安全边界模糊** — Agent 访问了敏感数据

Agent Governance 的解决方案：
- **策略执行** — 明确 Agent 能做什么、不能做什么
- **信任评分** — 动态评估 Agent 行为的可信度
- **审计追踪** — 记录 Agent 的所有操作
- **威胁检测** — 识别异常行为模式

---

## 🏗️ 治理框架

### 1. 策略层 (Policy)

```yaml
agent_policies:
  file_access:
    allow: ["src/", "docs/", "tests/"]
    deny: [".env", "secrets/", "*.key"]
    max_file_size: "10MB"
  
  network_access:
    allow: ["api.github.com", "registry.npmjs.org"]
    deny: ["*"]  # 默认拒绝
  
  code_execution:
    allow_commands: ["npm test", "git status"]
    deny_commands: ["rm -rf /", "curl | bash"]
    require_approval: ["git push", "npm publish"]
  
  data_handling:
    mask_pii: true
    log_level: "audit"
    retention_days: 30
```

### 2. 信任评分层 (Trust Score)

```
Agent: code-builder-001
当前信任评分: 85/100

评分维度:
✅ 历史成功率    95/100 （过去100次任务，95次成功）
✅ 策略遵守率    98/100 （仅2次触碰边界）
⚠️ 异常行为频率  70/100 （本周有3次重试次数异常）
✅ 人工干预率    92/100 （仅8%的任务需要人工介入）

趋势: ↗️ 上升（上周 78 → 本周 85）
```

### 3. 审计层 (Audit Log)

```json
{
  "timestamp": "2026-05-11T10:30:00Z",
  "agent_id": "code-builder-001",
  "session_id": "sess-abc123",
  "action": "file_write",
  "target": "src/auth/login.ts",
  "size_delta": +45,
  "policy_check": "pass",
  "trust_delta": 0,
  "user_approval": "auto"
}
```

### 4. 威胁检测层 (Threat Detection)

| 威胁类型 | 检测规则 | 响应动作 |
|----------|---------|---------|
| **权限提升** | 请求超出授权范围的操作 | 拒绝 + 告警 |
| **数据泄露** | 输出包含敏感信息 | 拦截 + 脱敏 |
| **循环调用** | 同一操作重复失败 > 3 次 | 暂停 + 人工审查 |
| **异常时间** | 非工作时间的敏感操作 | 需要二次确认 |
| **资源耗尽** | CPU/内存使用超过阈值 | 限流 + 告警 |

---

## 🚀 使用方式

### 方式一：制定治理策略

```
为我们的多Agent系统制定治理策略
Agent角色: Planner, Builder, Reviewer, Deployer
```

### 方式二：评估Agent风险

```
评估当前Agent配置的安全风险
```

### 方式三：设计审计方案

```
设计Agent操作审计日志方案
需要记录哪些字段？保留多久？
```

---

## 🆚 与 Security Audit 的区别

| | agent-governance | security-audit |
|---|---|---|
| **对象** | AI Agent 自身行为 | 代码安全漏洞 |
| **时机** | 运行时持续监控 | 开发阶段静态扫描 |
| **重点** | 行为边界、权限控制 | 注入、密钥泄露等漏洞 |
| **最佳组合** | agent-governance 运行时防护 + security-audit 代码层防护 |

---

> "治理不是限制 Agent 的能力，而是让它的能力在安全边界内最大化。"
