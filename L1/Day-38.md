# Day 38: Pull and Retag Docker Image

## Scenario

Nautilus project developers are preparing to start testing a new project. Following a meeting with the DevOps team, they plan to test features in a containerized environment. The task requires:

- Pulling the `busybox:musl` image on **App Server 3** in Stratos DC.
- Retagging (creating a new tag for) this image as `busybox:blog`.

---

## Task

- Pull the `busybox:musl` Docker image.
- Retag the image as `busybox:blog`.

---

## Solution

### 1. SSH into App Server 3

```bash
ssh banner@stapp03
```

---

### 2. Pull the busybox:musl Image

```bash
docker pull busybox:musl
```

---

### 3. Retag the Image

> Find the IMAGE ID for `busybox:musl` using `docker images` if needed.

```bash
docker tag busybox:musl busybox:blog
```

---

### 4. Verify the Images

```bash
docker images
```

---

## Result

- The `busybox:musl` image is pulled and retagged as `busybox:blog` on App Server 3.
