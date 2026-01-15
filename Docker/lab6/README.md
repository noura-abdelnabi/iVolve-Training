## 📌 Lab 8: Custom Docker Network for Microservices

### 🎯 Objective

* Containerize frontend and backend applications
* Create and use a custom Docker network
* Verify communication between containers
* Understand the difference between custom and default Docker networks

---

### 🧩 Lab Architecture

* Backend: Python Flask App
* Frontend: Python App
* Network: Custom Docker Bridge Network (`ivolve-network`)

---

### 📥 Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/Docker5.git
cd Docker5
```

📸 **Screenshot:**

> Clone repository successfully
> <img width="1053" height="201" alt="clone lab8-repo" src="https://github.com/user-attachments/assets/af97f892-b049-4721-955e-bddc95486151" />

---

### 🐳 Backend Dockerfile

```dockerfile
FROM python:3.15.0a3-alpine3.23
WORKDIR /lab8
COPY . .
RUN pip install flask
EXPOSE 5000
CMD ["python", "app.py"]
```

Build backend image:

```bash
docker build -t backend-image .
```

📸 **Screenshot:**

> Backend image build
> 
> <img width="452" height="238" alt="Dockerfile for backend" src="https://github.com/user-attachments/assets/26251bb8-3f7c-47c0-b5c4-56e118fd078a" />
>
> <img width="983" height="297" alt="build backend-image" src="https://github.com/user-attachments/assets/39f708eb-ba22-41fd-b5a2-6db3d396968a" />

---

### 🐳 Frontend Dockerfile

```dockerfile
FROM python:3.15.0a3-alpine3.23
WORKDIR /lab8
COPY . .
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]
```

Build frontend image:

```bash
docker build -t frontend-image .
```

📸 **Screenshot:**

> Frontend image build
>
> <img width="517" height="224" alt="Dockerfile for frontend" src="https://github.com/user-attachments/assets/b94df563-a1b1-4f39-afa8-a8df41bd89b7" />
>
> <img width="987" height="294" alt="build frontend-image" src="https://github.com/user-attachments/assets/cdb63d83-b335-479e-a204-6c31cfc50859" />

---

### 🌐 Create Custom Network

```bash
docker network create ivolve-network
```

📸 **Screenshot:**

> Docker network created
> <img width="986" height="179" alt="network create" src="https://github.com/user-attachments/assets/3f2b2949-9e79-45a1-a031-e066d839c316" />


---

### ▶️ Run Containers

#### Backend Container

```bash
docker run -d --name backend-container --network ivolve-network  backend-image
```

#### Frontend1 (Custom Network)

```bash
docker run -d --name frontend-container --network ivolve-network -p 5001:5000 frontend-image
```

#### Frontend2 (Default Network)

```bash
docker run -d --name frontend2-container -p 5002:5000 frontend-image
```

📸 **Screenshot:**

> Running containers
> <img width="1028" height="203" alt="3 cont" src="https://github.com/user-attachments/assets/786a71ff-0a8e-4523-a52c-00881f781fe4" />

---

### 🔍 Verify Communication

```bash
docker exec -it frontend-container ping backend-container
```

✔️ Successful communication

```bash
docker exec -it frontend2-container ping backend-container
```

❌ Failed communication (different network)

📸 **Screenshot:**

> Network communication test
> <img width="1047" height="379" alt="verifying" src="https://github.com/user-attachments/assets/2c7d053d-d9c8-498d-8d15-dc1b3b7e28bf" />

---

### 🧹 Cleanup

```bash
docker stop frontend-container frontend2-container backend-container
docker rm frontend-container frontend2-container backend-container
docker network rm ivolve-network
docker network ls
```

📸 **Screenshot:**

> Network removed
> <img width="682" height="181" alt="rm net" src="https://github.com/user-attachments/assets/eecc230e-939e-4c87-89db-4e993ea5adff" />

---
