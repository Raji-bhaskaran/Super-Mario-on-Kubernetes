Super Mario on Kubernetes

Deploy the classic Super Mario game on Amazon EKS (Elastic Kubernetes Service) using Terraform for infrastructure provisioning.

Project Overview
This project demonstrates modern DevOps practices by deploying a containerized Super Mario game on Kubernetes infrastructure provisioned with Terraform. Perfect for learning Infrastructure as Code (IaC) and container orchestration.

## Architecture

- Infrastructure: AWS EKS cluster provisioned with Terraform
- Application: Containerized Super Mario HTML5 game  
- Load Balancer: AWS Application Load Balancer for external access
- Container Registry: Docker Hub (rajibhaskaran/mario:latest)
- Orchestration: Kubernetes for deployment and scaling

## Technologies Used

- AWS EKS - Managed Kubernetes service
- Terraform - Infrastructure as Code
- Kubernetes - Container orchestration  
- Docker - Containerization
- NGINX - Web server inside container
- HTML5/JavaScript - Super Mario game

## Prerequisites

- AWS Account with appropriate permissions
- AWS CLI configured with credentials
- Terraform installed (v1.0+)
- kubectl installed
- Docker Desktop running
- Git installed

## Quick Start

### 1. Clone the Repository
```
git clone https://github.com/Raji-bhaskaran/Super-Mario-on-Kubernetes.git
cd Super-Mario-on-Kubernetes
```

### 2. Configure AWS Backend
Edit EKS-TF/backend.tf with your S3 bucket details

### 3. Deploy Infrastructure
```
cd EKS-TF
terraform init
terraform validate
terraform plan
terraform apply -auto-approve
```

### 4. Configure kubectl
```
aws eks update-kubeconfig --name EKS_CLOUD --region your-region
```

### 5. Deploy the Game
```
cd ..
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 6. Get Game URL
```
kubectl get services mario-service
```
Copy the EXTERNAL-IP and open it in your browser.

## Project Structure

```
Super-Mario-on-Kubernetes
├── EKS-TF/
│   ├── backend.tf          # Terraform backend configuration
│   ├── main.tf             # EKS cluster and node group
├── deployment.yaml         # Kubernetes deployment manifest
├── service.yaml           # Kubernetes service (LoadBalancer)
├── README.md              # Project documentation

```

## Troubleshooting

### Game Not Loading
```
# Check pods are running
kubectl get pods

# Check service status  
kubectl get services

# View pod logs
kubectl logs deployment/mario-deployment
```

### Load Balancer Issues
- Verify AWS security groups allow port 80
- Check if EKS cluster is in correct region
- Ensure IAM roles have proper permissions

### Terraform Errors
- Verify AWS CLI credentials: aws sts get-caller-identity
- Check S3 bucket exists and is accessible
- Ensure region consistency across all configs

## What I Learned

- Infrastructure as Code (IaC) with Terraform  
- Kubernetes deployment and service management  
- AWS EKS cluster provisioning and configuration  
- Container orchestration with Kubernetes  
- Load balancer setup for external access  
- DevOps best practices for cloud-native applications  

## Cleanup Resources

Important: Always cleanup to avoid AWS charges

```
# Delete Kubernetes resources
kubectl delete service mario-service
kubectl delete deployment mario-deployment

# Destroy Terraform infrastructure  
cd EKS-TF
terraform destroy -auto-approve

# Verify cleanup
aws eks list-clusters --region your-region
```

## Features

- Auto-scaling capabilities with Kubernetes
- High availability with multiple replicas
- Secure deployment with AWS IAM roles
- Monitoring ready with Kubernetes native tools
- Fast deployment with Infrastructure as Code

## Acknowledgments
- Super Mario game assets from open-source HTML5 implementation
- K21Academy for the project guidance
