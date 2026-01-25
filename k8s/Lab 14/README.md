## Lab 14: StatefulSet with Headless Service

**Objective:** Deploy a stateful MySQL application that maintains its identity and persists data using the resources created in previous labs.

### 1. Headless Service Definition

Created a Headless Service (`clusterIP: None`) to provide stable network identifiers for the MySQL Pods.

**`mysql-service.yaml`:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-headless
spec:
  ports:
  - port: 3306
  clusterIP: None 
  selector:
    app: mysql

```
## Screenshot
>
> <img width="364" height="251" alt="YAML OF SERVICE" src="https://github.com/user-attachments/assets/b512232c-a3d4-4c13-a30b-3a18b0851de0" />

---

### 2. MySQL StatefulSet Configuration

The StatefulSet was configured with the following key requirements:

* **Replicas:** 1.
* **Secrets:** Consumed `mysql-credentials` for the `MYSQL_ROOT_PASSWORD` environment variable.
* **Tolerations:** Added to allow scheduling on the node with the `node=worker:NoSchedule` taint.
* **Volume Mounts:** Mounted the `log-pvc` to `/var/lib/mysql` for data persistence.

**`mysql-statefulset.yaml`:**

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: "mysql-headless"
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-credentials
              key: MYSQL_ROOT_PASSWORD
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-storage
        persistentVolumeClaim:
          claimName: log-pvc

```
## Screenshot
>
> <img width="379" height="598" alt="STATEFUL YAML" src="https://github.com/user-attachments/assets/3258a59e-8d85-4a91-8661-18483faff7c2" />

---

### 3. Database Operational Verification

Confirmed that the database is operational by connecting through a MySQL client inside the Pod.

**Commands:**

```bash
# Verify the pod is running and scheduled on the correct node
kubectl get pods
kubectl get statfulset
kubectl get service mysql-headless
kubectl describe pod mysql-0
```
## Screenshot
>
> <img width="924" height="203" alt="VERIFY" src="https://github.com/user-attachments/assets/ae3f794d-9d63-4006-9471-1dbbe2bd1406" />
>
> <img width="940" height="597" alt="DESCRIBE POD" src="https://github.com/user-attachments/assets/0a3e08db-e8ae-4353-8737-4255c224e744" />
> <img width="938" height="564" alt="DESCRIBE POD2" src="https://github.com/user-attachments/assets/b13d88c3-f6b5-478b-8988-9179ec958da7" />

---

```bash
# Connect to MySQL
kubectl exec -it mysql-0 -- mysql -u root -prootpassword

```
## Screenshot
>
> <img width="734" height="272" alt="EXEC" src="https://github.com/user-attachments/assets/a56a3890-2ee3-4c92-9f14-ee5a37ecf2eb" />
