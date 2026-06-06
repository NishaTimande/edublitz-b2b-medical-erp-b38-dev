# EduBlitz Medical B2B ERP System
#this readme file and project is dedicated for b38 batch
#this is a immediate hotfix change that should be implement on prod immediately.
A production-grade **Medical Domain B2B ERP** platform for hospitals, distributors, and medical vendors. Built with a microservices architecture on AWS infrastructure.
it is cedc44...
## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        CloudFront CDN                           │
│                    (React Frontend via S3)                      │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│              AWS ALB Ingress Controller (EKS)                   │
└──────┬─────────────────────┬──────────────────────┬─────────────┘
       │                     │                      │
┌──────▼──────┐    ┌─────────▼────────┐   ┌────────▼────────┐
│ user-service│    │ product-service  │   │  order-service  │
│  Port: 8081 │    │   Port: 8082     │   │   Port: 8083    │
│             │    │                  │   │                 │
│ Auth / JWT  │    │ Inventory/Catalog │   │ Orders/Billing  │
│ Roles/Orgs  │    │ Stock Tracking   │   │ Order Lifecycle │
└──────┬──────┘    └─────────┬────────┘   └────────┬────────┘
       │                     │                      │
┌──────▼─────────────────────▼──────────────────────▼─────────────┐
│                     MongoDB Atlas                                │
│   users_db          products_db            orders_db            │
└─────────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Layer        | Technology                            |
|--------------|---------------------------------------|
| Frontend     | React 18 + Vite + TailwindCSS         |
| Backend      | Spring Boot 3.x (3 microservices)     |
| Database     | MongoDB Atlas                         |
| Auth         | JWT (RS256)                           |
| Cloud        | AWS (EKS, S3, CloudFront, Route53)    |
| IaC          | Terraform (modular)                   |
| CI/CD        | Jenkins                               |
| Containers   | Docker + Kubernetes                   |
| API Docs     | Swagger / OpenAPI 3.0                 |
| Scanning     | Trivy (container security)            |
| Quality Gate | SonarCloud                            |

## Services

| Service         | Port | Responsibilities                          |
|-----------------|------|-------------------------------------------|
| user-service    | 8081 | Auth, JWT, RBAC, Organization management  |
| product-service | 8082 | Products, Inventory, Stock tracking       |
| order-service   | 8083 | Orders, Billing simulation, Order history |

## Roles

| Role        | Access                                              |
|-------------|-----------------------------------------------------|
| ADMIN       | Full system access, user management, audit logs     |
| DISTRIBUTOR | Product catalog, stock management, orders           |
| HOSPITAL    | View products, place/track orders                   |

## Project Structure

```
├── frontend/              # React + Vite frontend
├── user-service/          # Spring Boot - Auth & User management
├── product-service/       # Spring Boot - Product & Inventory
├── order-service/         # Spring Boot - Orders & Billing
├── docker/                # Dockerfiles & Docker Compose
├── k8s/                   # Kubernetes manifests (EKS-ready)
├── terraform/             # AWS infrastructure (modular)
├── jenkins/               # CI/CD pipeline definitions
└── docs/                  # Deployment documentation
```

## Quick Start

### Local Development (without Docker)
See [MANUAL_DEPLOYMENT.md](docs/MANUAL_DEPLOYMENT.md)

### Docker Compose
See [DOCKER_DEPLOYMENT.md](docs/DOCKER_DEPLOYMENT.md)

### Kubernetes / EKS
See [KUBERNETES_DEPLOYMENT.md](docs/KUBERNETES_DEPLOYMENT.md)

### AWS Infrastructure (Terraform)
See [TERRAFORM_DEPLOYMENT.md](docs/TERRAFORM_DEPLOYMENT.md)

### Jenkins CI/CD
See [JENKINS_DEPLOYMENT.md](docs/JENKINS_DEPLOYMENT.md)

## Prerequisites

- Java 17+
- Node.js 18+
- Docker & Docker Compose
- kubectl & helm
- Terraform 1.5+
- AWS CLI configured
- MongoDB Atlas account

## Environment Variables

Each service uses `.env` files (not committed). Copy from `.env.example` in each service directory.

## Security

- All inter-service communication is authenticated
- JWT tokens signed with RS256
- Secrets managed via Kubernetes Secrets / AWS Secrets Manager
- All audit actions logged to `audit_logs` collection
- Trivy scan on every Docker image build

## License

Private / Proprietary — EduBlitz DevOps Project
