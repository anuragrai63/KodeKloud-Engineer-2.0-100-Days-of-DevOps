# Day 25: Git Merge Branches

## Scenario

The Nautilus application development team has been working on a project repository /opt/media.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:



Create a new branch devops in /usr/src/kodekloudrepos/media repo from master and copy the /tmp/index.html file (present on storage server itself) into the repo. Further, add/commit this file in the new branch and merge back that branch into master branch. Finally, push the changes to the origin for both of the branches.

---



## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to the Repository

```bash
cd /usr/src/kodekloudrepos/media

```

---

### 3. Create and switch to the devops branch

```bash
git checkout -b devops

```

---

### 4. Copy the index.html file into the repo

```bash
cp /tmp/index.html .

```

---

Add and commit the file:

git add index.html
git commit -m "Add index.html to devops branch"

Switch back to master and merge devops:
git checkout master
git merge devops

Push both branches to origin:
git push origin master
git push origin devops


## Result

