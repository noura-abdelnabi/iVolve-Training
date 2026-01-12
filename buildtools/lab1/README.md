# Building and Packaging Java Application with Gradle

This project demonstrates the process of building, testing, and packaging a Java application using **Gradle** as the build automation tool.

## 🛠 Prerequisites
* Java JDK installed.
* Gradle installed.

> **Screenshot:**
> *(C:\Users\Admin\Desktop\Career\NTI\iVolve\LAB1\install gradle.PNG)*

## 🚀 Steps Performed

### 1. Clone the Repository
First, I cloned the source code from the remote repository:
```bash
git clone [https://github.com/Ibrahim-Adel15/build1.git](https://github.com/Ibrahim-Adel15/build1.git)

```
> **Screenshot:**
> *(C:\Users\Admin\Desktop\Career\NTI\iVolve\LAB1\clone lab1-repo.PNG)*
> 
### 2. Run Unit Tests

To ensure the code quality and that all features work as expected:

```bash
gradle test

```

> **Screenshot:**
> *(C:\Users\Admin\Desktop\Career\NTI\iVolve\LAB1\Run Unit Test.PNG)*

### 3. Build and Package the Application

I generated the executable JAR file (artifact) using the build command:

```bash
gradle build

```

The artifact was successfully generated at:

`build/libs/ivolve-app.jar`

> **Screenshot:**
> *(C:\Users\Admin\Desktop\Career\NTI\iVolve\LAB1\build to generate ivolve-app.jar.PNG)*

### 4. Run and Verify the Application

Finally, I ran the application to verify it is working correctly:

```bash
java -jar build/libs/ivolve-app.jar

```

> **Screenshot:**
> *(C:\Users\Admin\Desktop\Career\NTI\iVolve\LAB1\Run App.PNG)*
---

```

```
