## Lab 12: Managing Configuration and Sensitive Data with ConfigMaps and Secrets

**Objective:** Decouple environment-specific configuration and sensitive credentials from the application code.

### 1. Configuration Management (ConfigMap)

Used to store non-sensitive MySQL configuration variables: `DB_HOST` and `DB_USER`.

**`mysql-configmap.yaml`:**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: ivolve
data:
  DB_HOST: "mysql-headless"
  DB_USER: "ivolve-user"

```

## Screenshot
>
> <img width="519" height="177" alt="new cm" src="https://github.com/user-attachments/assets/b69b8b66-9345-4bf4-9ee3-50aa211d9738" />


To verify the creation and content of Configmap:

```bash
# Verify ConfigMap
kubectl get configmap mysql-config -n ivolve
kubectl describe configmap mysql-config -n ivolve
```

## Screenshot
>
> <img width="870" height="554" alt="new cm desc" src="https://github.com/user-attachments/assets/fc5ff350-3563-4ad2-a4ff-4b464931ccd2" />

---


### 2. Sensitive Data Management (Secret)

Used to store sensitive MySQL credentials securely (`DB_PASSWORD` and `MYSQL_ROOT_PASSWORD`) using **base64** encoding.

**`mysql-secret.yaml`:**

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: ivolve
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQxMjM=
  MYSQL_ROOT_PASSWORD: cm9vdHBhc3N3b3Jk

```

## Screenshot
>
> <img width="875" height="91" alt="base 64 " src="https://github.com/user-attachments/assets/ab5aab5e-c77f-495e-acbb-04dd3d2afa43" />
>
> <img width="525" height="200" alt="new sc" src="https://github.com/user-attachments/assets/8a24241e-aa25-4007-9883-6ae2676b7043" />

---

To verify the creation and content of Secret:

```bash
# Verify Secret
kubectl get secret mysql-secret -n ivolve
kubectl describe secret mysql-secret -n ivolve
```

## Screenshot
>
> <img width="809" height="336" alt="new sc desc" src="https://github.com/user-attachments/assets/f8d0de6b-acaa-47f0-b269-2b92de1ed0d5" />


