# Day 52: Revert Deployment to Previous Version in Kubernetes

## Scenario

Earlier today, the Nautilus DevOps team deployed a new release for an application. However, a customer has reported a bug related to this recent release. Consequently, the team aims to revert to the previous version.
They've crafted an image `nginx:1.17` with the latest updates

- There exists a deployment named `nginx-deployment`; initiate a rollback to the previous revision.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Roll back the `nginx-deployment` to its previous revision.

---

## Solution

### 1. Roll back deployment

```bash
kubectl get deployments nginx-deployment -o wide
kubectl rollout undo deployment/nginx-deployment

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

- The `nginx-deployment` deployment is successfully rolled out to it's previous version.
