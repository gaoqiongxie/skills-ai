---
name: "mcp-builder"
description: "MCP Server / Tool 构建指南：把内部 Java API、OpenSpec 后端接口规范或 Lark OpenAPI 封装成符合 Model Context Protocol 的 Tool / Resource / Prompt，让 Claude Code、Cursor、Codex 等 AI 客户端通过标准 JSON-RPC 调用本地或远程能力。当用户说'MCP'、'Model Context Protocol'、'MCP Server'、'封装成 MCP'、'MCP Tool'、'MCP 工具定义'、'stdio'、'SSE'、'JSON-RPC'时触发。核心特点：协议对齐、传输协议选择、安全边界、与现有 API 工作流无缝对接。"
---

> **来源**: modelcontextprotocol/specification + Anthropic 官方文档 + 社区最佳实践
>
> **发布时间**: 2026-08
>
> **理念**: "把你的系统能力，变成 AI 能安全调用的标准接口。"

# 🔌 MCP Builder — MCP Server / Tool 构建指南

把现有 API、数据库、文档系统或内部服务封装成 **Model Context Protocol (MCP)** 标准接口，让 AI 客户端以统一方式发现、调用和组合你的能力。

---

## 为什么需要 MCP

| 问题 | 没有 MCP | 有 MCP |
|------|---------|--------|
| 每个 AI 工具集成方式不同 | 重复造轮子 | 一套协议通吃 Claude Code / Cursor / Codex / Windsurf |
| AI 不知道你的系统有什么能力 | 靠 prompt 硬编码 | Server 自动暴露 Tools / Resources / Prompts |
| 权限边界模糊 | 容易过度授权 | 客户端按能力粒度申请，Server 只开放必要接口 |
| 上下文碎片化 | 每次把文档贴进对话 | Resources 按需拉取最新上下文 |

**一句话**：MCP 是 AI 时代的「USB-C」，让你的系统能力即插即用。

---

## 核心技术栈

```
Model Context Protocol  # 协议规范
JSON-RPC 2.0            # 通信格式
stdio / SSE / HTTP      # 传输层
Tools                   # AI 可调用的函数
Resources               # AI 可读取的上下文/文档
Prompts                 # 可复用的提示词模板
Sampling                # Server 请求 LLM 补全的能力
```

### 协议三要素

| 要素 | 作用 | 示例 |
|------|------|------|
| **Tools** | AI 调用以执行动作 | `create_user`、`query_order`、`deploy_service` |
| **Resources** | AI 读取以获取上下文 | `openapi.json`、`database_schema.md`、`api_doc` |
| **Prompts** | 预置可复用的提示词模板 | `code_review_template`、`incident_response_template` |

---

## 项目结构模板

```
my-mcp-server/
├── src/
│   ├── index.ts              # Server 入口
│   ├── tools/                # Tool 定义与实现
│   │   ├── users.ts
│   │   └── orders.ts
│   ├── resources/            # Resource 定义
│   │   └── api-docs.ts
│   ├── prompts/              # Prompt 模板
│   │   └── code-review.ts
│   └── utils/
│       └── errors.ts
├── package.json
├── tsconfig.json
└── claude_config.json        # Claude Code 本地配置（可选）
```

---

## 开发到接入全链路

### Step 1：选择传输协议

| 协议 | 适用场景 | 特点 |
|------|---------|------|
| **stdio** | 本地 CLI 工具、内部脚本 | 最简单，进程级隔离 |
| **SSE** | 远程服务、多客户端共享 | 需要 HTTP 服务端，支持流式推送 |
| **HTTP (Streamable)** | 企业内网、微服务 | 与现有网关/鉴权体系集成 |

**新手建议**：先用 `stdio`，5 分钟跑通第一个 Tool。

---

### Step 2：定义你的第一个 Tool

以把内部用户查询 API 封装为 MCP Tool 为例：

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { CallToolRequestSchema, ListToolsRequestSchema } from "@modelcontextprotocol/sdk/types.js";

const server = new Server(
  { name: "user-service-mcp", version: "1.0.0" },
  { capabilities: { tools: {} } }
);

// 1. 声明 Tool 列表
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "query_user",
        description: "根据用户 ID 或手机号查询用户信息",
        inputSchema: {
          type: "object",
          properties: {
            userId: { type: "string", description: "用户唯一 ID" },
            phone: { type: "string", description: "用户手机号" }
          },
          anyOf: [{ required: ["userId"] }, { required: ["phone"] }]
        }
      }
    ]
  };
});

// 2. 实现 Tool 调用
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  if (request.params.name === "query_user") {
    const { userId, phone } = request.params.arguments || {};
    const user = await fetchUserFromBackend({ userId, phone });
    return {
      content: [{ type: "text", text: JSON.stringify(user, null, 2) }]
    };
  }
  throw new Error(`Unknown tool: ${request.params.name}`);
});

// 3. 启动 stdio 传输
const transport = new StdioServerTransport();
await server.connect(transport);
```

---

### Step 3：在 Claude Code 中接入

```json
// ~/.claude/settings.json 或项目级 .claude/settings.json
{
  "mcpServers": {
    "user-service": {
      "command": "node",
      "args": ["D:/work/my-mcp-server/dist/index.js"]
    }
  }
}
```

接入后，Claude Code 会自动：
1. 读取 `ListTools` 发现能力
2. 在需要时调用对应 Tool
3. 把 Tool 结果作为上下文继续推理

---

### Step 4：安全加固

| 风险 | 防护措施 |
|------|---------|
| 越权调用 | 每个 Tool 显式声明 required 字段，服务端二次校验 |
| 敏感数据泄露 | Resource 设置只读，避免返回密码/Token/密钥 |
| 误操作 | 写操作 Tool 增加 `confirm: true` 或要求人工确认 |
| 供应链污染 | 固定 SDK 版本，审计 Server 依赖 |
| 网络暴露 | stdio 不外网监听；SSE/HTTP 走网关 + OAuth |

**黄金规则**：
- 默认只读，写操作显式授权
- 每个 Tool 的 `description` 必须清晰说明副作用
- 不在 Tool 结果中返回内部系统路径或密钥

---

## 使用示例

### 示例 1：把 OpenSpec 后端接口封装为 MCP Tools

```typescript
// 假设已有 OpenSpec 规范 /openapi.yaml
// 自动生成 MCP Tool 定义

import yaml from "js-yaml";
import fs from "fs";

const spec = yaml.load(fs.readFileSync("./openapi.yaml", "utf8"));

const tools = Object.entries(spec.paths).flatMap(([path, methods]) =>
  Object.entries(methods).map(([method, op]) => ({
    name: `${method}_${path.replace(/\//g, "_")}`,
    description: op.summary,
    inputSchema: op.requestBody?.content?.["application/json"]?.schema || { type: "object" }
  }))
);

server.setRequestHandler(ListToolsRequestSchema, async () => ({ tools }));
```

**最佳组合**：
- `openspec-sdd` 设计并输出 OpenSpec
- `mcp-builder` 把 OpenSpec 自动转换为 MCP Tools
- `api-doc-generator` 生成配套 API 文档

---

### 示例 2：把 Lark OpenAPI 封装为 MCP Resources

```typescript
server.setRequestHandler(ListResourcesRequestSchema, async () => {
  return {
    resources: [
      {
        uri: "lark://docs/meeting-notes",
        name: "会议纪要汇总",
        mimeType: "application/json",
        description: "从飞书文档拉取最近会议纪要"
      }
    ]
  };
});

server.setRequestHandler(ReadResourceRequestSchema, async (request) => {
  if (request.params.uri === "lark://docs/meeting-notes") {
    const notes = await fetchLarkDocs();
    return { contents: [{ uri: request.params.uri, mimeType: "application/json", text: JSON.stringify(notes) }] };
  }
});
```

**最佳组合**：
- `lark-doc` / `lark-wiki` 读取飞书内容
- `mcp-builder` 把 Lark 能力暴露为 MCP Resource
- `memory-hub` 把读取到的内容沉淀为项目记忆

---

### 示例 3：Prompt 模板 —— 代码审查

```typescript
server.setRequestHandler(ListPromptsRequestSchema, async () => {
  return {
    prompts: [
      {
        name: "pr_code_review",
        description: "根据 PR diff 生成结构化代码审查意见",
        arguments: [
          { name: "diff", description: "PR diff 文本", required: true }
        ]
      }
    ]
  };
});

server.setRequestHandler(GetPromptRequestSchema, async (request) => {
  if (request.params.name === "pr_code_review") {
    return {
      messages: [
        {
          role: "user",
          content: {
            type: "text",
            text: `请对以下 PR diff 进行代码审查，关注：安全性、性能、可维护性、边界处理。\n\n${request.params.arguments.diff}`
          }
        }
      ]
    };
  }
});
```

---

## 调试技巧

```bash
# 1. 直接运行 Server 看输出
node dist/index.js

# 2. 用官方 inspector 可视化调试
npx @anthropic-ai/mcp-inspector node dist/index.js

# 3. 在 Claude Code 中查看已加载 Tools
# 输入："你有哪些工具可用？"

# 4. 手动触发一个 Tool 调用
# 输入："调用 query_user，userId 为 123"
```

---

## 快速入口

```
"封装个 MCP"          → 从 0 创建一个 stdio MCP Server
"把 API 转成 MCP"     → OpenSpec / Java API → MCP Tools
"MCP 安全怎么做"      → 权限边界 + 只读默认 + 写确认
"接入 Claude Code"    → settings.json 配置 + 自动发现 Tool
"Lark 接口 MCP 化"    → Lark OpenAPI → MCP Resources
```

---

## 与其他 Skill 的关系

| Skill | 关系 | 协作场景 |
|-------|------|---------|
| **openspec-sdd** | 前置 | 用 OpenSpec 设计接口，再用 `mcp-builder` 转为 MCP |
| **api-doc-generator** | 互补 | `api-doc-generator` 生成文档，`mcp-builder` 生成可调用接口 |
| **lark-openapi-explorer** | 互补 | 发现 Lark 原生 API，`mcp-builder` 负责协议封装 |
| **security-audit** | 质量保障 | 对 MCP Server 做安全审计，防止工具投毒和越权 |
| **memory-hub** | 下游 | MCP 读取的上下文沉淀到统一记忆中枢 |

**最佳实践链**：
```
openspec-sdd（设计接口契约）
  → api-doc-generator（生成文档）
  → mcp-builder（封装为 MCP Server）
  → security-audit（审计 Tool 权限）
  → memory-hub（沉淀上下文）
```

---

> "MCP 不是又一个集成框架，而是让 AI 真正理解你系统能力的通用语言。"
