# Day 53: Resolve VolumeMounts Issue in Kubernetes

## Scenario

We encountered an issue with our `Nginx` and `PHP-FPM` setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:

- The pod name is `nginx-phpfpm` and configmap name is `nginx-config`. Identify and fix the problem.
- Once resolved, `copy /home/thor/index.php` file from the jump host to the `nginx-container` within the nginx document root. After this, you should be able to access the website using Website button on the top bar.


  > **Note:** The `kubectl` utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Task

- Fix volume mount issue and copy `index.php` file from host to container.

---

## Solution

### 1. Inspect the Pod and ConfigMap

```bash
kubectl describe pod nginx-phpfpm
kubectl logs nginx-phpfpm
kubectl describe configmap nginx-config
kubectl get pod nginx-phpfpm -o yaml  > nginx.yaml

```
---

### 2. Fix the MountPath

```bash
vi nginx.yaml
```
Update the MountPath:

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"php-app"},"name":"nginx-phpfpm","namespace":"default"},"spec":{"containers":[{"image":"php:7.2-fpm-alpine","name":"php-fpm-container","volumeMounts":[{"mountPath":"/usr/share/nginx/html","name":"shared-files"}]},{"image":"nginx:latest","name":"nginx-container","volumeMounts":[{"mountPath":"/var/www/html","name":"shared-files"},{"mountPath":"/etc/nginx/nginx.conf","name":"nginx-config-volume","subPath":"nginx.conf"}]}],"volumes":[{"emptyDir":{},"name":"shared-files"},{"configMap":{"name":"nginx-config"},"name":"nginx-config-volume"}]}}
  creationTimestamp: "2025-09-15T17:02:35Z"
  labels:
    app: php-app
  name: nginx-phpfpm
  namespace: default
  resourceVersion: "724"
  uid: c3b83d09-5376-4084-baf5-845b50e34e52
spec:
  containers:
  - image: php:7.2-fpm-alpine
    imagePullPolicy: IfNotPresent
    name: php-fpm-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html     # updated MountPath
      name: shared-files
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-hct8h
      readOnly: true
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-files
    - mountPath: /etc/nginx/nginx.conf
      name: nginx-config-volume
      subPath: nginx.conf
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-hct8h
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kodekloud-control-plane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: shared-files
  - configMap:
      defaultMode: 420
      name: nginx-config
    name: nginx-config-volume
  - name: kube-api-access-hct8h
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2025-09-15T17:02:35Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2025-09-15T17:02:46Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2025-09-15T17:02:46Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2025-09-15T17:02:35Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://6fa59dd1de1797c7d980cbb85920c6ebad5d025e62d2090ffe763ae791ca4abc
    image: docker.io/library/nginx:latest
    imageID: docker.io/library/nginx@sha256:d5f28ef21aabddd098f3dbc21fe5b7a7d7a184720bc07da0b6c9b9820e97f25e
    lastState: {}
    name: nginx-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2025-09-15T17:02:45Z"
  - containerID: containerd://65a8dac95df427c3b0b384d2fe62e8f3b5e7452fae1b2b22279142acbe26c6b9
    image: docker.io/library/php:7.2-fpm-alpine
    imageID: docker.io/library/php@sha256:2e2d92415f3fc552e9a62548d1235f852c864fcdc94bcf2905805d92baefc87f
    lastState: {}
    name: php-fpm-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2025-09-15T17:02:38Z"
  hostIP: 172.17.0.2
  phase: Running
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2025-09-15T17:02:35Z"
```

---

### 3. Recreate pod to reload the config:

```bash
kubectl replace -f /tmp/nginx.yaml --force
kubectl get pods 
```
---

### 4. Copy the PHP file into the container:

```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container
```
### 5. Validate the result:

```bash
kubectl exec -it nginx-phpfpm -c nginx-container  -- curl -I  http://localhost:8099
```
> **Website:** Click on `Website` button to access website.

## Result

- The `volume mount` issue is successfully fixed.
