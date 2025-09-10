# Day 27: Git Revert Some Changes

## Scenario

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/demo present on Storage server in Stratos DC. However, they reported an issue with the recent commits being pushed to this repo. They have asked the DevOps team to revert repo HEAD to last commit. Below are more details about the task:


In /usr/src/kodekloudrepos/demo git repository, revert the latest commit ( HEAD ) to the previous commit (JFYI the previous commit hash should be with initial commit message ).


Use revert demo message (please use all small letters for commit message) for the new revert commit.

## Tasks


---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to the repository directory:

```bash
cd /usr/src/kodekloudrepos/demo

```

---

### 3. Revert the latest commit (HEAD):

```bash
git revert HEAD --no-edit
git commit --amend -m "revert demo"

```

---

### 4. Verify the commit history:

```bash
git log --oneline

```

---



## Result

