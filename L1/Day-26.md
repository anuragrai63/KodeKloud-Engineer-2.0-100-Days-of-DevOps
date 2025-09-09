# Day 26: Git Manage Remotes

## Scenario

The xFusionCorp development team added updates to the project that is maintained under /opt/apps.git repo and cloned under /usr/src/kodekloudrepos/apps. Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on /usr/src/kodekloudrepos/apps repository as per details mentioned below:


a. In /usr/src/kodekloudrepos/apps repo add a new remote dev_apps and point it to /opt/xfusioncorp_apps.git repository.


b. There is a file /tmp/index.html on same server; copy this file to the repo and add/commit to master branch.


c. Finally push master branch to this new remote origin.
---

## Task



---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to the cloned repository

```bash
cd /usr/src/kodekloudrepos/apps

```

---

### 3. Add the new remote named dev_apps

```bash
git remote add dev_apps /opt/xfusioncorp_apps.git

```

---

### 4. Copy `index.html` into the Repo

```bash
cp /tmp/index.html .
```

---

### 5. Add and commit the file to the master branch

```bash
git add index.html
git commit -m "Add index.html to master branch"

```

---

### 6. Push master branch to the new remote dev_apps

```bash
git push dev_apps master

```

---

### 7. Push Both Branches to Origin

```bash
git push origin master
git push origin devops
```

---

## Result

- A new branch `devops` is created from `master`.
- `index.html` is added and committed on the `devops` branch.
- Changes from `devops` are merged back into `master`.
- Both branches are pushed to the remote repository (`origin`).
