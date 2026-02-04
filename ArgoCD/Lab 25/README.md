# 🚀 Lab 25: Fully Automated GitOps Pipeline (CI/CD)
This project demonstrates a production-grade **GitOps** workflow using **Jenkins** for Continuous Integration and **ArgoCD** for Continuous Deployment on a Kubernetes cluster.

## 🎯 Objective
Automate the process of building a Java application, containerizing it, and deploying it to Kubernetes whenever a code change is pushed to GitHub, ensuring the cluster state always matches the Git repository.

---

## 🛠 Tech Stack
* **Jenkins:** Pipeline Orchestration
* **Maven:** Java Application Build
* **Docker:** Containerization
* **GitHub:** Source Control & GitOps Manifest Storage
* **ArgoCD:** GitOps CD Controller
* **Kubernetes:** Application Runtime

---

## 🏗 Pipeline Architecture


1. **Commit:** Developer pushes code to GitHub.
2. **CI (Jenkins):**
   * Triggers the pipeline.
   * Compiles the code using Maven.
   * Builds a Docker image with a dynamic tag (Build Number).
   * Pushes the image to Docker Hub.
3. **Manifest Update:** Jenkins updates the `k8s/deployment.yaml` with the new image tag.
4. **CD (ArgoCD):** * Detects the change in GitHub.
   * Syncs the new state to the Kubernetes Cluster.

---

## 📸 Project Milestones (Screenshots)

### 1️⃣ Continuous Integration (Jenkins)
The Jenkins pipeline successfully executes all stages: Maven Build, Docker Image Push, and GitHub Manifest Update.
> **Note:** We used `withCredentials` to securely handle Docker Hub and GitHub tokens.
>
> <img width="1439" height="372" alt="pipeline success" src="https://github.com/user-attachments/assets/1d643052-2b48-47f7-b256-ac0a79c2962c" />

### 2️⃣ Docker Hub Registry
The image is tagged dynamically using `${env.BUILD_NUMBER}` to ensure versioning and easy rollbacks.
>
> <img width="1136" height="545" alt="dockerhub image" src="https://github.com/user-attachments/assets/7334cca7-4c03-44ee-a2b7-8eac99c39ff1" />

### 3️⃣ GitOps Manifest Update
Jenkins automatically commits the new image tag to the repository, which serves as the "Source of Truth" for ArgoCD.
>
> <img width="1355" height="665" alt="deployment image tag edited" src="https://github.com/user-attachments/assets/1442a972-5b53-45e8-bfa0-6de9928fa5ab" />

### 4️⃣ Continuous Deployment (ArgoCD)
ArgoCD monitors the `k8s/` folder. Once the commit is detected, it triggers an automated Sync to update the running application.
>
> <img width="1193" height="705" alt="svc   deployment success" src="https://github.com/user-attachments/assets/758294bf-9e89-44de-8592-d9ff0c6fcfde" />
>
> <img width="1197" height="699" alt="rs pods success" src="https://github.com/user-attachments/assets/3e1dbdfd-1e45-4503-8dba-e8e9e510749a" />

---

## 🚀 How to Run
1. Create a Jenkins Pipeline Job pointing to this repository.
2. Configure `docker-hub-creds` and `github-token` in Jenkins Credentials.
3. Install ArgoCD on your K8s cluster.
4. Create an ArgoCD App pointing to the `k8s/` directory of this repo.
5. Push a change and watch the magic happen! ✨
