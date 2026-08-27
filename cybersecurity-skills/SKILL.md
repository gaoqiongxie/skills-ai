---
name: "cybersecurity-skills"
description: "网络安全分析师技能库：754个结构化安全技能，覆盖威胁狩猎、数字取证、事件响应、渗透测试、代码安全审计、威胁情报、恶意软件分析等26个安全领域。映射MITRE ATT&CK v19.1、NIST CSF 2.0等五大框架。当用户说'安全分析'、'威胁狩猎'、'威胁情报'、'渗透测试'、'事件响应'、'MITRE'、'数字取证'、'恶意软件分析'、'红队'、'蓝队'、'SOC'、'网络攻防'时触发。与security-audit互补：security-audit聚焦代码层静态扫描，本Skill覆盖全栈安全分析工作流。"
---

> **来源**: mukul975/cybersecurity-skills + MITRE/NIST 框架 + 安全社区实践
>
> **发布时间**: 2026-06
>
> **理念**: "安全不是工具，是系统化的思维方式。"

# Cybersecurity Skills — 网络安全分析师技能库

754 个结构化网络安全技能，赋予 AI 「Senior Analyst」级别的全栈安全分析能力。

---

## 功能介绍

本 Skill 将网络安全领域沉淀为 754 个可结构化调用的技能单元，覆盖从威胁狩猎到数字取证、从红队渗透到蓝队防御的完整安全运营生命周期。每个技能单元包含：

- **知识域定义**：该技能的边界与核心概念
- **操作步骤**：可执行的分析/检测/响应流程
- **工具链映射**：对应的开源/商业工具
- **框架对齐**：与 MITRE ATT&CK、NIST CSF 等框架的映射关系
- **检测规则/签名**：可落地的 IoC/行为检测逻辑
- **输出模板**：标准化的分析报告格式

渐进式加载设计确保在 500-2000 tokens 内完成核心能力注入，避免上下文窗口溢出。

---

## 核心技术栈

### 分析方法论

| 方法 | 说明 |
|------|------|
| **假设驱动调查 (HDI)** | 基于假设 → 证据收集 → 验证/否定 → 迭代 |
| **钻石模型 (Diamond Model)** |  adversary / infrastructure / capability / victim 四维分析 |
| **杀伤链分析 (Cyber Kill Chain)** | 侦察 → 武器化 → 投递 → 利用 → 安装 → C2 → 行动 |
| **ATT&CK 战术映射** | 将观测行为映射到标准战术技术矩阵 |
| **时间线重构** | 基于日志/取证数据重建事件时序 |

### 工具链生态

```
威胁狩猎: YARA / Sigma / Splunk / Elastic SIEM / Velociraptor
数字取证: Autopsy / Volatility / Rekall / SANS SIFT
恶意分析: Cuckoo Sandbox / REMnux / Ghidra / IDA Pro / x64dbg
渗透测试: Metasploit / Cobalt Strike / Burp Suite / Nmap / BloodHound
威胁情报: MISP / OpenCTI / VirusTotal / Abuse.ch / AlienVault OTX
日志分析: Splunk / ELK Stack / Graylog / Apache Kafka
网络监控: Zeek / Suricata / Wireshark / NetworkMiner
云安全: Prowler / ScoutSuite / CloudTrail / GuardDuty
容器安全: Trivy / Falco / Sysdig / Anchore
```

---

## 五大框架映射

### MITRE ATT&CK v19.1 (企业矩阵)

| 战术 (Tactic) | 技术数量 | 核心应用场景 |
|--------------|---------|------------|
| 初始访问 (Initial Access) | 11 | 钓鱼分析、边界突破检测 |
| 执行 (Execution) | 15 | 脚本分析、命令行取证 |
| 持久化 (Persistence) | 20 | 后门检测、启动项审计 |
| 权限提升 (Privilege Escalation) | 15 | UAC 绕过、Sudo 滥用 |
| 防御规避 (Defense Evasion) | 42 | 无文件攻击、Rootkit 检测 |
| 凭证访问 (Credential Access) | 19 | Hash dump、Kerberoasting |
| 发现 (Discovery) | 32 | 内网侦察、资产发现 |
| 横向移动 (Lateral Movement) | 13 | Pass-the-Hash、RDP 劫持 |
| 收集 (Collection) | 19 | 数据收集行为检测 |
| C2 (Command and Control) | 22 |  beacon 检测、DNS 隧道 |
| 数据渗出 (Exfiltration) | 11 | DLP 绕过、加密传输 |
| 影响 (Impact) | 15 | 勒索软件、数据破坏 |

### NIST CSF 2.0

| 核心功能 | 安全领域覆盖 |
|---------|------------|
| **识别 (GV/ID)** | 资产管理、风险评估、供应链安全 |
| **保护 (PR)** | 访问控制、数据安全、防护技术 |
| **检测 (DE)** | 异常检测、持续监控、检测流程 |
| **响应 (RS)** | 响应计划、通信、分析、缓解 |
| **恢复 (RC)** | 恢复计划、改进、通信 |
| **治理 (GV)** | 网络安全战略、政策、监督 |

### MITRE ATLAS v5.4 (AI 安全)

| 战术 | AI 特定威胁 |
|------|-----------|
| 侦察 | 模型架构探测、训练数据推断 |
| 资源开发 | 投毒数据集、对抗样本生成 |
| 初始访问 | ML 供应链污染、模型仓库投毒 |
| ML 模型访问 | 模型窃取、API 滥用 |
| ML 攻击阶段 | 对抗逃逸、模型逆向、成员推断 |

### MITRE D3FEND v1.3 (防御技术)

| 防御类别 | 技术示例 |
|---------|---------|
| 硬化 (Harden) | 应用隔离、代码签名验证 |
| 检测 (Detect) | 文件分析、流量分析、进程监控 |
| 隔离 (Isolate) | 网络分段、执行隔离 |
| 欺骗 (Deceive) | 蜜罐、DNS 陷阱 |
| 驱逐 (Evict) | 会话终止、进程终止 |

### NIST AI RMF 1.0

| 功能 | 安全映射 |
|------|---------|
| 治理 (Govern) | AI 安全策略、角色责任 |
| 映射 (Map) | AI 系统风险识别 |
| 测量 (Measure) | 对抗鲁棒性测试 |
| 管理 (Manage) | AI 事件响应计划 |

---

## 26 个安全领域速查

| 领域 | 技能数 | 核心能力 |
|------|-------|---------|
| Cloud Security | 60 | AWS/Azure/GCP 配置审计、IAM 分析、存储桶安全 |
| Threat Hunting | 55 | 假设驱动狩猎、行为分析、异常检测 |
| Threat Intelligence | 50 | IoC 管理、TTP 分析、情报评估 |
| Web App Security | 42 | OWASP、WAF 调优、API 安全 |
| Malware Analysis | 39 | 静态/动态分析、逆向工程、行为提取 |
| Digital Forensics | 37 | 磁盘取证、内存取证、日志分析 |
| Incident Response | 25 | IR 流程、遏制策略、证据保全 |
| Red Teaming | 24 | 攻击链设计、OPSEC、后渗透 |
| Container Security | 30 | 镜像扫描、运行时防护、K8s 安全 |
| OT/ICS Security | 28 | 工控协议、SCADA 安全、Modbus 分析 |
| Network Security | 35 | 流量分析、IDS/IPS、网络分段 |
| Endpoint Security | 32 | EDR 分析、主机取证、行为阻断 |
| Identity Security | 28 | AD 安全、IAM、零信任架构 |
| Data Security | 25 | 数据分类、DLP、加密策略 |
| Application Security | 30 | SDL、SAST/DAST、依赖安全 |
| Vulnerability Management | 22 | 漏洞评估、优先级排序、补丁管理 |
| Security Architecture | 20 | 安全域设计、纵深防御、安全建模 |
| Risk Management | 18 | 风险评估、合规映射、业务影响分析 |
| Compliance & GRC | 18 | SOC2/ISO27001/等保合规 |
| Security Operations (SOC) | 25 | SIEM 运营、告警分级、值班流程 |
| Penetration Testing | 28 | 外网/内网/无线/社工测试 |
| Social Engineering | 15 | 钓鱼测试、心理操控分析 |
| Wireless Security | 12 | WiFi 审计、蓝牙安全、RF 分析 |
| Cryptography | 18 | 算法分析、密钥管理、PKI |
| OSINT | 20 | 开源情报收集、资产暴露面分析 |
| AI/ML Security | 22 | 对抗样本、模型安全、AIGC 风险 |

---

## 使用示例

### 示例一：威胁狩猎 (Threat Hunting)

```
用户: 帮我进行一次威胁狩猎，最近发现内网有几台机器行为异常

AI (激活 cybersecurity-skills):
1. 定义狩猎假设
   - 假设: 内网存在横向移动行为
   - 依据: 多主机异常网络连接模式

2. 数据收集范围
   - 源: EDR 遥测、DNS 日志、认证日志、网络流量
   - 时间窗口: 过去 7 天

3. 狩猎查询 (Sigma 规则思路)
   - 检测: 同一凭证多主机登录
   - 检测: 非标准端口上的 SMB/RDP 流量
   - 检测: PowerShell 远程执行痕迹

4. ATT&CK 映射
   - T1021.002 (SMB/Windows Admin Shares)
   - T1021.001 (Remote Desktop Protocol)
   - T1059.001 (PowerShell)

5. 输出: 威胁狩猎报告
   - 发现: 3 台主机存在 PsExec 使用痕迹
   - 置信度: 高
   - 建议: 隔离主机、重置凭证、深度取证
```

### 示例二：事件响应 (Incident Response)

```
用户: 服务器被入侵了，怎么响应？

AI (激活 cybersecurity-skills):
1. 准备阶段 (Preparation)
   - 确认 IR 团队成员与联系方式
   - 准备取证工具包和隔离环境

2. 识别阶段 (Identification)
   - 确认入侵指标: 异常进程、未知用户、异常网络连接
   - 评估影响范围: 受影响系统、数据类型
   - 初步分类: P1(紧急)/P2(高)/P3(中)/P4(低)

3. 遏制阶段 (Containment)
   - 短期遏制: 隔离受感染主机、阻断 C2 通信
   - 长期遏制: 加固相似系统、部署检测规则

4. 根除阶段 (Eradication)
   - 清除恶意软件、后门、持久化机制
   - 修复漏洞入口点

5. 恢复阶段 (Recovery)
   - 逐步恢复系统上线
   - 加强监控验证

6. 总结阶段 (Lessons Learned)
   - 时间线重构
   - 改进建议
```

### 示例三：代码安全审计

```
用户: 审计这段 Python 代码的安全问题

def login(username, password):
    query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
    return db.execute(query)

AI (激活 cybersecurity-skills):
1. 漏洞识别
   - [HIGH] SQL 注入 (A03:2021 - Injection)
   - [HIGH] 明文密码比对 (A07:2021 - Identification and Authentication Failures)

2. 攻击向量分析
   - 输入: username = "admin' --"
   - 结果: 绕过认证

3. 修复方案
   ```python
   def login(username, password):
       query = "SELECT * FROM users WHERE username = %s"
       user = db.execute(query, (username,))
       if user and bcrypt.checkpw(password.encode(), user['password_hash']):
           return user
       return None
   ```

4. 纵深防御建议
   - 输入验证 (白名单)
   - 参数化查询 (永远)
   - 密码哈希 (bcrypt/Argon2)
   - 失败锁定 (防暴力破解)
   - 审计日志 (记录登录尝试)
```

---

## 快速入口

### 按场景选择技能集

| 场景 | 激活指令 | 加载技能数 |
|------|---------|-----------|
| 威胁狩猎 | "开始威胁狩猎" / "hunt for threats" | 55 |
| 事件响应 | "启动事件响应" / "incident response" | 25 |
| 恶意分析 | "分析这个样本" / "malware analysis" | 39 |
| 渗透测试 | "渗透测试方案" / "red team assessment" | 24 |
| 取证调查 | "数字取证" / "digital forensics" | 37 |
| 威胁情报 | "分析威胁情报" / "threat intelligence" | 50 |
| 云安全审计 | "云安全评估" / "cloud security audit" | 60 |
| 代码审计 | "代码安全审计" / "secure code review" | 30 |
| 网络监控 | "网络流量分析" / "network analysis" | 35 |
| 合规检查 | "安全合规评估" / "compliance check" | 18 |

### 按框架查询

```
"MITRE ATT&CK T1059" → 返回命令行接口技术详情
"NIST CSF DE.AE" → 返回异常事件检测要求
"D3FEND D3-DA" → 返回数据流分析防御技术
```

---

## 与其他 Skill 的关系

```
安全分析工作流:

代码开发阶段
    ├── security-audit (代码层安全审计)
    │       └── 聚焦: CodeQL / Semgrep / OWASP Top 10
    │       └── 场景: 静态代码扫描、依赖漏洞检测
    │
    └── cybersecurity-skills (本 Skill)
            └── 聚焦: 全栈安全分析工作流
            └── 场景: 威胁狩猎、事件响应、取证分析、渗透测试

互补关系:
- security-audit 回答 "这段代码有什么漏洞"
- cybersecurity-skills 回答 "这个系统怎么被攻击的、怎么检测、怎么响应"

联动使用:
1. security-audit 发现代码漏洞
2. cybersecurity-skills 评估漏洞利用路径 (ATT&CK 映射)
3. cybersecurity-skills 设计检测规则 (Sigma/YARA)
4. cybersecurity-skills 制定应急响应预案
```

---

## 渐进式加载说明

本 Skill 采用分层加载策略，根据用户请求自动选择加载深度：

| 层级 | Tokens | 内容 |
|------|--------|------|
| L1 (快速响应) | ~500 | 核心框架映射 + 相关领域技能索引 |
| L2 (标准分析) | ~1000 | 完整方法论 + 工具链 + 检测逻辑 |
| L3 (深度调查) | ~2000 | 全量 754 技能按需加载 + 实战案例 |

---

> "安全不是产品的堆砌，而是系统化思维的训练。每一个告警背后，都有一个完整的故事等待被还原。"
