# KubeAssist AI

Kubernetes troubleshooting assistant (student MVP). Collects live cluster evidence, retrieves Kubernetes docs with RAG, and returns structured diagnoses with fix steps — without auto-applying changes.

**Full project status, architecture, progress, and phase roadmap:**  
→ [docs/PROJECT_STATUS.md](docs/PROJECT_STATUS.md)

---

## Current progress

- **Done:** Phase 1 lab manifests in [`k8s/lab/`](k8s/lab/) (8 intentional failure scenarios)
- **Partial:** Verify every scenario on Kind
- **Next:** Phase 2 — Go + client-go collector
- **Overall:** ~10–15% of MVP

---

## How to run the lab

**Prerequisites:** Docker Desktop, Kind, kubectl.

```powershell
kind create cluster --name kubeassist-dev
kubectl create namespace kubeassist-lab
kubectl apply -f .\k8s\lab\
kubectl get pods -n kubeassist-lab
```

Inspect a failing pod (use the real name from `get pods`, or a label):

```powershell
kubectl describe pod -l app=crashloop-app -n kubeassist-lab
kubectl logs -l app=crashloop-app -n kubeassist-lab --tail=50
```

Reset:

```powershell
kubectl delete namespace kubeassist-lab
kubectl create namespace kubeassist-lab
kubectl apply -f .\k8s\lab\
```

---

## What to build next

1. Finish Phase 1 verification (golden notes for each failure).
2. Start Phase 2: Go module + client-go `ListPods` (waiting reason, restart count).
3. Do not start React or the LLM until Go can return a full diagnostic snapshot.

See [docs/PROJECT_STATUS.md](docs/PROJECT_STATUS.md) for the complete roadmap.
