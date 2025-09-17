# Day 60: Persistent Volumes in Kubernetes

## Scenario

The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster. There are some requirements to create/use persistent volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:

- Create a `PersistentVolume` named as `pv-devops`. Configure the `spec` as storage class should be `manual`, set capacity to `3Gi`, set access mode to `ReadWriteOnce`, volume type should be `hostPath` and set path to `/mnt/dba` (this directory is already created, you might not be able to access it directly, so you need not to worry about it).
- Create a `PersistentVolumeClaim` named as `pvc-devops`. Configure the `spec` as storage class should be `manual`, request `3Gi` of the storage, set access mode to `ReadWriteOnce`.
- Create a `pod` named as `pod-devops`, mount the persistent volume you created with claim name `pvc-devops` at document root of the web server, the container within the pod should be named as `container-devops` using image `nginx` with `latest` tag only (remember to mention the tag i.e `nginx:latest`).
- Create a `node port` type service named `web-devops` using node port `30008` to expose the web server running within the `pod`.

   > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Create `PersistentVolume`.
- Create `PersistentVolumeClaim`.
- Create a `pod`.
- Create `NodePort` to expose.


---

## Solution

### 1.PersistentVolume (pv-devops.yaml) 

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  storageClassName: manual
  capacity:
    storage: 3Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/dba

```
---

### 2. PersistentVolumeClaim (pvc-devops.yaml)

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi

```
---


### 3. pod-devops with Nginx container (pod-devops.yaml)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: devops
spec:
  containers:
  - name: container-devops
    image: nginx:latest
    volumeMounts:
    - name: devops-storage
      mountPath: /usr/share/nginx/html
  volumes:
  - name: devops-storage
    persistentVolumeClaim:
      claimName: pvc-devops

```
---

### 4. NodePort Service (web-devops.yaml)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: devops
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30008

```
---

### 5. Apply above yaml to deploy respective resources.
```bash
kubectl apply -f pv-devops.yaml
kubectl apply -f pvc-devops.yaml
kubectl apply -f pod-devops.yaml
kubectl apply -f web-devops.yaml
```
---


## Result

- `PersistentVolume` created and mounted as `PersistentVolumeClaim` inside `pod`. 
