---
name: "cloudflare-worker"
description: "Cloudflare Worker边缘函数构建指南：用Wrangler CLI开发、调试、部署Serverless函数，实现轻量API/边缘缓存/中间层/反向代理。当用户说'写个Worker'、'边缘函数'、'Cloudflare部署'、'Serverless API'、'轻量后端'、'边缘计算'、'CF Worker'时触发。核心特点：Wrangler工作流、边缘环境特性、KV/DO/R2存储、TypeScript最佳实践、本地调试到部署全链路。"
---

> **来源**: 基于 Cloudflare Workers 官方文档 + 社区最佳实践
>
> **发布时间**: 2026-05-29
>
> **理念**: "在距离用户最近的地方运行代码。"

# ☁️ Cloudflare Worker — 边缘函数构建指南

用 **Cloudflare Workers** 在边缘节点运行 JavaScript/TypeScript——轻量 API、中间层、缓存、反向代理，零服务器维护。

---

## 🎯 为什么用 Cloudflare Workers

| 对比项 | 传统服务器 (EC2/VPS) | Cloudflare Workers |
|--------|---------------------|-------------------|
| **部署复杂度** | 需配环境、装依赖、启服务 | 一条命令部署 |
| **冷启动** | 秒级 | 毫秒级（甚至零冷启动） |
| **地理分布** | 单区域/多区复制 | 全球 300+ 边缘节点 |
| **成本** | 按月付费，闲置也花钱 | 按请求计费，免费额度 generous |
| **SSL/域名** | 需手动配置 | 自动 HTTPS + 自定义域名 |
| **扩展性** | 需配置自动伸缩 | 自动无限扩展 |
| **适用场景** | 重计算、长连接 | 轻量 API、中间层、边缘逻辑 |

**一句话**：不适合跑数据库和重计算，适合跑**逻辑层**——鉴权、转发、缓存、轻量计算。

---

## 🛠️ 核心技术栈

```
Wrangler CLI      # 开发、调试、部署工具
TypeScript        # 类型安全
Hono / itty-router # 轻量 Web 框架（可选）
Cloudflare KV     # 键值存储
Durable Objects   # 有状态对象（协作/游戏/计数）
R2                # S3 兼容对象存储
D1                # 边缘 SQLite 数据库
```

### Workers 运行环境特性

```javascript
// ⚠️ 不是 Node.js！是 V8 Isolate
// 支持的 API：
fetch()           // ✅ 原生支持
Request/Response  // ✅ Web 标准
WebSocket         // ✅ 原生支持
URL/URLSearchParams // ✅ Web 标准
crypto.subtle     // ✅ Web Crypto
setTimeout/Interval // ✅ 但精度有限

// ❌ 不支持的 API：
require()         // ❌ 用 ES Module
fs                // ❌ 无文件系统，用 KV/R2
process.env       // ❌ 用 env 绑定
child_process     // ❌ 无子进程
```

---

## 📁 项目结构模板

```
my-worker/
├── src/
│   ├── index.ts          # Worker 入口
│   ├── routes/           # 路由模块
│   │   ├── api.ts        # API 路由
│   │   └── proxy.ts      # 代理路由
│   ├── middleware/       # 中间件
│   │   ├── auth.ts       # 鉴权
│   │   ├── cors.ts       # 跨域
│   │   └── rateLimit.ts  # 限流
│   ├── handlers/         # 业务处理器
│   │   ├── user.ts
│   │   └── order.ts
│   └── utils/
│       └── response.ts   # 统一响应格式
├── wrangler.toml         # Wrangler 配置文件
├── package.json
├── tsconfig.json
└── .dev.vars             # 本地环境变量
```

---

## 🚀 开发到部署全链路

### Step 1: 初始化项目

```bash
# 使用 Wrangler 创建项目
npx wrangler init my-worker --template cloudflare-workers

# 或用 Hono 框架快速启动
npm create hono@latest my-worker
# 选择 cloudflare-workers 模板
```

### Step 2: 编写 Worker（TypeScript）

```typescript
// src/index.ts
export interface Env {
  KV_CACHE: KVNamespace;      // KV 绑定
  R2_BUCKET: R2Bucket;        // R2 绑定
  D1_DB: D1Database;          // D1 绑定
  API_SECRET: string;         // 密钥
}

export default {
  async fetch(request: Request, env: Env, ctx: ExecutionContext): Promise<Response> {
    const url = new URL(request.url);
    
    // 1. CORS 处理
    if (request.method === 'OPTIONS') {
      return new Response(null, {
        headers: {
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE',
          'Access-Control-Allow-Headers': 'Content-Type, Authorization',
        }
      });
    }
    
    // 2. 路由分发
    try {
      if (url.pathname.startsWith('/api/')) {
        return await handleApi(request, env, ctx);
      }
      
      if (url.pathname.startsWith('/proxy/')) {
        return await handleProxy(request, env);
      }
      
      return jsonResponse({ error: 'Not Found' }, 404);
    } catch (err) {
      return jsonResponse({ error: err.message }, 500);
    }
  }
};

// 统一 JSON 响应
function jsonResponse(data: any, status = 200): Response {
  return new Response(JSON.stringify(data), {
    status,
    headers: {
      'Content-Type': 'application/json',
      'Access-Control-Allow-Origin': '*',
    }
  });
}

// API 处理器
async function handleApi(request: Request, env: Env, ctx: ExecutionContext): Promise<Response> {
  const url = new URL(request.url);
  
  // GET /api/users
  if (url.pathname === '/api/users' && request.method === 'GET') {
    const cache = await env.KV_CACHE.get('users');
    if (cache) {
      return jsonResponse({ data: JSON.parse(cache), cached: true });
    }
    
    const users = await fetchUsersFromD1(env.D1_DB);
    ctx.waitUntil(env.KV_CACHE.put('users', JSON.stringify(users), { expirationTtl: 300 }));
    
    return jsonResponse({ data: users, cached: false });
  }
  
  // POST /api/users
  if (url.pathname === '/api/users' && request.method === 'POST') {
    const body = await request.json();
    const result = await createUser(env.D1_DB, body);
    await env.KV_CACHE.delete('users');  // 清除缓存
    return jsonResponse({ data: result }, 201);
  }
  
  return jsonResponse({ error: 'Method not allowed' }, 405);
}

// 反向代理处理器
async function handleProxy(request: Request, env: Env): Promise<Response> {
  const url = new URL(request.url);
  const targetUrl = url.pathname.replace('/proxy/', '');
  
  const modifiedRequest = new Request(targetUrl, request);
  const response = await fetch(modifiedRequest);
  
  // 添加缓存头
  const modifiedResponse = new Response(response.body, response);
  modifiedResponse.headers.set('Cache-Control', 'max-age=3600');
  
  return modifiedResponse;
}
```

### Step 3: 配置 wrangler.toml

```toml
name = "my-worker"
main = "src/index.ts"
compatibility_date = "2026-05-29"

# 环境变量（生产环境）
[vars]
API_VERSION = "v1"

# KV 命名空间绑定
[[kv_namespaces]]
binding = "KV_CACHE"
id = "your-kv-namespace-id"

# R2 存储桶绑定
[[r2_buckets]]
binding = "R2_BUCKET"
bucket_name = "my-bucket"

# D1 数据库绑定
[[d1_databases]]
binding = "D1_DB"
database_name = "my-db"
database_id = "your-d1-database-id"

# 密钥（不在代码中硬编码）
[secrets]
API_SECRET = "your-secret-key"
```

### Step 4: 本地开发调试

```bash
# 启动本地开发服务器
npx wrangler dev

# 带环境变量启动
npx wrangler dev --env local

# 查看实时日志
npx wrangler tail
```

**本地测试**：
```bash
curl http://localhost:8787/api/users
curl -X POST http://localhost:8787/api/users \
  -H "Content-Type: application/json" \
  -d '{"name":"张三","email":"zhangsan@example.com"}'
```

### Step 5: 部署上线

```bash
# 部署到 Cloudflare
npx wrangler deploy

# 部署到特定环境
npx wrangler deploy --env production

# 查看部署状态
npx wrangler status
```

---

## 💡 使用示例

### 示例 1：轻量 API 中间层（鉴权+缓存）

```typescript
// 场景：前端直调用第三方 API 不安全，用 Worker 做中间层

export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    // 1. 鉴权
    const auth = request.headers.get('Authorization');
    if (!auth || !verifyToken(auth, env.API_SECRET)) {
      return new Response('Unauthorized', { status: 401 });
    }
    
    // 2. 检查缓存
    const cacheKey = `api:${request.url}`;
    const cached = await env.KV_CACHE.get(cacheKey);
    if (cached) {
      return new Response(cached, {
        headers: { 'Content-Type': 'application/json', 'X-Cache': 'HIT' }
      });
    }
    
    // 3. 转发到后端
    const response = await fetch('https://api.backend.com' + new URL(request.url).pathname, {
      method: request.method,
      headers: {
        'Authorization': `Bearer ${env.BACKEND_TOKEN}`,
        'Content-Type': 'application/json',
      },
      body: request.body,
    });
    
    const data = await response.text();
    
    // 4. 缓存结果（5分钟）
    await env.KV_CACHE.put(cacheKey, data, { expirationTtl: 300 });
    
    return new Response(data, {
      headers: { 'Content-Type': 'application/json', 'X-Cache': 'MISS' }
    });
  }
};
```

---

### 示例 2：边缘图片处理（缩略图+WebP转换）

```typescript
export default {
  async fetch(request: Request, env: Env): Promise<Response> {
    const url = new URL(request.url);
    const imagePath = url.pathname.slice(1); // 去掉开头的 /
    const width = url.searchParams.get('w');
    const format = url.searchParams.get('format') || 'webp';
    
    // 从 R2 获取原图
    const object = await env.R2_BUCKET.get(imagePath);
    if (!object) {
      return new Response('Not found', { status: 404 });
    }
    
    // 使用 Cloudflare Images API 进行转换（需绑定）
    // 或直接用 Canvas API 处理（简单缩放）
    
    const headers = new Headers();
    object.writeHttpMetadata(headers);
    headers.set('etag', object.httpEtag);
    headers.set('Content-Type', `image/${format}`);
    headers.set('Cache-Control', 'public, max-age=31536000');
    
    return new Response(object.body, { headers });
  }
};
```

---

### 示例 3：Durable Objects 实时协作（计数器/白板）

```typescript
// Durable Object 类
export class CollaborationRoom {
  constructor(state: DurableObjectState, env: Env) {
    this.state = state;
    this.env = env;
  }
  
  async fetch(request: Request): Promise<Response> {
    const url = new URL(request.url);
    
    if (url.pathname === '/increment') {
      // 持久化状态存储
      let current = await this.state.storage.get('count') || 0;
      current++;
      await this.state.storage.put('count', current);
      return new Response(JSON.stringify({ count: current }));
    }
    
    if (url.pathname === '/websocket') {
      // 升级 WebSocket
      const [client, server] = Object.values(new WebSocketPair());
      this.state.acceptWebSocket(server);
      return new Response(null, { status: 101, webSocket: client });
    }
    
    return new Response('Not found', { status: 404 });
  }
}
```

---

## 🧪 调试技巧

```bash
# 本地日志
console.log()  # 在 wrangler dev 中会输出到终端

# 查看生产日志
npx wrangler tail

# 使用 wrangler 调试器
npx wrangler dev --inspect

# 测试特定路由
curl -v https://your-worker.your-subdomain.workers.dev/api/test
```

---

## 🚀 快速入口

```
"写个Worker" → Cloudflare Worker 项目初始化 + Hello World
"边缘函数" → 轻量 API / 中间层 / 边缘逻辑
"Cloudflare部署" → Wrangler init → dev → deploy 全链路
"Serverless API" → TypeScript + KV缓存 + D1数据库
"轻量后端" → 鉴权 + 转发 + 缓存 中间层模式
"边缘计算" → 全球边缘节点 + 就近执行
"CF Worker" → 代码 + 配置 + 部署 一站式
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 协作场景 |
|-------|------|---------|
| **api-doc-generator** | 前置 | `api-doc-generator` 生成接口文档，本 Skill 实现边缘层接口 |
| **database-designer** | 互补 | `database-designer` 设计数据库，本 Skill 用 D1/R2 做边缘存储 |
| **backend-change-flow** | 互补 | 本 Skill 适合轻量边缘逻辑，重业务逻辑仍用 `backend-change-flow` |
| **web-artifacts-builder** | 平行 | 本 Skill 是后端/边缘，`web-artifacts-builder` 是前端 |

**最佳实践链**：
```
api-doc-generator（设计接口）
  → cloudflare-worker（实现边缘API）
  → web-artifacts-builder（前端消费API）
  → quality-gate（提交检查）
```

---

> "在距离用户最近的地方运行代码——这就是边缘计算的浪漫。"
