# Lab 15: Node.js Application Deployment 🚀

## Objective

Deploy a custom Node.js application with high availability and proper resource scheduling using Kubernetes.

## Tasks Performed

* **Custom Docker Image:** Built and pushed a Node.js application image to Docker Hub.
* **Deployment Configuration:** Created a deployment named `nodejs-app` with **2 replicas**.
* **Environment Management:** Injected sensitive database credentials and configurations using `ConfigMaps` and `Secrets`.
* **Storage Persistence:** Mounted a Static Persistent Volume (PV) to `/usr/src/app/logs` for application logs.
* **Advanced Scheduling:** Added a **Toleration** to the pod spec (`node=worker:NoSchedule`) to allow pods to run on the tainted worker node.
* **Service Discovery:** Exposed the application using a `ClusterIP` service named `nodejs-service` to load balance traffic.

## Infrastructure Components

| Component | Name | Type |
| --- | --- | --- |
| Deployment | `nodejs-app` | Apps/v1 |
| Service | `nodejs-service` | ClusterIP |
| Replicas | 2 | Desired State |

## Screenshot
>
> <img width="625" height="649" alt="DEPLOY YAML" src="https://github.com/user-attachments/assets/64305b0b-61d7-4ba5-a6f9-c2ab051f1fe3" />
>
> <img width="280" height="217" alt="SERVICE YAML" src="https://github.com/user-attachments/assets/b3714b4a-18b4-45b1-bec3-3e18bb78f0b4" />

---

## Final Verification (Screenshots)

### 1. Deployment & Service Status

> <img width="808" height="254" alt="VERIFY" src="https://github.com/user-attachments/assets/4cc264cc-2a70-4f38-b4a4-cd4c844e6fab" />


### 2. Node Scheduling (Toleration Proof)

Both pods are running successfully, proving that the `toleration` is correctly matching the node `taint`.

> <img width="1050" height="77" alt="PODS" src="https://github.com/user-attachments/assets/907ee60a-7acc-48a9-b04e-101f1123021e" />*
