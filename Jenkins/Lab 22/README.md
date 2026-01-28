# Lab 22: Comprehensive CI/CD Pipeline for Java App with Kubernetes

## 📝 Description
This project demonstrates a production-grade CI/CD pipeline using **Jenkins**. The pipeline automates the entire software development lifecycle—from code validation to containerization and final deployment on a **Kubernetes (Minikube)** cluster.

## 🚀 Pipeline Workflow
The `Jenkinsfile` is designed with 7 automated stages:
1. **Unit Test**: Validates the application logic.
2. **Build App**: Compiles the Java code into a JAR file using **Maven**.
3. **Build Docker Image**: Build a lightweight container image.
4. **Push to Docker Hub**: Uploads the versioned image to a central registry.
5. **Delete Local Image**: Maintains a clean build environment by removing local images.
6. **Edit deployment.yaml**: Automatically patches the Kubernetes manifest with the new build tag.
7. **Deploy to K8s**: Orchestrates the deployment to **Minikube**.



---

## 🛠️ Tech Stack
* **Continuous Integration:** Jenkins
* **Build Tool:** Maven (Java 17)
* **Containerization:** Docker
* **Orchestration:** Kubernetes (Minikube)
* **Version Control:** Git & GitHub

---

## 📖 Implementation Steps (Guided Setup)

### 1. Prerequisites
Ensure your Ubuntu server has the following installed:
* **Jenkins** (with Pipeline and Docker plugins)
* **Docker Engine**
* **Minikube & Kubectl**
* **Maven**

### 2. Permissions Configuration
For the pipeline to run without errors, grant Jenkins access to Docker and Kubernetes:
```bash
# Docker permissions
sudo usermod -aG docker jenkins
sudo chmod 666 /var/run/docker.sock

# Kubernetes config for Jenkins
sudo mkdir -p /var/lib/jenkins/.kube
sudo cp ~/.kube/config /var/lib/jenkins/.kube/
sudo chown -R jenkins:jenkins /var/lib/jenkins/.kube

```

### 3. Jenkins Credentials Setup

In the Jenkins dashboard, add **Global Credentials**:

* **ID:** `docker-hub-creds`
* **Type:** Username with Password (Your Docker Hub credentials)

### 4. Repository Structure

Ensure your files are organized as follows:

```text
.
└── Jenkins/
    └── Lab 22/
        ├── Jenkinsfile     # Pipeline definition
        ├── Dockerfile      # Container instructions
        ├── deployment.yaml # K8s manifest
        └── pom.xml         # Maven configuration

```

### 5. Running the Pipeline

1. Create a **New Item** in Jenkins (Pipeline).
2. Under **Pipeline Definition**, select **Pipeline script from SCM**.
3. Provide your Repository URL and branch (`main`).
4. Set the script path to `Jenkins/Lab 22/Jenkinsfile`.
5. Click **Build Now**.

---

## 📸 Proof of Success

### Jenkins Stage View
>
> <img width="1875" height="465" alt="success" src="https://github.com/user-attachments/assets/67b36f30-a1ba-4e8b-852c-cd08e39b8df0" />

### Docker Hub
>
> <img width="1588" height="323" alt="image on dockrhub" src="https://github.com/user-attachments/assets/eef45795-b4bb-48d5-9b77-231d54910ebf" />

### Kubernetes Status

*Deployment and Service running on Minikube.*
