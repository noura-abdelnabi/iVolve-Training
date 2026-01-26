## Lab 13: Persistent Storage Setup for Application Logging

**Objective:** Create a permanent storage solution on the host node to ensure log data persists even if the pod is deleted or restarted.

### 1. Manual Node Preparation

Since we are using `hostPath`, the directory must exist on the Kubernetes node with the correct permissions.

* **Steps taken:**
* Accessed the minikube node: `minikube ssh`
* Created the directory: `sudo mkdir -p /mnt/app-logs`
* Set permissions: `sudo chmod 777 /mnt/app-logs`


## Screenshot
>
> **<img width="624" height="110" alt="SSH MINIKUBE" src="https://github.com/user-attachments/assets/236b03ae-19a8-45f5-90ca-265348dd634c" />**

---

### 2. Persistent Volume (PV) Configuration

Defined a cluster-wide storage resource with 1Gi capacity and `ReadWriteMany` access mode.

**`pv.yaml`:**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: log-pv
spec:
  capacity:
    storage: 1Gi 
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany 
  persistentVolumeReclaimPolicy: Retain 
  storageClassName: manual
  hostPath:
    path: "/mnt/app-logs" 

```

---

### 3. Persistent Volume Claim (PVC)

Requested the storage resource to be used by the MySQL StatefulSet in Lab 14.

**`pvc.yaml`:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: log-pvc
  namespace: ivolve
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany 
  resources:
    requests:
      storage: 1Gi 

```
## Screenshot
>
> **<img width="467" height="580" alt="STORAGE YAML" src="https://github.com/user-attachments/assets/7a0523ef-046a-4648-82ae-c150a945330a" />**

---

### 4. Verification of Storage Binding

Checked the status to ensure the PV and PVC are successfully bound to each other.

```bash
kubectl get pv
kubectl get pvc 

```
## Screenshot
>
> **<img width="1032" height="245" alt="VERIFY" src="https://github.com/user-attachments/assets/5de475f2-adab-4dc7-95f2-3d804d1fd1be" />**
