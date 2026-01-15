
## 📌 Lab 9: Node.js and MySQL Stack Using Docker Compose

### 🎯 Objective

* Deploy Node.js application with MySQL
* Use Docker Compose
* Configure environment variables
* Use volumes for persistent database storage

---

### 📥 Clone the Repository

```bash
git clone https://github.com/Ibrahim-Adel15/kubernets-app.git
cd kubernets-app
```

📸 **Screenshot**

> Clone Node.js app repo
> 
> <img width="986" height="203" alt="clone lab9-repo" src="https://github.com/user-attachments/assets/a2ba3b52-153d-4a7f-be32-d025a3ab0961" />

---

### 🧾 docker-compose.yml

```yaml
version: "3.8"

services:
  app:
    build: .
    ports:
      - "3001:3000"
    environment:
      DB_HOST: db
      DB_USER: root
      DB_PASSWORD: root
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ivolve
    volumes:
      - db_mysql:/var/lib/mysql

volumes:
  db_mysql:
```

📸 **Screenshot:**

> Docker Compose file
>
> <img width="457" height="566" alt="docker compose" src="https://github.com/user-attachments/assets/ee142660-630e-4d41-b33c-d2c44f3668c0" />


---

### ▶️ Run the Application

```bash
docker-compose up -d
```

📸 **Screenshot Placeholder:**

> Docker Compose running
>
> <img width="1193" height="335" alt="dockercompse up" src="https://github.com/user-attachments/assets/05f86b2d-6a4c-435f-bbb1-5c13f198b7ce" />

---

### ✅ Verification

* App URL:

  ```
  curl localhost:3001
  ```

* Health Check:

  ```
  curl localhost:3001/health
  ```

* Ready Check:

  ```
  curl localhost:3001/ready
  ```

📸 **Screenshot**

> App running successfully
>
> <img width="1042" height="661" alt="verify" src="https://github.com/user-attachments/assets/7d0030d4-6a00-4123-870d-8943deca6378" />
>
> <img width="1049" height="121" alt="verify health   ready" src="https://github.com/user-attachments/assets/b853d315-3833-49c0-bf31-288ca7a1a1be" />

---

### 📜 Logs Verification

```bash
docker logs web-app
```

📸 **Screenshot:**

> Application logs
> 
> <img width="786" height="430" alt="web-app logs" src="https://github.com/user-attachments/assets/08f82057-9d46-4dce-a705-2dbd8aa154ad" />

---

### 📦 Push Image to DockerHub

```bash
docker login
docker tag kubernets-app-app:latest nouraabdelnabi/web-app
docker push nouraabdelnabi/web-app
```

📸 **Screenshot Placeholder:**

> DockerHub push
> 
> <img width="1128" height="597" alt="pushing into my dockerhub" src="https://github.com/user-attachments/assets/41b8f744-0de7-40fe-9675-bb3e6b9fdd32" />
>
> <img width="1573" height="292" alt="dockerhub" src="https://github.com/user-attachments/assets/85eb50fb-9050-4806-b42e-3c3cb00e680a" />

---
