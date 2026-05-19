# Glass Lewis DevOps Technical Challenge by Cedrick Eya

## Overview

This project deploys the Azure AKS Store Demo application into Azure Kubernetes Service (AKS) using Terraform, Kubernetes, Helm, and GitHub Actions CI/CD.

The solution uses the provided `aks-store-quickstart.yaml` manifest as the deployment starting point and enhances it with Infrastructure as Code, Kubernetes Ingress, Network Policies, Helm chart deployment, and automated CI/CD workflows.

---

# Repository Structure

```text
glasslewis-devops-challenge/
│
├── terraform/
│   ├── provider.tf
│   ├── variables.tf
│   ├── main.tf
│   └── outputs.tf
│
├── manifests/
│   ├── aks-store-quickstart.yaml
│   ├── ingress.yaml
│   └── network-policy.yaml
│
├── helm/
│   └── aks-store-demo/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│           └── store-front.yaml
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── architecture.md
│
└── README.md
```

---

# Technologies Used

- Azure Kubernetes Service (AKS)
- Terraform
- Kubernetes
- Helm
- GitHub Actions
- Azure CLI
- Docker
- NGINX Ingress Controller

---

# Challenge Requirements Covered

## 1. Kubernetes Manifest with Ingress Controller

Implemented Kubernetes Ingress resource to expose the Store Front application externally through the NGINX Ingress Controller.

Ingress manifest:

```text
manifests/ingress.yaml
```

---

## 2. Kubernetes Cluster Provisioned by Terraform

Terraform is used to provision:

- Azure Resource Group
- Azure Kubernetes Service (AKS) Cluster

Terraform files:

```text
terraform/
```

---

## 3. CI/CD Pipeline

GitHub Actions is used to automate:

### Continuous Integration (CI)

- Checkout source code
- Build Docker image
- Validate deployment pipeline
- Prepare Kubernetes deployment

### Continuous Deployment (CD)

- Authenticate to Azure
- Connect to AKS cluster
- Deploy Kubernetes manifests automatically

GitHub Actions workflow:

```text
.github/workflows/deploy.yml
```

---

## 4. Bonus Steps

### Helm Chart

Implemented a Helm chart to manage Kubernetes application deployment.

Helm chart location:

```text
helm/aks-store-demo
```

Deploy using Helm:

```bash
helm install aks-store-demo helm/aks-store-demo
```

---

### Resource Requests and Limits

Container resource requests and limits are configured in the Kubernetes manifests to improve workload stability and resource management.

---

### Network Policies

Implemented Kubernetes NetworkPolicy to improve inter-service communication security inside the AKS cluster.

Policy manifest:

```text
manifests/network-policy.yaml
```

Apply Network Policy:

```bash
kubectl apply -f manifests/network-policy.yaml
```

---

# Infrastructure Deployment

## Initialize Terraform

```bash
terraform init
```

## Validate Terraform

```bash
terraform validate
```

## Deploy Infrastructure

```bash
terraform apply -auto-approve
```

---

# Configure kubectl Access

```bash
az aks get-credentials \
  --resource-group rg-glasslewis-devops \
  --name aks-glasslewis
```

---

# Kubernetes Deployment

## Deploy Main Application

```bash
kubectl apply -f manifests/aks-store-quickstart.yaml
```

## Deploy Ingress Resource

```bash
kubectl apply -f manifests/ingress.yaml
```

## Deploy Network Policy

```bash
kubectl apply -f manifests/network-policy.yaml
```

---

# Verify Deployment

## Check Pods

```bash
kubectl get pods -n store-app
```

## Check Services

```bash
kubectl get svc -n store-app
```

## Check Ingress

```bash
kubectl get ingress -n store-app
```

## Check Network Policies

```bash
kubectl get networkpolicy -n store-app
```

---

# CI/CD Workflow

The GitHub Actions workflow automatically triggers whenever code is pushed to the `main` branch.

Pipeline stages include:

1. Checkout repository
2. Authenticate to Azure
3. Build container image
4. Validate deployment
5. Connect to AKS cluster
6. Deploy Kubernetes manifests
7. Deploy Ingress resource
8. Deploy Network Policies

---

# Kubernetes Improvements

The deployment includes:

- Namespace isolation
- Resource requests and limits
- Liveness probes
- Readiness probes
- Startup probes
- Kubernetes Ingress
- Network Policies
- Infrastructure as Code using Terraform
- Helm chart deployment

---

# Architecture

```text
GitHub Actions
      ↓
Terraform
      ↓
Azure Kubernetes Service (AKS)
      ↓
Deploy Kubernetes Manifests
      ↓
Ingress Controller
      ↓
Store Front Application
      ↓
Product Service + Order Service + RabbitMQ
```

---

# Potential Future Improvements

The following enhancements can be implemented in future iterations:

- Azure Container Registry integration
- Horizontal Pod Autoscaler (HPA)
- Azure Monitor integration
- Azure Key Vault integration
- HTTPS/TLS termination
- Multi-environment deployment strategy
- GitOps deployment using ArgoCD

---

# Notes

The project uses the official Azure AKS Store Demo manifest as the deployment starting point, as required in the assessment instructions.

The focus of this implementation is demonstrating:

- Kubernetes deployment knowledge
- Infrastructure as Code (Terraform)
- CI/CD automation
- AKS deployment practices
- Kubernetes networking using Ingress
- Helm package management
- Kubernetes security using Network Policies
```