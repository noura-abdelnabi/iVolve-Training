# Lab 20: Securing Kubernetes with RBAC and Service Accounts

## Description

This lab focuses on implementing **Role-Based Access Control (RBAC)** to secure a Kubernetes cluster. The goal is to create a restricted environment for a Jenkins Service Account, allowing it only to read (get/list) Pods within a specific namespace.

## Tasks

* **Service Account**: Create a `jenkins-sa` Service Account in the `ivolve` namespace.
* **Secret Management**: Manually create a secret to generate and retrieve a long-lived token for the Service Account.
* **Role Definition**: Define a Role named `pod-reader` that grants `get` and `list` permissions on Pods.
* **Access Binding**: Link the Role to the Service Account using a `RoleBinding`.
* **Validation**: Confirm the Service Account can list pods but cannot perform unauthorized actions (like deleting or creating pods).

## Configuration Files

### 1. Secret (`secret-jenkins.yaml`)

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: jenkins-sa-token
  namespace: ivolve
  annotations:
    kubernetes.io/service-account.name: jenkins-sa
type: kubernetes.io/service-account-token

```
## Screenshot
>
> <img width="522" height="203" alt="SECRET YAML" src="https://github.com/user-attachments/assets/eab4730f-d111-42f7-adb1-0777518895dd" />

---

### 2. RBAC Policies (`rbac-setup.yaml`)

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: ivolve
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: ivolve
subjects:
- kind: ServiceAccount
  name: jenkins-sa
  namespace: ivolve
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io

```
## Screenshot
>
> <img width="566" height="464" alt="RBAC" src="https://github.com/user-attachments/assets/6ff4b2de-d574-43d1-8445-6cab233e1a9b" />

---

## Step-by-Step Execution

1. **Create the namespace & service account**:
```bash
kubectl create namespace ivolve
kubectl create serviceaccount jenkins-sa -n ivolve

```

## Screenshot
>
> <img width="921" height="179" alt="ns + sa" src="https://github.com/user-attachments/assets/795a5c78-3653-4702-b090-d275ad3d5ff0" />


2. **Apply the Configurations**:
```bash
kubectl apply -f secret-jenkins.yaml
kubectl apply -f rbac-setup.yaml

```

3. **Retrieve the Token**:
```bash
kubectl get secret jenkins-sa-token -n ivolve -o jsonpath={.data.token} | base64 -d

```

## Screenshot
>
> <img width="1142" height="269" alt="SEC" src="https://github.com/user-attachments/assets/43d96955-7e94-4994-bfad-c62c7859408b" />

## Verification

Test the permissions using the `auth can-i` command:

* **Should return `yes**`:
```bash
kubectl auth can-i list pods --as=system:serviceaccount:ivolve:jenkins-sa -n ivolve

```

* **Should return `no**`:
```bash
kubectl auth can-i delete pods --as=system:serviceaccount:ivolve:jenkins-sa -n ivolve

```
## Screenshot
>
> <img width="1178" height="136" alt="AUTH" src="https://github.com/user-attachments/assets/1a8c9880-4dd8-4a2b-9e3a-4cbdeacb1322" />

