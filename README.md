# EKS Nginx GitOps

Deploy de uma aplicação Nginx em Kubernetes utilizando Kubernetes Manifests, Helm Charts, GitHub Actions e ArgoCD (GitOps).

## Objetivo

Este projeto foi criado para praticar conceitos de:

- Kubernetes
- Helm
- GitHub Actions
- ArgoCD
- GitOps
- Continuous Delivery
- Infrastructure Automation

---

## Arquitetura

```text
GitHub Repository
        |
        v
   GitHub Actions
        |
        v
      ArgoCD
        |
        v
   Kubernetes Cluster
        |
        v
       Nginx
```

---

## Estrutura do Projeto

```text
eks-nginx-gitops
├── .github/workflows
│   └── ci.yml
│
├── app
│   └── index.html
│
├── argocd
│   └── nginx-app.yaml
│
├── helm/nginx-app
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates
│
├── k8s
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
│
└── README.md
```

---

## Tecnologias Utilizadas

| Tecnologia | Finalidade |
|------------|------------|
| Kubernetes | Orquestração de containers |
| Helm | Gerenciamento de aplicações |
| ArgoCD | GitOps e Continuous Delivery |
| GitHub Actions | CI Pipeline |
| Nginx | Aplicação de demonstração |
| Docker | Container Runtime |

---

## Kubernetes Deployment

Aplicação implantada utilizando:

- Deployment
- Service
- ConfigMap
- Namespace

Validação:

```bash
kubectl get all -n nginx-app
```

---

## Helm

Validação do Chart:

```bash
helm lint helm/nginx-app
```

Renderização:

```bash
helm template nginx-app helm/nginx-app
```

Instalação:

```bash
helm install nginx-app helm/nginx-app -n nginx-app
```

Upgrade:

```bash
helm upgrade nginx-app helm/nginx-app -n nginx-app
```

---

## GitHub Actions

Pipeline responsável por:

- Helm Lint
- Manifest Validation
- Template Rendering

Workflow:

```text
Git Push
    |
    v
GitHub Actions
    |
    +--> Helm Lint
    +--> Render Templates
    +--> Validate Manifests
```

---

## ArgoCD GitOps

Application configurada:

```yaml
syncPolicy:
  automated:
    prune: true
    selfHeal: true
```

Recursos sincronizados automaticamente:

- Namespace
- ConfigMap
- Deployment
- Service

Validação:

```bash
kubectl get applications -n argocd
```

Resultado esperado:

```text
NAME       SYNC STATUS   HEALTH STATUS
nginx-app  Synced        Healthy
```

---

## GitOps Flow

```text
Developer
    |
    v
Git Push
    |
    v
GitHub
    |
    v
ArgoCD
    |
    v
Kubernetes
```

Qualquer alteração realizada no Git é sincronizada automaticamente pelo ArgoCD.

---

## Releases

### v1.0.0

- Kubernetes
- Helm
- GitHub Actions

### v2.0.0

- ArgoCD
- GitOps
- Self Heal
- Automated Sync
- ConfigMap managed through Git

---

## Próximos Passos

- Ingress Controller
- Deploy em Amazon EKS
- ExternalDNS
- Cert-Manager
- TLS com Let's Encrypt
- Observabilidade com Prometheus e Grafana

---

## Autor

**Paulo Júnior**

DevOps Engineer | Cloud Engineer

Tecnologias:

- AWS
- Terraform
- Kubernetes
- Docker
- GitHub Actions
- ArgoCD
- GitOps