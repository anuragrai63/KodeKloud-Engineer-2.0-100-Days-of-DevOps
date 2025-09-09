# Day 26: Managing Git Remotes

## Scenario

The xFusionCorp development team maintains a project in the `/opt/apps.git` repository, which is cloned locally at `/usr/src/kodekloudrepos/apps`. Recently, the Git server setup has changed, and you need to add a new remote, commit an updated file, and push changes accordingly.

---

## Tasks

1. In `/usr/src/kodekloudrepos/apps`, add a new remote named `dev_apps` that points to `/opt/xfusioncorp_apps.git`.
2. Copy the file `/tmp/index.html` into the repository and add/commit it to the `master` branch.
3. Push the `master` branch to the new `dev_apps` remote.

---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to the Cloned Repository

```bash
cd /usr/src/kodekloudrepos/apps
```

---

### 3. Add the New Remote Named `dev_apps`

```bash
git remote add dev_apps /opt/xfusioncorp_apps.git
```

---

### 4. Copy `index.html` into the Repository

```bash
cp /tmp/index.html .
```

---

### 5. Add and Commit the File to the `master` Branch

```bash
git add index.html
git commit -m "Add index.html to master branch"
```

---

### 6. Push the `master` Branch to the New Remote `dev_apps`

```bash
git push dev_apps master
```

---

## Result

- A new remote `dev_apps` is added, pointing to `/opt/xfusioncorp_apps.git`.
- `index.html` is copied, added, and committed to the `master` branch.
- The `master` branch is pushed to the new remote `dev_apps`.
