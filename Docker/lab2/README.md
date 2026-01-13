# Lab 4: Run Java Spring Boot App in a Container

This project demonstrates the full process of containerizing a Spring Boot application using Docker.

---

## 🚀 Step 1: Clone the Application
First, we clone the source code from the repository.

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git

```

> **Screenshot:**
>
> <img width="893" height="278" alt="clone LAB4-REPO" src="https://github.com/user-attachments/assets/27fc88d7-e93c-4017-b911-c92027e05627" />

---

## 🛠️ Step 2: Build the Application

We build the project to generate the executable JAR file.

```bash
./mvn package

```

> **Screenshot:**
>
> <img width="899" height="246" alt="build app" src="https://github.com/user-attachments/assets/ddda44ec-77e5-4709-a1f0-3e012fd95c7d" />


---

## 🐳 Step 3: Write Dockerfile

A `Dockerfile` was created with the following requirements:

* Base image: `eclipse-temurin:17.0.17_10-jdk-alpine-3.23`
* Work directory: `/lab4`
* Port: `8080`

> **Screenshot (Dockerfile Content):**
>
> <img width="572" height="171" alt="Dockerfile" src="https://github.com/user-attachments/assets/848e5c3a-163a-4f3b-810b-7478b4bb69ec" />


---

## 🏗️ Step 4: Build app2 Image

Building the Docker image and checking its size as requested.

```bash
docker build -t app2 .
docker images

```

> **Screenshot (Build & Image Size):**
>
> <img width="1170" height="575" alt="docker build" src="https://github.com/user-attachments/assets/47744c3b-446c-43ad-a3f3-001f840110e8" />


---

## ▶️ Step 5: Run container2

Launching the container from the `app2` image.

```bash
docker run -d -p 8080:8080 --name container2 app2

```

> **Screenshot (Running Container):**
>
> <img width="1181" height="216" alt="docker run" src="https://github.com/user-attachments/assets/4ea4478b-4ad0-4291-bd92-d21f458df64e" />


---

## 🧪 Step 6: Test the Application

Testing the application in the browser or via terminal to ensure it's working.

> **Screenshot (Application Preview):**
>
> <img width="1180" height="98" alt="test the app" src="https://github.com/user-attachments/assets/5e2b184e-8b8c-44cd-a8d7-d1360edc686e" />


---

## 🧹 Step 7: Stop and Delete

Cleaning up the environment by stopping and removing the container.

```bash
docker stop container2
docker rm container2

```

> **Screenshot (Cleanup):**
>
> <img width="1175" height="193" alt="stop   remove container" src="https://github.com/user-attachments/assets/7cf46ef3-19ed-4cd9-8463-4c5506dc0519" />


```
