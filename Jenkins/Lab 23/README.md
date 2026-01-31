## Lab 23: Jenkins Shared Library Pipeline for Spring Boot App

### Project Overview

This project demonstrates a complete CI/CD Pipeline for a Spring Boot application using:

* **Jenkins Shared Library** for reusable code.
* **Maven** for building and testing.
* **Trivy** for security scanning.
* **Docker** for containerization.
* **Kubernetes (Minikube)** for deployment.

---

### **Infrastructure & Components**

#### **1. Distributed Build Architecture (Jenkins Agent)**

* The Pipeline does not run on the Jenkins Master; it uses a dedicated **Linux Agent (Ubuntu VM)** to execute tasks.
* The Agent is connected via **SSH/JNLP**, providing an isolated environment for building and deploying.
* **Key Advantage**: Offloading work from the Master and scaling the infrastructure.

#### **2. Jenkins Shared Library**

* To follow **DRY (Don't Repeat Yourself)** principles, all core logic is moved to a central repository called `SahredLibrary-NTI`.
* **Custom Functions Used**:
* `buildApp()`: Handles Maven lifecycle.
* `buildAndPushImage()`: Manages Docker builds and pushes.
* `deployToK8s()`: Automates Kubernetes manifest application.


* **Benefits**: Centralized updates and cleaner Jenkinsfiles.

---

### **Screenshots to Include for these parts:**

1. **Nodes Management Screen**:
  >
  > <img width="723" height="341" alt="linux-agent" src="https://github.com/user-attachments/assets/09c3b482-d02e-41ab-8824-d6a81313faa0" />
  >
  >  "Jenkins Distributed Architecture showing the Linux Agent connected."


2. **Shared Library Definition in Jenkins**:
  >
  > <img width="1873" height="822" alt="SHARED LIB ON JENKINS" src="https://github.com/user-attachments/assets/88454e43-2b8d-41f4-9637-9b5a63801c5d" />
  > "Global Pipeline Libraries configuration in Jenkins."


3. **Library Structure (GitHub)**:
  >
  > <img width="1106" height="481" alt="shared-lib repo" src="https://github.com/user-attachments/assets/436b478f-d933-4877-a809-c22d9ee683fc" /> 
  > "Structure of the Jenkins Shared Library repository."


---
### Pipeline Stages

1. **Checkout SCM**: Pulling code from GitHub.
2. **Unit Test & Build**: Running `mvn test` and `mvn package`.
3. **Docker Build**: Creating the image from Dockerfile.
4. **Security Scan**: Using **Trivy** to scan the image for vulnerabilities.
5. **Docker Push**: Uploading the image to Docker Hub.
6. **Deploy to K8s**: Applying the `deployment.yaml` to Minikube.

---

### Screenshots to Include

1. **Jenkins Stage View (The Blocks)**:
  >
  > <img width="1908" height="409" alt="success" src="https://github.com/user-attachments/assets/1686121d-b0d3-4af3-b9fb-75eecd0f2d33" />  
  > "Successful Pipeline Execution showing all stages."


2. **Maven Build Success**:
  >
  > <img width="1345" height="777" alt="mvn test" src="https://github.com/user-attachments/assets/4a2ce016-453a-482f-826f-9f89b396f7bb" />
  >
  > <img width="1520" height="825" alt="mvn package" src="https://github.com/user-attachments/assets/11e501d8-cc10-46f6-9278-8b7c1fadade1" />  
  > "Maven build and packaging success."


3. **Trivy Scan Results**:
  >
  > <img width="1556" height="826" alt="trivy scan" src="https://github.com/user-attachments/assets/e33fe665-ab25-433f-acd2-2d4f4b90f9b7" />
  > "Vulnerability scanning using Trivy."


4. **Docker Hub Repository**:
  >
  > 
  > "Docker Image pushed successfully to Docker Hub."


5. **Kubernetes Deployment**:
  >
  >
  > "Application deployed and running on Minikube."



---

### How to Run

1. Ensure **Minikube** is running: `minikube start`.
2. Set up Jenkins **Credentials** for Docker Hub and Kubernetes Token.
3. Run the Jenkins Pipeline.
