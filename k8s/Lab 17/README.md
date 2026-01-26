# Lab 17: Pod Resource Management (Requests & Limits) ⚖️

## Objective

The goal of this lab is to manage cluster resources efficiently by defining the minimum guaranteed resources (**Requests**) and the maximum allowed usage (**Limits**) for the application pods.

## Tasks Performed

* **Deployment Update:** Modified the existing `nodejs-app` deployment to include resource specifications for the containers.
* **Resource Configuration:** * Set **CPU Request** to `1` (1 vCPU) and **Memory Request** to `1Gi`.
* Set **CPU Limit** to `2` (2 vCPUs) and **Memory Limit** to `2Gi`.


* **Deployment Execution:** Successfully applied the updated YAML configuration using `kubectl apply`.
* **Validation:** Verified the resource allocation using `kubectl describe` and monitored real-time usage with `kubectl top`.

---

## Technical Specifications

| Resource Type | Request (Guaranteed) | Limit (Maximum) |
| --- | --- | --- |
| **CPU** | 1 vCPU | 2 vCPUs |
| **Memory** | 1 GiB | 2 GiB |

---

## Verification & Screenshots

### 1. Resource Configuration 
>
> <img width="666" height="206" alt="RESOURCES" src="https://github.com/user-attachments/assets/dac42fe9-df8a-4d1a-af7b-008e1949ea85" />
