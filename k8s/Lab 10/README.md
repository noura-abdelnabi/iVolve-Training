## Lab 10: Node Isolation Using Taints in Kubernetes

**Objective:** Prevent pods from being scheduled on a specific node unless they have a matching toleration.

### Steps:

1. Created a Kubernetes cluster with 2 nodes.
   
### Screenshots:
>
> <img width="645" height="91" alt="nodes" src="https://github.com/user-attachments/assets/8a77fa1b-eb67-4081-a5fc-4ab135900310" />

2. Applied a taint to the worker node:
```bash
kubectl taint nodes minikube-m02 node=worker:NoSchedule

```
### Screenshots:
>
> <img width="969" height="42" alt="tainted minikubem02" src="https://github.com/user-attachments/assets/dc3c5967-3981-433b-91cc-0600e811a5d8" />


3. Verified the taint application:
```bash
kubectl describe nodeminikube-m02

```

### Screenshots:
>
> <img width="974" height="89" alt="verification" src="https://github.com/user-attachments/assets/292f5fc4-4ac9-4618-8ece-1d14d3ab19d3" />
غل الملفات؟**
