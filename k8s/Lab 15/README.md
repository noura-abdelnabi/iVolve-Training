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
> Deployment Yaml File
> 
> <img width="767" height="691" alt="new deploy" src="https://github.com/user-attachments/assets/c0f0f221-715f-4584-9635-5ae1013a406e" />
>
> Service Yaml File
> 
> <img width="408" height="256" alt="new service" src="https://github.com/user-attachments/assets/5d2078be-c19e-404d-9158-b43fb5bdc7b2" />

---

## Final Verification (Screenshots)

### 1. Deployment & Service Status

> <img width="919" height="377" alt="new verify" src="https://github.com/user-attachments/assets/ffc3d3e8-c425-4cee-a0fb-fee29f169ae2" />
 

### 2. Node Scheduling (Toleration Proof)

Both pods are running successfully, proving that the `toleration` is correctly matching the node `taint`.

> <img width="1193" height="118" alt="newpods" src="https://github.com/user-attachments/assets/a51c031b-b14f-4f8f-830a-6fd2cddba871" />
