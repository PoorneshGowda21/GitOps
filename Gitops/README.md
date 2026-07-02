# VProfile GitOps Project

This repository contains a full end-to-end deployment setup for the VProfile application using a Java web app, Kubernetes/Helm manifests, and Terraform-based AWS infrastructure provisioning.

It is organized into three main parts:

- [vprofile-app](vprofile-app): the VProfile Java web application built with Spring MVC, Spring Security, JPA, MySQL, RabbitMQ, Elasticsearch, and JSP.
- [vprofile-helm](vprofile-helm): Helm charts, Kubernetes manifests, and ArgoCD configuration for deploying the application stack.
- [vprofile-infra](vprofile-infra): Terraform code to provision an AWS EKS environment and supporting network resources.

## Project Overview

The goal of this project is to deploy the VProfile application on Kubernetes in a GitOps-friendly way:

1. Provision the AWS infrastructure with Terraform.
2. Build and package the Java application.
3. Deploy the application and its supporting services with Helm or ArgoCD.
4. Expose the application through ingress and manage secrets securely.

## Repository Structure

```text
.
├── vprofile-app/        # Spring MVC web application source code
├── vprofile-helm/       # Helm chart, manifests, and ArgoCD config
└── vprofile-infra/      # Terraform infrastructure for AWS EKS
```

## Prerequisites

Before using this repository, make sure you have the following installed:

- Java 17
- Maven
- Docker
- kubectl
- Helm
- Terraform
- AWS CLI
- Access to an AWS account
- An existing Kubernetes cluster or EKS environment

## 1. Build the Application

Navigate to the application folder and build the WAR package:

```bash
cd vprofile-app
mvn clean package
```

This produces a deployable application artifact for the containerized or Kubernetes deployment workflow.

## 2. Provision Infrastructure

Navigate to the infrastructure folder and initialize Terraform:

```bash
cd vprofile-infra
terraform init
terraform plan
terraform apply
```

This provisions the AWS VPC, EKS cluster, node group, and supporting IAM resources.

## 3. Deploy with Helm

From the Helm directory:

```bash
cd vprofile-helm
kubectl create namespace vprofile
helm install vprofile ./helm/vprofile -n vprofile
```

To upgrade later:

```bash
helm upgrade vprofile ./helm/vprofile -n vprofile
```

You can also render the manifests locally:

```bash
helm template vprofile ./helm/vprofile -n vprofile
```

## 4. Deploy with ArgoCD

If you are using ArgoCD, apply the project and application manifests:

```bash
kubectl apply -f vprofile-helm/argocd/project/vprofile-project.yaml
kubectl apply -f vprofile-helm/argocd/app/vprofile-project.yaml
```

## Application Stack

The deployed stack typically includes:

- VProfile application
- MySQL database
- Memcached
- RabbitMQ
- Ingress configuration
- Kubernetes secrets

## Configuration Notes

Important configuration files include:

- [vprofile-app/src/main/resources/application.properties](vprofile-app/src/main/resources/application.properties)
- [vprofile-helm/helm/vprofile/values.yaml](vprofile-helm/helm/vprofile/values.yaml)
- [vprofile-infra/variables.tf](vprofile-infra/variables.tf)

For production use, avoid storing sensitive values directly in Git. Use a secret management tool such as Sealed Secrets, External Secrets Operator, SOPS, or ArgoCD Vault Plugin.

## Useful Commands

Check the deployed resources:

```bash
kubectl get pods -n vprofile
kubectl get svc -n vprofile
kubectl get ingress -n vprofile
```

Remove the Helm release if needed:

```bash
helm uninstall vprofile -n vprofile
```

## Notes

- The application is a Java-based web application packaged as a WAR.
- The deployment workflow is designed to be GitOps-friendly.
- The infrastructure and deployment manifests are intentionally separated for easier maintenance and reuse.

## License

No license file is currently included in this repository. Add one if you plan to distribute or reuse this project publicly.
