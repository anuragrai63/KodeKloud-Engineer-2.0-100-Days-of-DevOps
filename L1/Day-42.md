# Day 42: Create a Docker Network

## Scenario

The Nautilus DevOps team needs to set up several Docker environments for different applications. One team member has been assigned a ticket to create a specific Docker network with the following requirements:

- Create a Docker network named `ecommerce` on **App Server 3** in Stratos DC.
- Configure the network to use the **macvlan** driver.
- Set the network to use subnet `172.28.0.0/24` and IP range `172.28.0.0/24`.

---

## Task

- Create a Docker network called `ecommerce` using the macvlan driver, with the specified subnet and IP range.

---

## Solution

### 1. SSH into App Server 3

```bash
ssh banner@stapp03
```

---

### 2. Create the Macvlan Network

```bash
docker network create \
  -d macvlan \
  --subnet=172.28.0.0/24 \
  --ip-range=172.28.0.0/24 \
  --gateway=172.28.0.1 \
  -o parent=eth0 \
  ecommerce
```

> **Note:** Replace `eth0` with the actual network interface if it differs on your server.

---

### 3. Verify the Network

```bash
docker network inspect ecommerce
```

---

## Result

- The `ecommerce` Docker network is successfully created with the macvlan driver, subnet `172.28.0.0/24`, and IP range `172.28.0.0/24` on App Server 3.
