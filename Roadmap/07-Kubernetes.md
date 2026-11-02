# 7. KUBERNETES — Roadmap

> Resume lists Kubernetes. On AWS that's **EKS**. Know the objects, self-healing, scaling, and how a request reaches a pod.

```
KUBERNETES
│
├── 1. ARCHITECTURE
│   ├── Control plane — API server, etcd, scheduler, controller-manager
│   ├── Nodes — kubelet, kube-proxy, container runtime
│   └── kubectl → API server
│
├── 2. WORKLOADS
│   ├── Pod — smallest unit (1+ containers)
│   ├── ReplicaSet — keep N replicas
│   ├── Deployment ⭐ — rolling update + rollback
│   ├── StatefulSet — stable identity/storage (DBs)
│   ├── DaemonSet — one pod per node (agents)
│   └── Job / CronJob — batch / scheduled
│
├── 3. NETWORKING
│   ├── Service — ClusterIP / NodePort / LoadBalancer ⭐
│   ├── Ingress — HTTP routing + TLS
│   ├── kube-proxy, cluster DNS (CoreDNS)
│   └── Request path: Ingress → Service → Endpoints → Pod
│
├── 4. CONFIG & SECRETS
│   ├── ConfigMap (plain config)
│   ├── Secret (base64, sensitive)
│   ├── env / volume mounts
│   └── External Secrets (AWS Secrets Manager)
│
├── 5. HEALTH & SCALING
│   ├── Liveness probe (restart if dead)
│   ├── Readiness probe (remove from LB if not ready)
│   ├── Startup probe
│   ├── HPA ⭐ — scale pods on CPU/metrics
│   └── requests / limits (resources)
│
├── 6. STORAGE
│   ├── Volume, PersistentVolume (PV), PVC
│   ├── StorageClass (EBS CSI on EKS)
│   └── emptyDir / configMap volumes
│
├── 7. SECURITY & ORG
│   ├── Namespaces
│   ├── RBAC (Role, RoleBinding)
│   ├── ServiceAccount + IRSA (IAM Roles for Service Accounts) ⭐
│   └── NetworkPolicy
│
├── 8. PACKAGING & DEPLOY
│   ├── Helm (charts, values, releases)
│   ├── Kustomize (overlays per env)
│   └── Rolling / Blue-Green / Canary
│
└── 9. EKS (AWS) ⭐
    ├── managed control plane
    ├── node groups / Fargate profiles
    ├── AWS Load Balancer Controller (ALB)
    ├── IRSA for pod IAM
    └── ECR for images
```

## 🔑 kubectl reflexes
| Task | Command |
|------|---------|
| List pods | `kubectl get pods -n <ns>` |
| Describe/diagnose | `kubectl describe pod <p>` |
| Logs | `kubectl logs <p> -f` |
| Exec into pod | `kubectl exec -it <p> -- sh` |
| Scale | `kubectl scale deploy app --replicas=5` |
| Rollout status | `kubectl rollout status deploy/app` |
| Rollback | `kubectl rollout undo deploy/app` |
| Apply manifest | `kubectl apply -f deploy.yaml` |

## 🔑 Decision reflexes
| Question | Answer |
|----------|--------|
| Deployment vs StatefulSet | stateless/interchangeable vs stable id + storage (DBs) |
| ConfigMap vs Secret | plain config vs sensitive (base64, can encrypt at rest) |
| Liveness vs Readiness | restart-if-dead vs route-traffic-only-if-ready |
| Service types | ClusterIP (internal) / NodePort / LoadBalancer (external) |
| Self-healing | controller reconciles desired state; restarts/reschedules pods |
| CrashLoopBackOff | app keeps crashing → check `logs` + `describe` |

## 🎯 Interview focus
- How does a rolling update work + how to roll back.
- How does HPA scale; how self-healing works.
- Debug CrashLoopBackOff / ImagePullBackOff / Pending pod.
- How a request reaches a pod (Ingress→Service→Pod).
- IRSA: give pods IAM access without keys.

→ Definitions: [`../Definitions/07-Kubernetes-definitions.md`](../Definitions/07-Kubernetes-definitions.md)
