# 🚀 VProfile GitOps Deployment on AWS EKS

This repository contains a complete **GitOps implementation** for deploying the **VProfile Java Web Application** on **Amazon EKS** using modern DevOps tools and best practices.

The project demonstrates an end-to-end CI/CD and GitOps workflow, starting from infrastructure provisioning with Terraform to automated Kubernetes deployments using ArgoCD.

This project is based on the **Udemy Course: Decoding DevOps – From Basics to Advanced Projects with AI** by **Imran Teli**, with additional customizations and improvements.

---

# 📌 Project Architecture

The project consists of three independent repositories combined into a single repository for easier maintenance.

- **vprofile-app**
  - Java Spring MVC Application
  - Docker configuration
  - Maven Build
  - SonarQube Configuration

- **vprofile-helm**
  - Helm Charts
  - Kubernetes Manifests
  - ArgoCD Applications
  - Ingress Configuration
  - Secrets & Configurations

- **vprofile-infra**
  - Terraform Infrastructure
  - AWS VPC
  - Amazon EKS Cluster
  - Node Groups
  - IAM Roles
  - S3 Backend
  - Load Balancer Controller

---

# 🛠 Technologies Used

### Cloud

- AWS EC2
- Amazon EKS
- Amazon ECR
- Amazon VPC
- IAM
- ACM
- Route53 / DuckDNS
- S3
- Security Groups

### DevOps

- Git
- GitHub
- Docker
- Kubernetes
- Helm
- ArgoCD
- Terraform
- AWS CLI
- kubectl
- eksctl

### Application

- Java
- Spring MVC
- Spring Security
- Hibernate
- JSP
- Maven

### Supporting Services

- MySQL
- RabbitMQ
- Memcached

---

# 📂 Repository Structure

```text
.
├── vprofile-app/
│   ├── src/
│   ├── Docker-files/
│   ├── pom.xml
│   └── sonar-project.properties
│
├── vprofile-helm/
│   ├── helm/
│   ├── kubedefs/
│   ├── argocd/
│   └── README.md
│
├── vprofile-infra/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── backend.tf
│   └── iam_policy.json
│
└── README.md
```

---

# 🚀 Project Workflow

The deployment follows a complete GitOps workflow.

### Step 1

Provision AWS Infrastructure using Terraform.

- Create VPC
- Public & Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- IAM Roles
- Amazon EKS Cluster
- Managed Node Group

---

### Step 2

Configure AWS CLI and Terraform Backend.

- IAM User
- AWS CLI Configuration
- Remote Terraform State in S3

---

### Step 3

Configure Kubernetes.

- Install kubectl
- Install Helm
- Install eksctl
- Configure kubeconfig

---

### Step 4

Install AWS Load Balancer Controller.

- IAM Policy
- IAM Service Account
- Helm Installation

---

### Step 5

Containerize the application.

- Build WAR
- Build Docker Image
- Push Image to Amazon ECR

---

### Step 6

Deploy supporting services using Helm.

- MySQL
- RabbitMQ
- Memcached

---

### Step 7

Deploy VProfile Application.

- Deployment
- Service
- Persistent Volume
- Secrets
- Configurations

---

### Step 8

Configure Ingress.

- AWS Application Load Balancer
- Host-based Routing
- SSL Certificate (AWS ACM)
- Custom Domain (GoDaddy / DuckDNS)

---

### Step 9

Configure ArgoCD.

- Install ArgoCD
- Create Project
- Create Application
- Git Repository Sync
- Automatic Deployment

---

# ⚙️ Prerequisites

Before running this project, install the following:

- Java 17
- Maven
- Docker
- Git
- kubectl
- Helm
- Terraform
- AWS CLI
- eksctl
- AWS Account
- GitHub Account

---

# 📦 Build the Application

```bash
cd vprofile-app

mvn clean package
```

---

# 🐳 Build Docker Image

```bash
docker build -t vprofile .

docker tag vprofile:latest <ECR-Repository>

docker push <ECR-Repository>
```

---

# ☁️ Provision AWS Infrastructure

```bash
cd vprofile-infra

terraform init

terraform plan

terraform apply
```

---

# ☸ Configure Kubernetes

Update kubeconfig

```bash
aws eks update-kubeconfig \
--region us-east-1 \
--name vprofile-eks-cluster
```

Verify

```bash
kubectl get nodes
```

---

# 📦 Deploy using Helm

```bash
cd vprofile-helm

kubectl create namespace vprofile

helm install vprofile ./helm/vprofile \
-n vprofile
```

Upgrade

```bash
helm upgrade vprofile ./helm/vprofile \
-n vprofile
```

---

# 🚀 Deploy using ArgoCD

Apply Project

```bash
kubectl apply -f argocd/project/
```

Apply Application

```bash
kubectl apply -f argocd/application/
```

Verify

```bash
kubectl get applications -n argocd
```

---

# 🌐 Application Access

The application is exposed using:

- AWS Application Load Balancer
- Kubernetes Ingress
- DuckDNS / Custom Domain
- AWS Certificate Manager (SSL)

Example

```
https://vprofile.your-domain.com
```

---

# 📋 Useful Commands

Pods

```bash
kubectl get pods -A
```

Services

```bash
kubectl get svc -A
```

Ingress

```bash
kubectl get ingress -A
```

Namespaces

```bash
kubectl get ns
```

Helm Releases

```bash
helm list -A
```

Terraform

```bash
terraform plan

terraform apply

terraform destroy
```

---

# 📸 Project Output

Screenshots of the completed project can be found inside the **OUTPUT/** directory.

These include:

- AWS Infrastructure
- EKS Cluster
- Terraform Execution
- Docker Build
- Amazon ECR
- Helm Deployment
- Kubernetes Pods
- ArgoCD Dashboard
- Application Load Balancer
- Final Running Application

---

# 🎯 Learning Outcomes

This project helped in understanding:

- GitOps Workflow
- Infrastructure as Code (Terraform)
- Kubernetes Deployment
- Helm Packaging
- Amazon EKS
- AWS Networking
- IAM & Security
- Docker Containerization
- Amazon ECR
- ArgoCD Continuous Deployment
- AWS Load Balancer Controller
- ACM SSL Integration
- Domain Configuration
- CI/CD Best Practices

---

# 🙏 Acknowledgements

This project is based on the Udemy course:

**Decoding DevOps – From Basics to Advanced Projects with AI**

Instructor:

**Imran Teli**

The project has been customized and extended with additional configurations, repository organization, deployment improvements, and documentation.

---

# 📜 License

This repository is intended for educational and learning purposes.

Feel free to fork, modify, and learn from the implementation while giving proper credit to the original course and instructor.
