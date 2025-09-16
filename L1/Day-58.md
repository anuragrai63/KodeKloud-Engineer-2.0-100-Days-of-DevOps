# Day 58: Deploy Grafana on Kubernetes Cluster

## Scenario

The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.
- Create a deployment named `grafana-deployment-devops` using any grafana image for Grafana app. Set other parameters as per your choice.
- Create `NodePort` type service with nodePort `32000` to expose the app.

`You need not to make any configuration changes inside the Grafana app once deployed, just make sure you are able to access the Grafana login page.`

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create `grafana deployment`.
- Make it accessible via `NodePort` service.

---

## Solution

### 1. Create the Deployment Manifest (grafana-deployment.yaml)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - name: grafana-container
        image: grafana/grafana:latest
        ports:
        - containerPort: 3000


```
---

### 2. Apply the deployment

```bash
kubectl apply -f grafana-deployment.yaml

```
---

### 3. Create the NodePort Service (grafana-service.yaml)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
  - port: 3000
    targetPort: 3000
    nodePort: 32000


```
---

### 4. Apply the service

```bash
kubectl apply -f grafana-service.yaml

```
---

### 4. Verify and Access Grafana

```bash
kubectl get pods -l app=grafana
kubectl get svc grafana-service
http://<node-ip>:32000

```
---

> **Note:** Click on `Grafana` to access Grafana login page.

## Result

- The `Grafana` deployed and accessible. 
