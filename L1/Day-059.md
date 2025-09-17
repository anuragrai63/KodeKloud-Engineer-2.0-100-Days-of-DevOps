# Day 59: Troubleshoot Deployment issues in Kubernetes

## Scenario

Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far. This morning one of the team members was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.

- The deployment name is `redis-deploymen`t. The pods are not in running state right now, so please look into the issue and fix the same.

  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Troubleshoot the deployment `redis-deployment`.


---

## Solution

### 1. Describe the pod to see events 

```bash
kubectl describe pod redis-deployment-6fd9d5fcb-lv84m
```
---

### 2. Check deployment

```bash
kubectl get deployments.apps redis-deployment -o yaml

```
---

> **Issues Identified:** Typo in `ConfigMap` name and incorect `image`.


### 3. Edit the deployment to correct Configmap and image

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "2"
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"creationTimestamp":null,"labels":{"app":"redis"},"name":"redis-deployment","namespace":"default"},"spec":{"replicas":1,"selector":{"matchLabels":{"app":"redis"}},"strategy":{},"template":{"metadata":{"creationTimestamp":null,"labels":{"app":"redis"}},"spec":{"containers":[{"image":"redis:alpin","name":"redis-container","ports":[{"containerPort":6379}],"resources":{"requests":{"cpu":"0.3"}},"volumeMounts":[{"mountPath":"/redis-master-data","name":"data"},{"mountPath":"/redis-master","name":"config"}]}],"volumes":[{"emptyDir":{},"name":"data"},{"configMap":{"name":"redis-cofig"},"name":"config"}]}}}}
  creationTimestamp: "2025-09-17T04:33:52Z"
  generation: 2
  labels:
    app: redis
  name: redis-deployment
  namespace: default
  resourceVersion: "1859"
  uid: c006c15b-3306-4a8e-8a51-47e6f8f3e7d8
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: redis
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: redis
    spec:
      containers:
      - image: redis:alpine     ## Updated
        imagePullPolicy: IfNotPresent
        name: redis-container
        ports:
        - containerPort: 6379
          protocol: TCP
        resources:
          requests:
            cpu: 300m
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /redis-master-data
          name: data
        - mountPath: /redis-master
          name: config
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - emptyDir: {}
        name: data
      - configMap:
          defaultMode: 420
          name: redis-config  ##Updated
        name: config
status:
  availableReplicas: 1
  conditions:
  - lastTransitionTime: "2025-09-17T04:48:52Z"
    lastUpdateTime: "2025-09-17T04:48:52Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
  - lastTransitionTime: "2025-09-17T04:48:47Z"
    lastUpdateTime: "2025-09-17T04:48:52Z"
    message: ReplicaSet "redis-deployment-7c8d4f6ddf" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"
    type: Progressing
  observedGeneration: 2
  readyReplicas: 1
  replicas: 1
  updatedReplicas: 1
```
---

### 4. Check Pod Status

```bash
kubectl get pods

```
---

## Result

- Typo corrected and `pods` are running fine.. 
