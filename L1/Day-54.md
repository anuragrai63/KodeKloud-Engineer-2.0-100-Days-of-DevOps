# Day 54: Kubernetes Shared Volumes

## Scenario

We are working on an application that will be deployed on multiple containers within a pod on Kubernetes cluster. There is a requirement to share a volume among the containers to save some temporary data. The Nautilus DevOps team is developing a similar template to replicate the scenario. Below you can find more details about it.

- Create a pod named `volume-share-devops`.
- For the first container, use image debian with latest tag only and remember to mention the tag i.e `debian:latest`, container should be named as `volume-container-devops-1`, and run a `sleep` command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/official`.
- For the second container, use image debian with the latest tag only and remember to mention the tag i.e `debian:latest`, container should be named as `volume-container-devops-2`, and again run a `sleep` command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/cluster`.
- Volume name should be `volume-share` of type `emptyDir`.
- After creating the pod, `exec` into the first container i.e `volume-container-devops-1`, and just for testing create a file `official.txt` with any content under the mounted path of first container i.e `/tmp/official`.
- The file `official.txt` should be present under the mounted path `/tmp/cluster` on the second container `volume-container-devops-2` as well, since they are using a shared volume.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create Pod with `shared volume` between two containers.

---

## Solution

### 1. Create the Pod Manifest (volume-share-devops.yaml)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-devops
spec:
  volumes:
  - name: volume-share
    emptyDir: {}

  containers:
  - name: volume-container-devops-1
    image: debian:latest
    command: ["sleep", "3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/official

  - name: volume-container-devops-2
    image: debian:latest
    command: ["sleep", "3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/cluster

```
---

### 2. Apply the Pod

```bash
kubectl apply -f volume-share-devops.yaml
```

---

### 3. Create the Shared File inside first container:

```bash
kubectl exec -it volume-share-devops -c volume-container-devops-1 -- /bin/bash
echo "Shared volume test" > /tmp/official/official.txt
exit

```
---

### 4. Verify from Second Container:

```bash
kubectl exec -it volume-share-devops -c volume-container-devops-2 -- /bin/bash
cat /tmp/cluster/official.txt

```

## Result

- The pod created with `shared-volume` successfully.
