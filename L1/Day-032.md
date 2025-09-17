# Day 32: Git Rebase

## Scenario

The Nautilus application development team has been working on a project repository at `/opt/media.git`. This repository is cloned at `/usr/src/kodekloudrepos/media` on the Storage Server in Stratos DC. While a developer was working on the `feature` branch, some new commits were pushed to the `master` branch. The developer now wants to rebase the `feature` branch onto the latest `master` to incorporate the new changes.

After rebasing, make sure to push the updated `feature` branch to the remote repository.

---

## Task

- Rebase the `feature` branch in `/usr/src/kodekloudrepos/media` onto the latest `master` branch.
- Push the rebased `feature` branch to the remote repository.

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

### 3. Check the Current Branch and List All Branches

```bash
git branch
```

---

### 4. Switch to the `feature` Branch

```bash
git checkout feature
```

---

### 5. Rebase the `feature` Branch Onto `master`

```bash
git fetch origin
git rebase origin/master
```

---

### 6. Push the Rebases `feature` Branch to the Remote

```bash
git push origin feature --force
```

---

## Result

- The `feature` branch is now rebased onto the latest `master` branch and pushed to the remote repository, ensuring it is up-to-date with recent changes from `master`.
