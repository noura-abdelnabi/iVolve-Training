# Lab 2: Building and Packaging Java Applications with Maven

This project demonstrates the lifecycle of a Java application using **Apache Maven**.

## 🛠 Tech Stack
* **Build Tool:** Maven
* **Language:** Java

> **Screenshot:**
> 
> <img width="1073" height="178" alt="maven install" src="https://github.com/user-attachments/assets/c2db8c8e-52e8-4f43-9aea-e3cbe2006308" />

## 🚀 Steps Performed

### 1. Clone the Repository
First, I cloned the source code from the remote repository:
```bash
git clone https://github.com/Ibrahim-Adel15/build2.git

```
> **Screenshot:**
> 
> <img width="1222" height="650" alt="clone lab2-repo" src="https://github.com/user-attachments/assets/7daa2bb8-4818-4ad6-95cb-67e17f681d5d" />

### 2. Run Unit Tests

To ensure the code quality and that all features work as expected:

```bash
mvn test

```

> **Screenshot:**
> 
> <img width="715" height="688" alt="Run Unit Test" src="https://github.com/user-attachments/assets/c5bc6195-97e5-4716-8f0a-5383ff7a6fdd" />


### 3. Build and Package the Application

I generated the executable JAR file (artifact) using the build command:

```bash
mvn pakage
```

The artifact was successfully generated at:

`target/hello-ivolve-1.0-SNAPSHOT.jar`

> **Screenshot:**
> 
> <img width="1226" height="663" alt="build app to generate  jar file" src="https://github.com/user-attachments/assets/c363dc59-7a9d-4da1-aef3-2662aaff3222" />


### 4. Run and Verify the Application

Finally, I ran the application to verify it is working correctly:

```bash
java -jar target/hello-ivolve-1.0-SNAPSHOT.jar

```

> **Screenshot:**
> 
> <img width="921" height="88" alt="Run App" src="https://github.com/user-attachments/assets/1e771acd-6d13-4821-a320-9ed5b094c119" />

---

```

```
