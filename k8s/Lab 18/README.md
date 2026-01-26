# Lab 18: Controlling Pod-to-Pod Traffic via Network Policy 🛡️

## Objective

The goal of this lab is to implement a zero-trust security model within the cluster by restricting network traffic to the MySQL database, allowing access only from authorized application pods.

## Tasks Performed

* **Network Policy Creation:** Designed a policy named `allow-app-to-mysql` to manage Ingress traffic.
* **Target Selection:** Used `podSelector` to apply the policy specifically to pods labeled with `app: mysql`.
* **Ingress Rule Configuration:** * Allowed traffic strictly from pods with the label `app: nodejs`.
* Restricted access to the standard MySQL port **3306**.

## Screenshot
>
> <img width="454" height="387" alt="YAML" src="https://github.com/user-attachments/assets/633541fc-3372-4194-8b45-ae845a4c81b5" />


---

## Technical Specifications

| Feature | Configuration |
| --- | --- |
| **Policy Name** | `allow-app-to-mysql` |
| **Policy Type** | `Ingress` (Inbound Traffic) |
| **Source Selector** | `app: nodejs` |
| **Destination Port** | TCP 3306 |

---

## Verification & Screenshots

### 1. Network Policy Deployment

The policy was successfully applied to the cluster, ensuring that only authorized traffic can reach the database layer.

>
> <img width="767" height="69" alt="NETPOL" src="https://github.com/user-attachments/assets/524e7103-6d6f-448c-8810-41fe6f0de0a7" />

### 2. Policy Details

Using `kubectl describe networkpolicy allow-app-to-mysql -n ivolve`, we can verify the ingress rules and selectors.

> <img width="1005" height="310" alt="des" src="https://github.com/user-attachments/assets/e7fcc79d-3216-4553-b117-86527437053c" />
