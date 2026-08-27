---
name: "devops-toolchain"
description: "DevOps工具链实战指南：Docker/Kubernetes/Terraform/GitHub Actions 的本地开发、CI/CD、部署与运维。当用户说'DevOps'、'Docker'、'Kubernetes'、'K8s'、'Terraform'、'GitHub Actions'、'CI/CD'、'部署'、'容器化'、'Helm'、'IaC'、'基础设施'、'运维'时触发。核心特点：从本地容器到生产K8s的完整链路、IaC最佳实践、GitOps部署、与质量门控/并行开发联动。"
---

> **来源**: containers/kubernetes-mcp-server + hashicorp/terraform-mcp-server + alirezarezvani/claude-skills + 社区最佳实践
>
> **发布时间**: 2026-08
>
> **理念**: "一次把应用包好，任何地方都能跑；一次把基础设施声明好，任何时候都能重建。"

# 🚢 DevOps Toolchain — Docker / K8s / Terraform / GitHub Actions 实战

从本地开发容器到生产 Kubernetes 集群，用一套标准化工具链实现「代码 → 镜像 → 基础设施 → 部署」的全自动化。

---

## 什么时候用什么

| 场景 | 首选工具 | 说明 |
|------|---------|------|
| 本地开发环境一致化 | Docker + Docker Compose | 避免"我本地能跑" |
| 单机/小规模部署 | Docker Compose / Docker Swarm | 简单，学习成本低 |
| 生产级容器编排 | Kubernetes | 自动扩缩容、自愈、服务发现 |
| 云资源声明管理 | Terraform | 基础设施即代码，多云一致 |
| CI/CD 自动化 | GitHub Actions | 与 GitHub 原生集成，社区生态丰富 |
| 配置管理/应用交付 | Helm / ArgoCD | 包管理 + GitOps 持续交付 |

---

## 核心技术栈

```
Docker              # 容器化
Docker Compose      # 本地多服务编排
Kubernetes          # 容器编排
Helm                # K8s 包管理
Terraform           # 基础设施即代码 (IaC)
GitHub Actions      # CI/CD
ArgoCD / Flux       # GitOps 持续交付
```

---

## 工作流程：Build → Ship → Run → Observe

### Step 1：容器化（Docker）

#### 多阶段构建 Dockerfile 模板

```dockerfile
# 构建阶段
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# 运行阶段（最小镜像）
FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package.json ./
EXPOSE 3000
CMD ["node", "dist/main.js"]
```

**优化 checklist**：
- [ ] 使用 Alpine 或 Distroless 基础镜像
- [ ] `.dockerignore` 排除 node_modules/.git
- [ ] 敏感信息绝不写入镜像，用运行时环境变量注入
- [ ] 非 root 用户运行：`USER node`

---

### Step 2：本地编排（Docker Compose）

```yaml
# docker-compose.yml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://postgres:password@db:5432/mydb
    depends_on:
      - db
      - redis
  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_PASSWORD: password
    volumes:
      - pgdata:/var/lib/postgresql/data
  redis:
    image: redis:7-alpine

volumes:
  pgdata:
```

---

### Step 3：Kubernetes 部署

#### 核心资源模板

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: app
          image: ghcr.io/myorg/my-app:v1.0.0
          ports:
            - containerPort: 3000
          envFrom:
            - secretRef:
                name: my-app-secrets
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "512Mi"
              cpu: "500m"
          livenessProbe:
            httpGet:
              path: /health
              port: 3000
          readinessProbe:
            httpGet:
              path: /ready
              port: 3000
---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 3000
---
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: app.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app
                port:
                  number: 80
```

#### 常用 kubectl 诊断

```bash
# 查看 Pod 状态
kubectl get pods -n mynamespace

# 查看 Pod 日志
kubectl logs -f deployment/my-app -n mynamespace

# 进入容器排查
kubectl exec -it pod/my-app-xxx -n mynamespace -- /bin/sh

# 查看事件
kubectl get events -n mynamespace --sort-by='.lastTimestamp'

# 资源使用
kubectl top pod -n mynamespace
```

---

### Step 4：基础设施即代码（Terraform）

```hcl
# main.tf
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "my-app/terraform.tfstate"
    region = "us-east-1"
  }
}

provider "aws" {
  region = var.aws_region
}

module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  version = "~> 20.0"

  cluster_name    = "${var.project_name}-cluster"
  cluster_version = "1.30"

  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnets

  eks_managed_node_groups = {
    general = {
      desired_size = 2
      min_size     = 1
      max_size     = 5
      instance_types = ["t3.medium"]
    }
  }
}
```

**Terraform 最佳实践**：
- 远程 state 存储（S3 + DynamoDB 锁）
- 模块化：按环境 `dev/`、`staging/`、`prod/` 拆分
- 变量化所有可配置项
- `terraform plan` 必看，`terraform apply` 谨慎

---

### Step 5：CI/CD（GitHub Actions）

```yaml
# .github/workflows/deploy.yml
name: Build and Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: "20"
          cache: "npm"
      - run: npm ci
      - run: npm run lint
      - run: npm run test
      - run: npm run build

  build-and-push:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      - name: Login to Container Registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - name: Build and push
        uses: docker/build-push-action@v5
        with:
          push: true
          tags: ghcr.io/${{ github.repository }}:${{ github.sha }}
          cache-from: type=gha
          cache-to: type=gha,mode=max

  deploy:
    needs: build-and-push
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to K8s
        run: |
          echo "${{ secrets.KUBECONFIG }}" | base64 -d > kubeconfig
          kubectl --kubeconfig=kubeconfig set image deployment/my-app app=ghcr.io/${{ github.repository }}:${{ github.sha }}
          kubectl --kubeconfig=kubeconfig rollout status deployment/my-app
```

---

### Step 6：GitOps 持续交付（ArgoCD）

```yaml
# argocd-app.yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/myorg/my-app-gitops.git
    targetRevision: main
    path: overlays/prod
  destination:
    server: https://kubernetes.default.svc
    namespace: prod
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

---

## 部署策略

| 策略 | 适用场景 | 风险 |
|------|---------|------|
| **滚动更新** | 默认策略，平滑 | 回滚时间较长 |
| **蓝绿部署** | 需要零停机，资源充足 | 资源翻倍 |
| **金丝雀** | 逐步放量，观察指标 | 需要流量控制 |
| **重建** | 开发/测试环境 | 有停机窗口 |

---

## 安全与成本守则

| 维度 | 建议 |
|------|------|
| **镜像安全** | 用 Trivy/Grype 扫描镜像漏洞，定期更新基础镜像 |
| **Secrets** | 用 K8s Secrets / Vault / AWS Secrets Manager，绝不提交 Git |
| **网络** | 最小权限 NetworkPolicy，生产不暴露 NodePort |
| **RBAC** | ServiceAccount 按需授权，不用 cluster-admin |
| **成本** | 非生产环境定时缩容，Spot 实例跑批处理 |
| **可观测性** | 必配日志、指标、链路追踪，否则不要上生产 |

---

## 快速入口

```
"帮我写个 Dockerfile"              → 多阶段构建模板 + 优化建议
"K8s 部署这个服务"                 → Deployment/Service/Ingress 模板
"写个 GitHub Actions"              → CI/CD workflow 模板
"Terraform 搭个 EKS"               → EKS + VPC 模块模板
"Helm Chart 怎么写"                → Chart 结构 + values.yaml 模板
"CI/CD 最佳实践"                   → Build → Test → Image → Deploy 全流程
```

---

## 与其他 Skill 的关系

| Skill | 关系 | 协作场景 |
|-------|------|---------|
| **cloudflare-worker** | 互补 | 边缘函数 vs 容器编排，按场景选择部署方式 |
| **quality-gate** | 前置 | CI 前跑质量门控（测试/安全/规范/逻辑/性能） |
| **solo-parallel-dev** | 工作模式 | 多分支并行开发时，每个分支独立部署到隔离环境 |
| **security-audit** | 安全补充 | 对 Dockerfile/K8s manifest/Terraform 做安全审计 |
| **postgres-pro** | 下游 | K8s 部署 PostgreSQL 时参考运行时诊断 |
| **api-doc-generator** | 前置 | API 文档生成后，再容器化并部署 |

**最佳实践链**：
```
openspec-sdd（接口设计）
  → api-doc-generator（文档）
  → quality-gate + security-audit（质量与安全检查）
  → devops-toolchain（容器化 → CI/CD → K8s 部署）
  → postgres-pro（数据库运维保障）
```

---

> "DevOps 不是工具堆砌，而是让变更从代码到用户的路径变得可预测、可回滚、可观测。"
