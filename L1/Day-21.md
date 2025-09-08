# Day 1: Creating a User with a Non-Interactive Shell

## Scenario

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC:

Utilize yum to install the git package on the Storage Server.

Create a bare repository named /opt/media.git (ensure exact name usage).

---



## Solution

### 1. SSH into App Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Install Git using yum

```bash
sudo yum install git -y
```

---

Create a Bare Git Repository:

sudo git init --bare /opt/media.git


## Explanation



---

**Result:**  
