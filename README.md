# EKS Nginx GitOps

Deploy de uma aplicação Nginx em Kubernetes utilizando manifests Kubernetes e Helm Charts.

## Objetivo

Este projeto foi criado para praticar conceitos de:

- Kubernetes
- Helm
- GitOps Ready Structure
- ConfigMaps
- Deployments
- Services
- GitHub Actions (em evolução)

## Arquitetura

```text
┌─────────────┐
│   GitHub    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ Helm Chart  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ Kubernetes  │
│ Deployment  │
│ Service     │
│ ConfigMap   │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    Nginx    │
└─────────────┘
```

## Estrutura do Projeto

```text
eks-nginx-gitops/
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── helm/
│   └── nginx-app/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│
├── k8s/
│   ├── namespace.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
│
└── README.md
```

## Tecnologias Utilizadas

- Kubernetes
- Helm
- Docker
- Kind
- GitHub Actions
- Nginx

## Criando o Cluster Local

Instalar Kind:

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-amd64
chmod +x kind
sudo mv kind /usr/local/bin/
```

Criar cluster:

```bash
kind create cluster --name devops-lab
```

Verificar:

```bash
kubectl get nodes
```

## Deploy com Kubernetes

Criar namespace:

```bash
kubectl apply -f k8s/namespace.yaml
```

Aplicar deployment:

```bash
kubectl apply -f k8s/deployment.yaml
```

Aplicar service:

```bash
kubectl apply -f k8s/service.yaml
```

Verificar:

```bash
kubectl get all -n nginx-app
```

## Deploy com Helm

Validar chart:

```bash
helm lint helm/nginx-app
```

Renderizar templates:

```bash
helm template nginx-app helm/nginx-app
```

Instalar chart:

```bash
helm install nginx-app helm/nginx-app \
  -n nginx-app
```

Verificar release:

```bash
helm list -n nginx-app
```

## Upgrade da Aplicação

Editar:

```yaml
replicaCount: 3
```

Executar:

```bash
helm upgrade nginx-app helm/nginx-app \
  -n nginx-app
```

Verificar:

```bash
kubectl get pods -n nginx-app
```

## Acessando a Aplicação

Port Forward:

```bash
kubectl port-forward \
  -n nginx-app \
  svc/nginx 8080:80
```

Acessar:

```bash
curl http://localhost:8080
```

## Funcionalidades Implementadas

- Namespace Kubernetes
- Deployment Nginx
- Service ClusterIP
- ConfigMap para conteúdo customizado
- Helm Chart
- Helm Upgrade
- Escalabilidade via réplicas

## Roadmap

### v0.4.0

- [x] Namespace
- [x] Deployment
- [x] Service
- [x] ConfigMap
- [x] Helm Chart
- [x] Helm Upgrade

### v1.0.0

- [ ] GitHub Actions
- [ ] Helm Lint
- [ ] Helm Template Validation

### v1.1.0

- [ ] NGINX Ingress Controller

### v1.2.0

- [ ] ArgoCD GitOps

### v1.3.0

- [ ] Deploy em Amazon EKS

## Autor

Paulo Júnior

DevOps Engineer em formação

LinkedIn:
https://www.linkedin.com/in/paulojúnior

GitHub:
https://github.com/pauloojr