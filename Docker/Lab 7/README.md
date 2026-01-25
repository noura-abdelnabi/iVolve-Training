## 🔹 Lab 7: Docker Volume and Bind Mount with Nginx

### 🎯 Objective

* Persist Nginx logs using Docker volumes
* Serve custom HTML using bind mounts

---

### 🛠️ Steps

#### 1️⃣ Create Docker Volume

```bash
docker volume create nginx_logs
```

> 📸 Screenshot:
>
> <img width="712" height="200" alt="creating docker volume" src="https://github.com/user-attachments/assets/9e2161e7-4eb2-40fb-9489-05c9633b0b68" />

---

#### 2️⃣ Create Bind Mount Directory

```bash
mkdir -p ~/nginx-bind/html
echo "Hello from Bind Mount" > index.html
```

> 📸 Screenshot:
>
> <img width="992" height="91" alt="create bind mount   index html" src="https://github.com/user-attachments/assets/6504ca36-5251-4abb-ad8d-02be420802a8" />

---


#### 3️⃣ Run Nginx Container

```bash
docker run -d \
-p 8086:80 \
--name container-nginx \
-v nginx_logs:/var/log/nginx \
-v ~/nginx-bind/html:/usr/share/nginx/html \
nginx
```

> 📸 Screenshot:
>
> <img width="1181" height="68" alt="run the container with volume and bind mount   test" src="https://github.com/user-attachments/assets/a75bb46c-e2cf-4a4f-8a75-102bfd6d22b6" />

---

#### 4️⃣ Verify Nginx Page

```bash
curl localhost:8086
```

> 📸 Screenshot:
>
> <img width="1191" height="200" alt="test the contaier" src="https://github.com/user-attachments/assets/fd6b2d2d-ab88-447c-9468-aeaf6e87d187" />
>
> <img width="887" height="258" alt="verify from inside the container" src="https://github.com/user-attachments/assets/a26c7b91-3af5-451d-babe-b2aaf0b9d070" />


---

#### 5️⃣ Modify HTML File and Re-Verify

Update `index.html` and refresh browser.

> 📸 Screenshot:
>
> <img width="818" height="179" alt="changing index html" src="https://github.com/user-attachments/assets/f7ad4f41-854f-4aed-af27-48ea58117f86" />

---

#### 6️⃣ Verify Logs Stored in Volume

```bash
docker volume inspect nginx_logs
sudo ls /var/lib/docker/volumes/nginx_logs/_data
```

> 📸 Screenshot:
>
> <img width="932" height="68" alt="verify logs store" src="https://github.com/user-attachments/assets/fc05b39f-e6d0-41f5-9360-23cd47dd6ef3" />

---

#### 7️⃣ Cleanup

```bash
docker stop container-nginx
docker rm container-nginx
docker volume rm nginx_logs
```

> 📸 Screenshot:
>
> <img width="1060" height="199" alt="removing the volume" src="https://github.com/user-attachments/assets/3358d030-757d-4ad1-900f-3f740b29cc2d" />

