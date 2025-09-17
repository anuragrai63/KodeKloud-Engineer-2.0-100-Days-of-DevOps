# Day 51: Execute Rolling Updates in Kubernetes.

## Scenario

An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment.

They've crafted an image `nginx:1.17` with the latest updates

- Execute a rolling update for this application, integrating the `nginx:1.17` image. The deployment is named nginx-deployment.
- Ensure all pods are operational post-update.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Execute a rolling update for the `nginx-deployment` using the updated image `nginx:1.17`.

---

## Solution

### 1. Update the Deployment Image

```bash
kubectl get deployments nginx-deployment -o wide
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.17

```
---

### 2. Monitor the Rollout

```bash
kubectl rollout status deployment/nginx-deployment

```

---

### 3. Check deployment history and pod

```bash
kubectl rollout history deployment  nginx-deploymentdeployment.apps/nginx-deployment 
kubectl get pods 
```

---

## Result

- The `nginx-deployment` deployment is successfully rolled out  with the `nginx:1.17` image.
