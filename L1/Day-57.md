# Day 57: Print Environment Variables

## Scenario

The Nautilus DevOps team is working on to setup some pre-requisites for an application that will send the greetings to different users. There is a sample deployment, that needs to be tested. Below is a scenario which needs to be configured on Kubernetes cluster. Please find below more details about it.

- Create a `pod` named `print-envars-greeting`.
- Configure spec as, the container name should be `print-env-container` and use `bash` image.
- Create three environment variables:
  
    - `GREETING` and its value should be `Welcome to`.
    - `COMPANY` and its value should be `xFusionCorp`.
    - `GROUP` and its value should be `Industries`.
      
- Use command `["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']` (please use this exact command), also set its `restartPolicy` policy to `Never` to avoid crash loop back.
- You can check the output using `kubectl logs -f print-envars-greeting` command.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create pod to print environment variable.

---

## Solution

### 1. Create the pod Manifest (print-envars-greeting.yaml)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  restartPolicy: Never
  containers:
  - name: print-env-container
    image: bash:latest
    env:
    - name: GREETING
      value: "Welcome to"
    - name: COMPANY
      value: "xFusionCorp"
    - name: GROUP
      value: "Industries"
    command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']


```
---

### 2. Apply the pod

```bash
kubectl apply -f print-envars-greeting.yaml

```
---

### 3. View the Output

```bash
kubectl logs -f print-envars-greeting

```
---


## Result

- The pod `print-envars-greeting` created and environment variable printed. 
