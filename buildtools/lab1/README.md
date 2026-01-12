# Building and Packaging Java Application with Gradle

This project demonstrates the process of building, testing, and packaging a Java application using **Gradle** as the build automation tool.

## 🛠 Prerequisites
* Java JDK installed.
* Gradle installed.

> **Screenshot:** <img width="822" height="699" alt="install gradle" src="https://github.com/user-attachments/assets/08072e9c-8c3d-4137-a604-7f8f19357fd3" />

## 🚀 Steps Performed

### 1. Clone the Repository
First, I cloned the source code from the remote repository:
```bash
git clone [https://github.com/Ibrahim-Adel15/build1.git](https://github.com/Ibrahim-Adel15/build1.git)

```
> **Screenshot:** <img width="823" height="269" alt="clone lab1-repo" src="https://github.com/user-attachments/assets/f254cdfd-94f2-422a-8451-3d0767b5fcbb" />

> 
### 2. Run Unit Tests

To ensure the code quality and that all features work as expected:

```bash
gradle test

```

> **Screenshot:** <img width="1226" height="214" alt="Run Unit Test" src="https://github.com/user-attachments/assets/560aa449-7e86-4171-9831-20d7e50dab26" />


### 3. Build and Package the Application

I generated the executable JAR file (artifact) using the build command:

```bash
gradle build

```

The artifact was successfully generated at:

`build/libs/ivolve-app.jar`

> **Screenshot:** <img width="1226" height="687" alt="build to generate ivolve-app jar" src="https://github.com/user-attachments/assets/62ce14a9-fe6d-4b94-8037-d7e5f3a03d44" />


### 4. Run and Verify the Application

Finally, I ran the application to verify it is working correctly:

```bash
java -jar build/libs/ivolve-app.jar

```

> **Screenshot:** <img width="823" height="96" alt="Run App" src="https://github.com/user-attachments/assets/5adc9e94-ac96-4d51-b713-43269bc0f75d" />

---

```

```
