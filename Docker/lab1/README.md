# Lab 3: Run Java Spring Boot App in a Container

This project demonstrates how to **Dockerize** a Java Spring Boot application by creating a custom Dockerfile, building a Docker Image, and running it as a Container.

## 🛠 Prerequisites
* Docker installed and running.
* Basic knowledge of Docker commands.

## 📝 Steps Performed

### 1. Clone the Application Code
First, I cloned the Spring Boot application source code:
```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git

```
> **Screenshot:**
> 
> <img width="1133" height="449" alt="clone lab3-repo" src="https://github.com/user-attachments/assets/48e980c7-4bfb-44b6-9199-c6e74db02f72" />


### 2. Write the Dockerfile

I created a `Dockerfile` in the project root with the following configuration:

* **Base Image:** Used Maven with Java 17.
* **Work Directory:** Set up a working directory inside the container.
* **Copy Source:** Copied the code into the container.
* **Build:** Used `mvn package` to build the app.
* **Command:** Configured it to run the generated JAR file from `target/demo-0.0.1-SNAPSHOT.jar`.
* **Port:** Exposed port `8080`.

> **Screenshot of Dockerfile:**
>
> <img width="610" height="239" alt="Dockerfile" src="https://github.com/user-attachments/assets/31840016-c7af-4262-853f-d7a830a35794" />


### 3. Build the Docker Image

I built the image and named it `lab3`:

```bash
docker build -t lab3 .

```

> **Screenshot of Build Process:**
>
> <img width="1241" height="478" alt="docker build" src="https://github.com/user-attachments/assets/e1857bb8-c7e1-4fbe-a2e9-de3ce34fadf9" />
>
> <img width="925" height="148" alt="docker images" src="https://github.com/user-attachments/assets/a0431239-0152-4541-b995-b9f6932092cd" />



### 4. Run the Container

I started a container named `container1` based on the `lab3` image:

```bash
docker run -d --name container1 -p 8081:8080 lab3

```

> **Screenshot of Run Process:**
>
> <img width="1226" height="238" alt="container run" src="https://github.com/user-attachments/assets/0e8e25fa-dda9-4dd7-bc41-4590b5af70f3" />



### 5. Test the Application

After running the container, I verified that the application is accessible.

> **Screenshot of Application Test:**
>
> <img width="1226" height="110" alt="test the application" src="https://github.com/user-attachments/assets/4b86e93f-c2ad-469e-aa72-b55bfddbd691" />


### 6. Cleanup

To stop and remove the container after testing:

```bash
docker stop container1
docker rm container1

```
> **Screenshot of Cleaning:**
>
> <img width="1245" height="366" alt="stop   delete the container" src="https://github.com/user-attachments/assets/5c5e16ef-e892-47fe-9139-821ed5bcf4c9" />

---
