
## 🚀 DevSecOps Demo Lab

This is a **Kubernetes-based DevSecOps demo environment** built for showcasing modern GitOps, security, and infrastructure best practices.

> 🔒 Designed for **SOC2-style compliance**, **secure-by-default Kubernetes**, and **GitOps automation** with real-world tools.

---

### 🧰 Tech Stack

- **FluxCD** – GitOps continuous delivery
- **Kyverno** – Kubernetes policy enforcement
- **cert-manager** – TLS management with self-signed & CA issuers
- **External Secrets Operator** – Secure secrets management (Azure)
- **Prometheus + Grafana** – Observability stack
- **NGINX Ingress Controller** – Routing with optional TLS
- **SOPS** – Secret encryption at rest
- **Go + PostgreSQL app** – Sample microservice + database deployment

---

### ✅ What This Demo Proves

- 🔁 GitOps-first infra using Flux
- 🛡️ Pod security policies with Kyverno
- 🔐 TLS and secret handling with cert-manager + ESO
- 📈 Monitoring via Prometheus + Grafana
- 🧪 CI validation of manifests using `kubeconform`
- 🧱 Docker security best practices (non-root, pinned versions)
- 🛠️ Custom Go app + DB deployment for hands-on realism

---

### 📦 Local Development

You can run everything locally using [kind](https://kind.sigs.k8s.io/) and [Flux bootstrap](https://fluxcd.io/flux/installation/). Setup instructions are in the `kind_deployment/README.md`.
