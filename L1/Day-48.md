# Day 48: Deploy Pods in Kubernetes Cluster

## Scenario

The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a pod according to the details below:

- Create a pod named `pod-httpd` using the `httpd image` with the latest tag. Ensure to specify the tag as **httpd:latest**.
- Set the app label to `httpd_app`, and name the container as `httpd-container`.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create a pod called `pod-httpd` using the `httpd:latest` image, with the specified label `app` and container name `httpd-container`.

---

## Solution

### 1. Create a manifest file named pod-httpd.yaml with the following content:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest

```

### 2. Apply it using

```bash
kubectl apply -f pod-httpd.yaml
```

---

### 3. Verify pod

```bash
kubectl get pods -l app=httpd_app
kubectl describe pod pod-httpd

```

---

## Result

- The `pod-httpd` pod is successfully created with the httpd:latest image, container name `httpd-container`, and label `httpd_app`. 
