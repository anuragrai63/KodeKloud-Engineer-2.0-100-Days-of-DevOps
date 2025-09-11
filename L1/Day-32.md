# Day 32: Git Rebase

## Scenario

The Nautilus application development team has been working on a project repository /opt/media.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:



One of the developers is working on feature branch and their work is still in progress, however there are some changes which have been pushed into the master branch, the developer now wants to rebase the feature branch with the master branch without loosing any data from the feature branch, also they don't want to add any merge commit by simply merging the master branch into the feature branch. Accomplish this task as per requirements mentioned.


Also remember to push your changes once done.
---

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
cd /usr/src/kodekloudrepos/media
```

---

### 3. Check the current branch and list all branches:

```bash
git branch

```

---

### 4. Switch to the feature branch:

```bash
git checkout feature
```

---

### 5. Rebase the feature branch with master:

```bash
git fetch origin
git rebase origin/master

```

---

### 6. Push the rebased feature branch to origin:

```bash
git push origin feature --force

```

---


## Result



