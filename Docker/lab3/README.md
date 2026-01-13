# Lab 5: Multi-Stage Build for Java Spring Boot App

This project demonstrates how to use **Multi-stage builds** in Docker to optimize image size. By separating the build environment from the runtime environment, we create a much smaller and more secure final image.

---

## 🚀 Step 1: Clone the Application
Clone the repository to get the source code.

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1

```

> **Screenshot:**
>
><img width="1109" height="226" alt="clone lab5-repo" src="https://github.com/user-attachments/assets/1e4e5df3-6b4a-4052-a943-b39662d0e8ea" />
 

---

## 🏗️ Step 2: Multi-Stage Dockerfile Configuration

We created a `Dockerfile` using two stages:

1. **Build Stage:** Uses a Maven image to compile and package the app.
2. **Runtime Stage:** Uses a lightweight Java JRE image to run the compiled JAR.

**Dockerfile Content:**

```dockerfile
# Stage 1: Build
FROM maven:4.0.0-rc-5-eclipse-temurin-17-alpine AS build
WORKDIR /lab5
COPY . .
RUN mvn package

# Stage 2: Runtime
FROM eclipse-temurin:17.0.17_10-jdk-alpine-3.23
WORKDIR /final
COPY --from=build /lab5/target/demo-0.0.1-SNAPSHOT.jar .
EXPOSE 8080
CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]

```

> **Screenshot (Dockerfile):**
>
> <img width="602" height="316" alt="Dockerfile" src="https://github.com/user-attachments/assets/0fa58f8d-ef88-4dfa-b6f9-e120aa8cc9e9" />


---

## 📦 Step 3: Build app3 Image

Build the image and observe the size difference compared to single-stage images.

```bash
docker build -t lab5 .
docker images

```

> **Screenshot (Image Size):**
>
> <img width="1170" height="554" alt="docker build" src="https://github.com/user-attachments/assets/87d76ff2-58e7-40c5-a34e-aeb7c58c0bda" />


---

## ▶️ Step 4: Run container3

Run the optimized container.

```bash
docker run -d --name container5 -p 8083:8080 app5

```

> **Screenshot (Running Container):**
>
><img width="1180" height="224" alt="docker run" src="https://github.com/user-attachments/assets/3e61a23c-3eb8-4d9e-bfa0-879d65c94a14" />
 

---

## 🧪 Step 5: Test the Application

Verify that the application is running correctly on port 8080.

> **Screenshot (Testing):**
>
> <img width="1182" height="126" alt="test the app" src="https://github.com/user-attachments/assets/c61e7cc7-5138-43cd-b3d8-d5d81e45fbed" />


---

## 🧹 Step 6: Cleanup

Stop and remove the container.

```bash
docker stop container5
docker rm container5
docker ps -a

```

> **Screenshot (Cleanup):**
>
> <img width="1182" height="203" alt="stop   remove container" src="https://github.com/user-attachments/assets/ffe08ea9-eca5-41e1-afe3-e188f3056df9" />


---

## 💡 Why Multi-Stage?

* **Smaller Image Size:** The final image doesn't contain Maven or source code, only the JAR and JRE.
* **Security:** Fewer tools in the final image mean a smaller attack surface.
* **Efficiency:** Faster deployment and lower storage costs.
