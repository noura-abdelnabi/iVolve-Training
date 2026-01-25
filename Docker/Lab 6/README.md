## 🔹 Lab 6: Managing Docker Environment Variables Across Build and Runtime

### 🎯 Objective

* Build a Docker image for a Flask application
* Run multiple containers with environment variables set using:

  * Command line
  * Environment file
  * Dockerfile

---

### 🛠️ Steps

#### 1️⃣ Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3
```

>📸 Screenshot:
>
><img width="1179" height="246" alt="clone lab6-repo" src="https://github.com/user-attachments/assets/653797dc-d06d-41b4-8e8c-9100a5c3832a" />


---

#### 2️⃣ Create Dockerfile

Dockerfile uses:

* Python base image
* Flask installation
* Port 8080 exposure
* Default environment variables (production)

```Dockerfile
FROM python:3.15.0a3-alpine3.23
WORKDIR /lab6
COPY . .
RUN pip install flask
EXPOSE 8080
CMD ["python", "app.py"]
```

> 📸 Screenshot:
>
> <img width="567" height="234" alt="Dockerfile" src="https://github.com/user-attachments/assets/3d089376-6ebe-400d-ae13-f97b7c8c3497" />


---

#### 3️⃣ Build Docker Image

```bash
docker build -t imaeg1 .
```

> 📸 Screenshot:
>
> <img width="1164" height="290" alt="docker build" src="https://github.com/user-attachments/assets/3686764a-6a83-4cd5-b7d4-0177f42745ac" />


---

#### 4️⃣ Run Containers with Environment Variables

##### 🔹 a) Using Command Line Variables

```bash
docker run -d -p 8081:8080 \
-e APP_MODE=development \
-e APP_REGION=us-east \
--name container6.1 image1
```

> 📸 Screenshot:
>
> <img width="1179" height="181" alt="setting env by cli" src="https://github.com/user-attachments/assets/8946338f-9150-43eb-be34-6b2c23004583" />


---

##### 🔹 b) Using Environment File

Create `env.txt`:

```env
APP_MODE=staging
APP_REGION=us-west
```
> 📸 Screenshot:
>
> <img width="389" height="165" alt="env file" src="https://github.com/user-attachments/assets/9a5db7bf-599a-4fbd-a67f-2ca7e63a2620" />



Run container:

```bash
docker run -d -p 8082:8080 \
--env-file=env \
--name container6.2 image1
```

> 📸 Screenshot:
>
> <img width="1175" height="156" alt="setting env by file" src="https://github.com/user-attachments/assets/bcf7b942-54dc-4ff0-a671-661a7d1c8853" />


---

##### 🔹 c) Using Dockerfile Environment Variables

```Dockerfile
FROM python:3.15.0a3-alpine3.23
WORKDIR /lab6
COPY . .
ENV APP_MODE=production APP_REGION=canada-west
RUN pip install flask
EXPOSE 8080
CMD ["python", "app.py"]
```

Build New Docker Image
```bash
docker build -t imaeg2 .
```

```bash
docker run -d -p 8083:8080 \
--name contauner6.3 image2
```

> 📸 Screenshot:
>
> <img width="583" height="233" alt="setting env inside the docker file" src="https://github.com/user-attachments/assets/8cc265dc-3cc9-4089-8508-11f5a4deea7d" />
>
> <img width="1158" height="316" alt="building new image with the env insde the dockerfile" src="https://github.com/user-attachments/assets/3ab2e51e-8828-4a74-87d8-8e6d2214e9e4" />
>
> <img width="1177" height="152" alt="run container6 3" src="https://github.com/user-attachments/assets/e2930514-2bb5-407a-9c5e-b6d52e5f3cad" />


---

#### 5️⃣ Verify Running Containers

```bash
docker ps
curl localhost:8081
curl localhost:8082
curl localhost:8083
```

> 📸 Screenshot:
>
> <img width="792" height="46" alt="test the containe6 1" src="https://github.com/user-attachments/assets/7d0e404f-f5bf-4378-94ce-21e9d48c0e00" />
>
> <img width="873" height="49" alt="test the container6 2" src="https://github.com/user-attachments/assets/50b7982c-49e0-4ad8-a870-6d4bb4c81a6d" />
>
> <img width="574" height="42" alt="test container6 3" src="https://github.com/user-attachments/assets/06ca9b62-43d3-4efe-bb3d-539ca2bd6cd5" />


