## Lab 11: Namespace Management and Resource Quota

**Objective:** Create an isolated environment with restricted resource consumption.

### Steps:

1. Created a namespace named `ivolve`.
   
### Screenshots:
>
> <img width="914" height="49" alt="create namespace" src="https://github.com/user-attachments/assets/90f85f3d-5e6c-446e-9e2e-166bd0ed841a" />

2. Applied a `ResourceQuota` to limit the number of pods to **2** within the namespace.
```yaml
# quota.yaml
apiVersion: v1
kind: ResourceQuota
spec:
  hard:
    pods: "2"

```

### Screenshots:
>
> <img width="358" height="191" alt="quota yaml" src="https://github.com/user-attachments/assets/23cc366b-c39d-4585-ae2f-b046a153f4a9" />

Verification of ResourceQuota and deploying pods
>
> <img width="893" height="112" alt="apply verify" src="https://github.com/user-attachments/assets/2b65ac88-5e2d-4825-baba-cf9988c787b0" />
>
> <img width="1032" height="158" alt="pods verifying" src="https://github.com/user-attachments/assets/517b73cb-e177-472e-ac6d-2fd64c01d553" />



