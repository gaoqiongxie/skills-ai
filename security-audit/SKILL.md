---
name: "security-audit"
description: "安全审计工作流：AI驱动的代码安全审查，集成CodeQL/Semgrep静态分析，识别OWASP Top 10漏洞。当用户说'安全审计'、'代码安全检查'、'漏洞扫描'、'security review'、'代码安全'、'渗透测试'、'安全漏洞'、'OWASP'时触发。核心特点：静态分析集成、漏洞模式识别、修复建议自动生成、合规性检查。"
---

> **来源**: trailofbits/skills + OWASP + 安全社区实践
>
> **发布时间**: 2026-05
>
> **理念**: "安全不是可选项，是每个 commit 的必选项。"

# 🔒 Security Audit — 安全审计工作流

AI 驱动的代码安全审查，在开发阶段就消灭漏洞。

---

## 🎯 核心能力

| 能力 | 说明 |
|------|------|
| **静态分析** | 集成 CodeQL / Semgrep / Bandit 等工具 |
| **漏洞识别** | 识别 OWASP Top 10 及其他常见漏洞模式 |
| **依赖审计** | 检查第三方库已知 CVE 漏洞 |
| **密钥扫描** | 检测代码中硬编码的密钥、Token、密码 |
| **修复建议** | 自动生成安全修复代码 |
| **合规检查** | 检查是否符合安全编码规范 |

---

## 🔍 审计检查清单

### OWASP Top 10 覆盖

| 排名 | 漏洞类型 | 检测能力 | 示例 |
|------|---------|---------|------|
| A01 | 注入攻击 (Injection) | ✅ SQL/XSS/命令注入 | `SELECT * FROM users WHERE id = '$id'` |
| A02 | 失效认证 (Broken Auth) | ✅ 弱密码/JWT 配置/会话管理 | JWT 无过期时间 |
| A03 | 敏感数据暴露 | ✅ 明文存储/传输/日志 | 密码明文打印日志 |
| A04 | XML 外部实体 (XXE) | ✅ XML 解析器配置 | `DocumentBuilder` 未禁用 DTD |
| A05 | 失效访问控制 | ✅ 越权访问/IDOR | 缺少权限校验 |
| A06 | 安全配置错误 | ✅ 默认配置/调试信息泄露 | 生产环境开启 debug |
| A07 | 跨站脚本 (XSS) | ✅ 反射型/存储型/DOM型 | 未转义用户输入 |
| A08 | 不安全的反序列化 | ✅ 反序列化漏洞 | Java `ObjectInputStream` |
| A09 | 使用含漏洞组件 | ✅ 依赖 CVE 扫描 | Log4j 漏洞 |
| A10 | 不足的日志监控 | ✅ 缺少审计日志 | 关键操作无记录 |

### 扩展检查

| 检查项 | 说明 |
|--------|------|
| **硬编码密钥** | API Key、Secret、密码 |
| **不安全的随机数** | 使用 `Math.random()` 生成 Token |
| **不安全的文件上传** | 缺少类型/大小校验 |
| **CORS 配置不当** | `Access-Control-Allow-Origin: *` |
| **不安全的加密** | MD5/SHA1、ECB 模式、弱密钥 |
| **路径遍历** | `../` 未过滤 |
| **SSRF** | 服务端请求伪造 |

---

## 🛠️ 集成工具链

```
代码提交 → 安全审计触发
    ├── CodeQL 分析（语义分析）
    ├── Semgrep 扫描（模式匹配）
    ├── Bandit 检查（Python专用）
    ├── Dependency-Check（依赖漏洞）
    └── Gitleaks（密钥扫描）
        ↓
    生成安全报告 + 修复建议
```

---

## 📋 审计输出格式

```markdown
## 安全审计报告

### 概览
- 扫描文件：127
- 发现问题：5（高危 2 / 中危 2 / 低危 1）
- 扫描时间：2026-05-09 10:30

### 高危问题

#### [HIGH] SQL 注入 (A01)
- **位置**: `src/user/dao.py:45`
- **代码**: `cursor.execute(f"SELECT * FROM users WHERE name = '{name}'")`
- **风险**: 攻击者可执行任意 SQL 命令
- **修复**:
  ```python
  cursor.execute("SELECT * FROM users WHERE name = %s", (name,))
  ```

#### [HIGH] 硬编码 JWT 密钥 (A03)
- **位置**: `src/config.py:12`
- **代码**: `JWT_SECRET = "my-secret-key-123"`
- **风险**: 密钥泄露导致身份伪造
- **修复**: 从环境变量读取

### 中危问题
...

### 修复优先级
1. 立即修复：高危问题
2. 本周修复：中危问题
3. 下次迭代：低危问题
```

---

## 🚀 使用方式

### 方式一：全量审计

```
对当前项目执行安全审计
```

扫描整个代码库，生成完整安全报告。

### 方式二：增量审计

```
审计本次变更的安全问题
git diff 与 main 分支对比
```

只检查新增/修改的代码，适合 CI/CD 集成。

### 方式三：特定文件审计

```
安全审计 src/auth/login.py
重点关注：认证逻辑、会话管理
```

### 方式四：修复模式

```
审计并修复安全问题
自动生成修复代码
```

---

## 🔧 CI/CD 集成

```yaml
# .github/workflows/security-audit.yml
name: Security Audit
on: [pull_request]
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: CodeQL Analysis
        uses: github/codeql-action/init@v3
      - name: Semgrep Scan
        uses: returntocorp/semgrep-action@v1
      - name: Secret Scan
        uses: trufflesecurity/trufflehog@main
```

---

## 🆚 与其他 Skill 的关系

**最佳实践链**：
```
编码阶段 → multi-agent-orchestration（Security Agent 审计）
    → security-audit（深度漏洞扫描）
    → confidence-check（评估修复方案可信度）
    → test-driven-development（安全测试用例）
    → git-commit（规范提交安全修复）
    → hermes-experience（沉淀安全经验）
```

---

## 💡 最佳实践

### DO
- ✅ 每次 PR 前执行安全审计
- ✅ 高危问题阻塞合并
- ✅ 定期扫描依赖库 CVE
- ✅ 密钥使用专门管理工具（Vault/AWS Secrets）
- ✅ 安全测试纳入自动化测试

### DON'T
- ❌ 忽视低危问题（累积成高危）
- ❌ 在生产环境调试信息
- ❌ 自己实现加密算法
- ❌ 信任用户输入（永远校验）

---

> "安全不是一次性的检查，而是持续的过程。每个 commit 都应该是安全的。"
