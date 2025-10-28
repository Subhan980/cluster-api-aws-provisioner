# 🚀 cluster-api-aws-provisioner

A fully automated **Kubernetes Cluster API (CAPI)** implementation for **AWS**, enabling declarative cluster provisioning, scaling, and lifecycle management.

This project demonstrates **enterprise-grade Kubernetes infrastructure automation** using the **Cluster API Provider for AWS (CAPA)**.  
It allows you to define, deploy, and manage complete EKS or self-managed clusters using native Kubernetes-style YAML manifests.

---

## 🌐 Overview

**Cluster API (CAPI)** brings Kubernetes-style declarative APIs to cluster management —  
allowing you to manage clusters just like any other Kubernetes resource.

This implementation automates:

- VPC and networking creation  
- Control plane and worker node provisioning  
- Cluster scaling and upgrade workflows  
- Multi-cluster management from a single management cluster  

---

## 🧩 Tech Stack

| Tool | Purpose |
|------|----------|
| **Kubernetes** | Management plane for clusters |
| **Cluster API (CAPI)** | Declarative cluster lifecycle management |
| **Cluster API Provider AWS (CAPA)** | Infrastructure provider for AWS |
| **Helm / Kustomize** | Configuration and templating |
| **GitHub Actions** | (Optional) CI/CD automation for cluster provisioning |

---

## 🎯 Key Features

✅ Declarative cluster provisioning on AWS  
✅ Fully managed control plane and worker nodes  
✅ Support for EKS and self-managed Kubernetes clusters  
✅ Secure VPC, subnet, and IAM role setup  
✅ Rolling updates and scaling policies  
✅ Works with your observability stack (Prometheus + Grafana + Loki)  
✅ Ready for production-grade deployments  

---
     +-------------------------------------------+
     |          Management Cluster               |
     |-------------------------------------------|
     | Cluster API + CAPA Controllers             |
     | Custom Resources (Cluster, Machine, etc.)  |
     +-------------------------------------------+
                      │
                      ▼
     +-------------------------------------------+
     |        AWS Infrastructure Provider         |
     | (VPCs, Subnets, EC2, IAM, EKS)             |
     +-------------------------------------------+
                      │
                      ▼
     +-------------------------------------------+
     |         Target Kubernetes Cluster          |
     |  (Control Plane + Worker Nodes)            |
     +-------------------------------------------+
                      │
                      ▼
     +-------------------------------------------+
     |         Observability & Automation         |
     | (Prometheus, Grafana, Loki, Alerts)        |
     +-------------------------------------------+

---

## 🚀 Quick Start

### 1️⃣ Prerequisites

- AWS Account with programmatic access (CLI credentials)  
- A running management Kubernetes cluster  
- `kubectl`, `clusterctl`, and `aws` CLI installed  
- IAM permissions for EC2, VPC, and IAM resource creation  

---

### 2️⃣ Initialize the Management Cluster

```bash
clusterctl init --infrastructure aws
This installs:

Cluster API core components

Cluster API AWS provider (CAPA)
---
## **3️⃣ Generate Cluster Manifests**

```bash
clusterctl generate cluster aws-demo \
  --infrastructure aws \
  --kubernetes-version v1.29.0 \
  --control-plane-machine-count=1 \
  --worker-machine-count=2 > aws-cluster.yaml


4️⃣ Apply and Create the Cluster
bash
Copy code
kubectl apply -f aws-cluster.yaml
CAPI and CAPA will automatically:

Create VPC, subnets, and security groups

Deploy the control plane and worker nodes

Register the new cluster for management

5️⃣ Verify the Cluster
bash
Copy code
kubectl get clusters
kubectl get machines
Once provisioning completes, fetch the kubeconfig:

bash
Copy code
clusterctl get kubeconfig aws-demo > demo.kubeconfig
kubectl --kubeconfig=demo.kubeconfig get nodes
📦 Repository Structure
bash
Copy code
📁 cluster-api-aws-provisioner/
 ├── config/                  # Cluster API configuration templates
 ├── manifests/               # Generated YAML for clusters and machines
 ├── scripts/                 # Helper scripts for bootstrap and cleanup
 ├── docs/                    # Documentation and architecture notes
 ├── .github/workflows/       # Optional CI/CD automation
 └── README.md
🧩 Future Enhancements
🔹 Automate teardown and cleanup workflows

🔹 Integrate AWS SSM for secure node access

🔹 Add Terraform-based infra bootstrapping

🔹 Support multi-region cluster provisioning

🔹 Integrate cost dashboards and usage insights

🤝 Contributing
Contributions are welcome!
You can:

Extend cluster templates

Add new automation scripts

Improve CI/CD workflows

Enhance documentation

💡 Maintainer
cluster-api-aws-provisioner
Developed and maintained by Your Name.

For suggestions or issues, please open a GitHub issue.
