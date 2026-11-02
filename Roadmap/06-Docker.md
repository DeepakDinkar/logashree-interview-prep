# 6. DOCKER — Roadmap

> Resume: *"Containerized workloads with Docker, removed env-specific issues, improved consistency."* Images go to **Amazon ECR**, run on **ECS/EKS**.

```
DOCKER
│
├── 1. CONCEPTS
│   ├── Image (immutable template) vs Container (running instance)
│   ├── Layers + union filesystem
│   ├── Registry (Docker Hub, Amazon ECR)
│   └── Docker Engine / daemon
│
├── 2. CORE COMMANDS
│   ├── docker build -t app:1.0 .
│   ├── docker run -d -p 8080:80 app
│   ├── docker ps / images / logs / exec
│   ├── docker stop / rm / rmi
│   └── docker pull / push / tag
│
├── 3. DOCKERFILE
│   ├── FROM, WORKDIR, COPY, ADD
│   ├── RUN, ENV, ARG
│   ├── EXPOSE, CMD vs ENTRYPOINT
│   ├── USER (non-root)
│   └── HEALTHCHECK
│
├── 4. MULTI-STAGE BUILD ⭐
│   ├── build stage (compile)
│   ├── copy artifact to slim runtime
│   ├── smaller image, no build tools
│   └── distroless / alpine base
│
├── 5. IMAGE OPTIMIZATION
│   ├── layer caching (order matters)
│   ├── .dockerignore
│   ├── minimal base images
│   └── combine RUN steps
│
├── 6. DATA & NETWORK
│   ├── Volumes (persistent) vs bind mounts
│   ├── Networks (bridge, host, none)
│   └── container-to-container DNS
│
├── 7. COMPOSE
│   ├── docker-compose.yml (multi-service local)
│   ├── depends_on, env, ports, volumes
│   └── up / down / logs
│
├── 8. ECR (AWS) ⭐
│   ├── aws ecr get-login-password | docker login
│   ├── tag + push to <acct>.dkr.ecr.<region>.amazonaws.com
│   ├── image scanning
│   └── lifecycle policies (clean old images)
│
└── 9. SECURITY
    ├── non-root USER
    ├── scan images (Trivy, ECR scan)
    ├── pin versions, no secrets in layers
    └── minimal attack surface
```

## 🏗️ Multi-stage Dockerfile (say this in interview)
```dockerfile
# build stage
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# runtime stage (small)
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
```

## 🔑 Decision reflexes
| Question | Answer |
|----------|--------|
| Image vs container | Template (class) vs running instance (object) |
| CMD vs ENTRYPOINT | CMD = default args (overridable); ENTRYPOINT = fixed executable |
| COPY vs ADD | COPY plain; ADD also untars + URLs (prefer COPY) |
| Why multi-stage | Drop build tools → smaller, safer image |
| Container vs VM | Container shares host kernel (light); VM = full OS (heavy) |
| Persist data | Volumes |

## 🎯 Interview focus
- Reduce image size (multi-stage, alpine/distroless, .dockerignore, layer order).
- What is a layer? Why cache busts on code change.
- Debug a container that exits immediately (`docker logs`, ENTRYPOINT).
- Push to ECR flow.

→ Definitions: [`../Definitions/06-Docker-definitions.md`](../Definitions/06-Docker-definitions.md)
