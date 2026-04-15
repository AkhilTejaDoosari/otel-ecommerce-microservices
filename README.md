# <img src="https://opentelemetry.io/img/logos/opentelemetry-logo-nav.png" alt="OTel logo" width="45"> otel-ecommerce-microservices

> **Note:** This project is a fork of [`opentelemetry-demo`](https://github.com/open-telemetry/opentelemetry-demo). Thanks to the team and 141+ contributors for open-sourcing this wonderful demo project — definitely one of the best on the internet.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg?color=red)](https://github.com/open-telemetry/opentelemetry-demo/blob/main/LICENSE)

End-to-end DevOps implementation of a cloud-native e-commerce platform. The application is the **OpenTelemetry Astronomy Shop** — a production-grade microservices distributed system. My work covers the full infrastructure, deployment, and operations layer on top of it.

---

## 📚 Course

This project is built as part of the Udemy course:

**[Ultimate DevOps Project Implementation](https://www.udemy.com/course/ultimate-devops-project-with-resume-preparation/)** by [Abhishek Veeramalla](https://github.com/iam-veeramalla)

> 70 videos across 5 phases — covering containerization, IaC, Kubernetes, GitOps and CI/CD.

| Phase | Videos | Focus |
|---|---|---|
| 1. Foundation & Local Setup | 01 - 18 | AWS account, IAM, EC2, Docker, kubectl, Terraform |
| 2. Containerization | 19 – 31 | Dockerfiles, Docker Compose, ECR, K8s onboarding intro |
| 3. Infrastructure as Code | 32 – 43 | Terraform state, S3 backend, DynamoDB locking, VPC & EKS modules |
| 4. Kubernetes & Networking | 44 – 63 | K8s manifests, Service types, Ingress, ALB, Route 53, custom domain |
| 5. GitOps & CI/CD | 64 – 70 | GitHub Actions, ArgoCD, GitOps workflow |

---

## My DevOps Implementation

> The application code belongs to the OpenTelemetry community. Everything below is my work.

### Phase 01 — Foundation & Local Setup
- Created AWS account and configured IAM user with required permissions
- Provisioned EC2 instance (t2.large minimum — Assignment 1) for all workloads
- Installed Docker, kubectl, and Terraform on the EC2 instance
- Ran the project locally on EC2 to verify baseline functionality
- Configured AWS Security Groups to control inbound/outbound access
- Studied Docker lifecycle to understand container runtime behaviour

### Phase 02 — Containerization
- Wrote and validated Dockerfiles per service (Go, Java, Python, and others)
- Used `docker init` where applicable to accelerate Dockerfile authoring
- Built and pushed all container images to Amazon ECR
- Ran all services locally with Docker Compose and verified inter-service networking and health checks
- Compared Docker vs Kubernetes and Docker Compose vs Kubernetes to understand when and why to graduate to orchestration
- Completed steps to onboard the project onto Kubernetes

### Phase 03 — Infrastructure as Code (Terraform)
- Studied the Terraform lifecycle and statefile as the source of truth for infrastructure
- Configured AWS provider and remote state backend using S3
- Enabled Terraform state locking via DynamoDB to prevent concurrent conflicts
- Provisioned the S3 bucket and DynamoDB table themselves using Terraform
- Adopted a modular Terraform approach: VPC module → EKS module → main execution
- Verified all provisioned resources post-apply

### Phase 04 — Kubernetes & Networking
- Configured kubeconfig to connect to single and multiple EKS clusters from the command line
- Created and configured Kubernetes Service Accounts and understood their real-world importance
- Authored Kubernetes manifests: Deployments (scaling & healing), Services (service discovery), ConfigMaps, Secrets
- Reviewed manifests for all microservices in the project (Assignment 2)
- Deployed the full application to EKS across three staged rollouts
- Compared Kubernetes Service Types and accessed the project via LoadBalancer service type
- Identified disadvantages of the LoadBalancer service type as justification for moving to Ingress
- Studied Ingress and Ingress Controllers (concepts and architecture)
- Deployed the ALB Ingress Controller on EKS
- Configured Ingress resources and accessed the project through the ALB
- Registered a custom domain and created a Route 53 hosted zone
- Updated nameservers and set the Ingress hostname to the custom domain
- Verified end-to-end browser access via custom domain

### Phase 05 — GitOps & CI/CD
- Studied CI/CD concepts and GitOps principles
- Understood GitHub Actions structure (triggers, jobs, steps, runners)
- Built a CI pipeline for a microservice: lint → test → Docker build → push to ECR
- Executed and validated the CI pipeline end-to-end
- Installed and configured ArgoCD on EKS
- Connected this repo as the ArgoCD GitOps source of truth
- Deployed the full project via ArgoCD and implemented automated sync/reconciliation
- Verified cluster-wide "Healthy" status in the ArgoCD UI

---

## Tech Stack

| Layer | Tool |
|---|---|
| Application | OpenTelemetry Astronomy Shop (microservices) |
| Containerization | Docker, Docker Compose |
| Container Registry | Amazon ECR |
| Orchestration | Kubernetes (Amazon EKS) |
| IaC | Terraform |
| GitOps | ArgoCD |
| CI/CD | GitHub Actions |
| DNS | AWS Route 53 |
| Ingress | AWS ALB Ingress Controller |

---

## Infrastructure

All workloads run on AWS. No local cluster — everything deploys directly to cloud infrastructure.

| Service | Usage |
|---|---|
| Amazon EC2 | Initial setup and local project verification |
| Amazon EKS | Kubernetes cluster |
| Amazon ECR | Container image registry |
| Amazon S3 | Terraform remote state |
| Amazon DynamoDB | Terraform state locking |
| AWS Route 53 | DNS and domain routing |

---

## Lab Environment

| Machine | Role |
|---|---|
| Mac (M-series) | VS Code, YAML authoring, git push only |
| AWS (EC2 + EKS) | All infrastructure, Docker, Kubernetes, Terraform — primary environment |

> All heavy workloads run directly on AWS. No local Docker engine or Minikube required.

---

## Quick Start (Application)

- [Docker Compose](https://opentelemetry.io/docs/demo/docker_deployment/)
- [Kubernetes](https://opentelemetry.io/docs/demo/kubernetes_deployment/)

---

## About the Application

The OpenTelemetry Astronomy Shop is a microservice-based distributed system intended to illustrate OpenTelemetry instrumentation in a near real-world environment. Our goals are threefold:

- Provide a realistic example of a distributed system demonstrating OpenTelemetry instrumentation and observability
- Build a base for vendors, tooling authors, and others to extend and demonstrate their OpenTelemetry integrations
- Create a living example for OpenTelemetry contributors to use for testing new versions of the API, SDK, and components

For detailed documentation, see [opentelemetry.io/docs/demo](https://opentelemetry.io/docs/demo/).

---

## Acknowledgements

- **Application**: [open-telemetry/opentelemetry-demo](https://github.com/open-telemetry/opentelemetry-demo) 
- **Guidance & Course**: [Abhishek Veeramalla](https://github.com/iam-veeramalla) — [Ultimate DevOps Project Implementation](https://www.udemy.com/course/ultimate-devops-project-with-resume-preparation/) on Udemy
- **Original fork**: [iam-veeramalla/ultimate-devops-project-demo](https://github.com/iam-veeramalla/ultimate-devops-project-demo)
