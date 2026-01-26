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
  namespace: ivolve
spec:
  ports:
  - port: 3306
  clusterIP: None 
  selector:
    app: mysql

```
## Screenshot
>
> <img width="379" height="258" alt="new servcie" src="https://github.com/user-attachments/assets/12bdaca2-edc0-40d5-91d5-9f2521b3d245" />


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
  namespace: ivolve
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
> <img width="294" height="627" alt="new state" src="https://github.com/user-attachments/assets/adb02a64-79aa-4fc9-9965-d713f486ecdd" />


---

### 3. Database Operational Verification

Confirmed that the database is operational by connecting through a MySQL client inside the Pod.

**Commands:**

```bash
# Verify the pod is running and scheduled on the correct node
kubectl get pods -n ivolve
kubectl get statfulset -n ivolve
kubectl get service mysql-headless -n ivolve
```
## Screenshot
>
> <img width="884" height="203" alt="verify new" src="https://github.com/user-attachments/assets/b3e62e84-04a4-499d-9bb2-c2960b04c19b" />

---

```bash
# Connect to MySQL
kubectl exec -it mysql-0 -n ivolve -- mysql -u root -prootpassword

```
## Screenshot
>
> <img width="874" height="344" alt="new exec" src="https://github.com/user-attachments/assets/53f48b51-dd1e-49f0-b0d1-81387818b851" />
