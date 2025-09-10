# Day 28: Git Cherry Pick

## Scenario

The Nautilus application development team has been working on a project repository /opt/demo.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with the DevOps team:



There are two branches in this repository, master and feature. One of the developers is working on the feature branch and their work is still in progress, however they want to merge one of the commits from the feature branch to the master branch, the message for the commit that needs to be merged into master is Update info.txt. Accomplish this task for them, also remember to push your changes eventually.

## Task


---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to the Repository Directory

```bash
cd /usr/src/kodekloudrepos/demo
```

---

### 3. Ensure you have the latest changes:

```bash
git fetch --all

```


---

### 4. Identify the commit hash from the feature branch:

```bash
git log feature

```

---
5 Look for the commit with the message:
Update info.txt

6 Cherry-pick the commit into master:
git cherry-pick <commit-hash>


7 Push the changes to the remote master branch:
git push origin master



## Result

