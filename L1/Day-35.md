# Day 35 Docker Install

## Scenario

The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team. They intend to conduct testing with the following steps:

Install docker-ce and docker compose packages on App Server 2.

Initiate the docker service.

---

## Task



---

## Solution

### 1. SSH into the Storage Server

```bash
ssh steve@stapp02
```

---

### 2. Install Docker CE & Compose

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose -y

```

---

### 3. Start and Enable Docker Service

```bash
sudo systemctl start docker
sudo systemctl enable docker

```


## Result

