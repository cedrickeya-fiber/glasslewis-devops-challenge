# Glass Lewis DevOps Technical Challenge by Cedrick Eya

## Overview

This project deploys the Azure AKS Store Demo application into Azure Kubernetes Service (AKS).

The deployment uses:

- Terraform
- Kubernetes
- GitHub Actions CI/CD
- Azure Kubernetes Service (AKS)

---

## Repository Structure

```text
terraform/
manifests/
.github/workflows/
```

---

## Infrastructure Deployment

```bash
terraform init
terraform apply -auto-approve
```

---

## Kubernetes Deployment

```bash
kubectl apply -f manifests/aks-store-quickstart.yaml
```

---

## CI/CD

GitHub Actions automatically deploys the application into AKS whenever code is pushed to the main branch.

---

## Improvements

Potential future enhancements:

- Helm charts
- Ingress Controller
- Azure Monitor
- Horizontal Pod Autoscaler
- Azure Key Vault Integration