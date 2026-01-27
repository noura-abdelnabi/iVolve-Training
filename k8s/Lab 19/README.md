# Lab 19: Node-Wide Pod Management with DaemonSet

## Description

This lab demonstrates how to deploy a pod on every node within a Kubernetes cluster using a **DaemonSet**. The primary focus is deploying the `prometheus-node-exporter` to gather hardware and OS metrics from all nodes, including those with taints.

## Tasks

* **Namespace Creation**: Create a dedicated `monitoring` namespace for isolation.
* **DaemonSet Deployment**: Deploy the Prometheus `node-exporter`.
* **Taint Tolerance**: Configure the DaemonSet to tolerate all existing node taints to ensure full cluster coverage.
* **Validation**: Verify that exactly one pod is scheduled on each available node.
* **Metrics Confirmation**: Access the metrics endpoint via `:9100/metrics` on any node IP.

## Prerequisites

* A running Kubernetes cluster.
* `kubectl` CLI tool configured.

## Configuration File (`node-exporter.yaml`)

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
  namespace: monitoring
spec:
  selector:
    matchLabels:
      name: node-exporter
  template:
    metadata:
      labels:
        name: node-exporter
    spec:
      tolerations:
      - operator: Exists
      hostNetwork: true
      containers:
      - name: node-exporter
        image: prom/node-exporter:latest
        ports:
        - containerPort: 9100
          hostPort: 9100
          name: metrics

```
## Screenshot
>
> <img width="441" height="504" alt="YAML" src="https://github.com/user-attachments/assets/1acdcc6d-55d4-4815-bf8a-df1f3df0fa47" />

## How to Run

1. **Create the namespace**:
```bash
kubectl create namespace monitoring

```
## Screenshot
>
> <img width="756" height="49" alt="NAMEPACE" src="https://github.com/user-attachments/assets/a5530ef8-3622-4d28-95c9-7c6eec0fcc1b" />


2. **Apply the DaemonSet**:
```bash
kubectl apply -f node-exporter.yaml

```


3. **Check the status**:
```bash
kubectl get pods -n monitoring -o wide

```


To confirm the metrics are being exposed correctly, run:

```bash
curl http://<NODE_IP>:9100/metrics

```
## Screenshot
>
> <img width="1147" height="547" alt="VERIFY" src="https://github.com/user-attachments/assets/85dc337e-eb0c-48e8-a57d-90d921031d2c" />
