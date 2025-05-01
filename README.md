# vProfile CI/CD Project with EKS and GitHub Actions

This project demonstrates a complete CI/CD pipeline for a Java-based web application (`vprofile`) using modern DevOps practices and AWS cloud infrastructure. It covers the entire process from code validation to containerized deployment in EKS using Helm.

---

##  Tools & Technologies

- **GitHub Actions** – CI/CD automation
- **Maven** – Java build and test
- **SonarCloud** – Code quality analysis
- **Docker & Amazon ECR** – Containerization and image storage
- **Terraform** – Infrastructure as Code (created separately)
- **Amazon EKS** – Kubernetes cluster for deployment
- **Helm** – Kubernetes package manager

---

##  CI/CD Workflow Overview

The GitHub Actions workflow includes **three main stages**:

### 1.  Testing

- Checks out the code
- Builds using Maven
- Runs unit tests
- Performs code analysis via:
  - `checkstyle`
  - `sonar-scanner` with SonarCloud

### 2.  Build & Publish Docker Image

- Builds a Docker image using the application WAR
- Pushes the image to **Amazon ECR**
- Tags: `latest` and GitHub `run_number`

### 3.  Deploy to EKS

- Configures AWS credentials
- Updates kubeconfig for EKS cluster
- Creates a Kubernetes secret for ECR auth
- Deploys the Helm chart using dynamic values:
  - `image.repository`
  - `image.tag`

---

##  Helm Chart

Located at: `helm/vprofilecharts`

Dynamic values passed via `--set` in GitHub Actions:

```yaml
image:
  repository: <ECR URL>
  tag: <GitHub run number>
  pullPolicy: IfNotPresent
```

---

##  Notes

- No Route 53 domain is used — access will be through the **ALB DNS** created by the Ingress
- Secrets are stored securely in GitHub:
  - `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`
  - `REGISTRY`, `SONAR_TOKEN`, etc.

---

##  Status

**Project finalized and deployed on:** May 01, 2025

---

##  Author

Roberto Rodríguez  
CI/CD & Cloud Engineering Practice  
GitHub: [@kuota1](https://github.com/kuota1)


