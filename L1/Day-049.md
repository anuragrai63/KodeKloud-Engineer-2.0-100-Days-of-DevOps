# Day 49: Deploy Applications with Kubernetes Deployments.

## Scenario

The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:

- Create a deployment named nginx to deploy the application nginx using the image nginx:latest (ensure to specify the tag)
- Set the app label to `httpd_app`, and name the container as `httpd-container`.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create a deployment called `nginx` using the `nginx:latest` image.

---

## Solution

### 1. Create a manifest file named nginx-deployment.yaml with the following content:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest


```

### 2. Apply it using

```bash
kubectl apply -f nginx-deployment.yaml
```

---

### 3. Verify the deployment

```bash
kubectl get deployments
kubectl describe deployment nginx
kubectl get pods -l app=nginx


```

---

## Result

- The `nginx` deployment is successfully created with the `nginx:latest` image.
