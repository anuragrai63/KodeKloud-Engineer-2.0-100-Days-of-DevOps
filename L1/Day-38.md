# Day 38: Pull Docker Image

## Scenario

Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task:


a. Pull busybox:musl image on App Server 3 in Stratos DC and re-tag (create new tag) this image as busybox:blog.

---

## Task


---

## Solution

### 1. SSH into App Server 1

```bash
ssh banner@stapp03
```

---

### 2. Image pull 

```bash
docker pull busybox:musl
```

---

### 3. Retag image

```bash
docker tag 44f1048931f5 busybox:blog
```

---

### 4. Verify image

```bash
docker images
```

---

## Result

