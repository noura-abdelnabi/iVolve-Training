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
> <img width="380" height="217" alt="config yaml" src="https://github.com/user-attachments/assets/0d81e752-f361-49cf-91ef-3cbd28c4997a" />

To verify the creation and content of Configmap:

```bash
# Verify ConfigMap
kubectl get configmap mysql-config
kubectl describe configmap mysql-config
```

## Screenshot
>
> <img width="1028" height="115" alt="apply verify" src="https://github.com/user-attachments/assets/8a3b1c1b-2a2d-41ba-bab4-8302763181df" />
>
> <img width="1032" height="467" alt="describe cm" src="https://github.com/user-attachments/assets/4402ecad-66cd-45ec-8e5c-b12fea7395ab" />

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
> <img width="475" height="254" alt="secret yamlfile" src="https://github.com/user-attachments/assets/0e7adbd2-1d7f-4c85-8e14-f39ffa7329de" />

---

To verify the creation and content of Secret:

```bash
# Verify Secret
kubectl get secret mysql-secret
kubectl describe secret mysql-secret
```

## Screenshot
>
> <img width="872" height="114" alt="apply verify sc" src="https://github.com/user-attachments/assets/4433b305-db32-4387-b27c-e479251f3450" />
>
> <img width="844" height="267" alt="describe sc" src="https://github.com/user-attachments/assets/222db25e-25c1-46f5-928a-984163c99567" />
