# 📖 Docker — Definitions & Examples

> Roadmap: [`../Roadmap/06-Docker.md`](../Roadmap/06-Docker.md)

### 📚 Reference docs
- [Docker documentation](https://docs.docker.com/) · [Get Started guide](https://docs.docker.com/get-started/)
- [Dockerfile reference](https://docs.docker.com/reference/dockerfile/) · [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker CLI reference](https://docs.docker.com/reference/cli/docker/) · [Compose](https://docs.docker.com/compose/)
- [Amazon ECR docs](https://docs.aws.amazon.com/ecr/) · [Docker Hub](https://hub.docker.com/)
- [Multi-stage builds](https://docs.docker.com/build/building/multi-stage/) · [Trivy (image scan)](https://trivy.dev/) · [distroless images](https://github.com/GoogleContainerTools/distroless)

---

## Core concepts
**Container vs VM** 🔥🔥 — a container shares the **host kernel** and isolates at process level (lightweight, seconds to start). A VM runs a **full guest OS** on a hypervisor (heavy, GBs).

**Image** 🔥 — immutable, layered template. **Container** — a running instance of an image (image : container ≈ class : object).

**Layer** — each Dockerfile instruction creates a cached layer; changing one busts all layers below it (why you copy `package.json` + install **before** copying source).

**Registry** — stores images: Docker Hub, **Amazon ECR** (private).

**Dockerfile** — build recipe.
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
CMD ["node","server.js"]
```

**CMD vs ENTRYPOINT** 🔥 — `ENTRYPOINT` = fixed executable; `CMD` = default args (easily overridden at `docker run`). Common: `ENTRYPOINT ["python"]` + `CMD ["app.py"]`.

**COPY vs ADD** 🔥 — `COPY` just copies; `ADD` also extracts tar + fetches URLs. **Prefer COPY**.

**EXPOSE** — documents a port (doesn't publish). `-p 8080:80` actually maps host→container.

**Multi-stage build** 🔥🔥 — compile in a build stage, copy only the artifact into a slim runtime image → smaller, no build tools, fewer vulns.

**Volume vs bind mount** — volume = Docker-managed persistent storage; bind mount = host path. Containers are ephemeral — use volumes to persist data.

---

## ECR flow 🔥
```bash
aws ecr get-login-password --region us-east-1 \
  | docker login --username AWS --password-stdin <acct>.dkr.ecr.us-east-1.amazonaws.com
docker build -t app:$GIT_SHA .
docker tag app:$GIT_SHA <acct>.dkr.ecr.us-east-1.amazonaws.com/app:$GIT_SHA
docker push <acct>.dkr.ecr.us-east-1.amazonaws.com/app:$GIT_SHA
```

## Image optimization 🔥
- Multi-stage + alpine/distroless base.
- `.dockerignore` (skip node_modules, .git).
- Order layers least→most changing.
- Combine `RUN` steps, pin versions.

## Security
- Run as **non-root** `USER`. Scan images (Trivy / ECR scan). No secrets in layers (they persist in history). Minimal base image.

---

## 🎯 Likely interview Qs
- Container vs VM. Image vs container. What is a layer?
- CMD vs ENTRYPOINT. COPY vs ADD.
- What is a multi-stage build and why use it?
- How do you reduce image size?
- How do you persist data? (volumes)
- Debug a container that exits immediately. (`docker logs`, check ENTRYPOINT/CMD)
- Push an image to ECR.
