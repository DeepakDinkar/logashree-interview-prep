# 📖 Kubernetes — Definitions & Examples

> Roadmap: [`../Roadmap/07-Kubernetes.md`](../Roadmap/07-Kubernetes.md) · On AWS = **EKS**.

### 📚 Reference docs
- [Kubernetes documentation](https://kubernetes.io/docs/home/) · [Concepts](https://kubernetes.io/docs/concepts/)
- [kubectl cheat sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) · [kubectl reference](https://kubernetes.io/docs/reference/kubectl/)
- [Amazon EKS docs](https://docs.aws.amazon.com/eks/) · [EKS Best Practices Guide](https://aws.github.io/aws-eks-best-practices/) · [IRSA](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)
- [Helm docs](https://helm.sh/docs/) · [Kustomize](https://kustomize.io/)
- [Probes guide](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/) · [HPA](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

---

## Architecture
**Control plane** — API server (front door), **etcd** (cluster state store), scheduler (places pods), controller-manager (reconciles state).
**Node** — worker: **kubelet** (runs pods), **kube-proxy** (networking), container runtime.
**Desired state / reconciliation** 🔥 — you declare desired state; controllers continuously make reality match → self-healing.

## Workloads
**Pod** 🔥 — smallest deployable unit; 1+ containers sharing network/storage. Ephemeral.
**ReplicaSet** — keeps N pod replicas.
**Deployment** 🔥🔥 — manages ReplicaSets → rolling updates + rollback (`kubectl rollout undo`).
**StatefulSet** 🔥 — stable network id + persistent storage per pod (databases).
**DaemonSet** — one pod per node (log/monitoring agents).
**Job / CronJob** — run-to-completion / scheduled.

## Networking
**Service** 🔥 — stable endpoint + load balancing for pods:
- **ClusterIP** (internal), **NodePort** (node port), **LoadBalancer** (cloud LB / ALB on EKS).
**Ingress** — HTTP(S) routing + TLS into services (path/host rules).
**Request path** 🔥 — Ingress → Service → Endpoints → Pod. DNS via CoreDNS.

## Config & health
**ConfigMap vs Secret** 🔥 — plain config vs sensitive data (base64, encryptable at rest).
**Liveness vs Readiness probe** 🔥🔥
- **Liveness** — if it fails, kubelet **restarts** the container.
- **Readiness** — if it fails, pod is **removed from the Service** (no traffic) but not restarted.
- **Startup** — gives slow apps time before liveness kicks in.
**requests / limits** — guaranteed vs max CPU/memory.
**HPA** 🔥 — Horizontal Pod Autoscaler scales replica count on CPU/custom metrics.

## Storage
**Volume / PV / PVC** — storage abstraction; PVC requests a PersistentVolume via a **StorageClass** (EBS CSI on EKS).

## Security & org
**Namespace** — virtual cluster partition.
**RBAC** — Role + RoleBinding grant least-privilege in-cluster.
**IRSA** 🔥 (EKS) — IAM Roles for Service Accounts; gives pods AWS permissions without keys.
**NetworkPolicy** — firewall between pods.

## Packaging
**Helm** — K8s package manager (charts + values). **Kustomize** — overlay config per env.

## Common failures 🔥
| Status | Meaning | Fix |
|--------|---------|-----|
| CrashLoopBackOff | app keeps crashing | `kubectl logs`, `describe` |
| ImagePullBackOff | can't pull image | check tag/registry/ECR auth |
| Pending | can't schedule | no resources / node selector / PVC |
| OOMKilled | exceeded memory limit | raise limit / fix leak |

---

## 🎯 Likely interview Qs
- Pod vs Deployment vs StatefulSet.
- Service types; how a request reaches a pod.
- Liveness vs readiness probe.
- ConfigMap vs Secret.
- How rolling update + rollback work; how HPA/self-healing work.
- Debug CrashLoopBackOff / ImagePullBackOff / Pending.
- EKS: how do pods get AWS access? (IRSA)
