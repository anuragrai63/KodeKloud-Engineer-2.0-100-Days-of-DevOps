# Day 25: Git Merge Branches

## Scenario

The Nautilus application development team has been working on the project repository `/opt/media.git`, which is cloned at `/usr/src/kodekloudrepos/media` on the Storage Server in Stratos DC. The team has requested that a new branch be created, a file added and committed, and the changes merged back into the master branch.

---

## Task

- Create a new branch `devops` from `master` in `/usr/src/kodekloudrepos/media` Git repo.
- Copy the `/tmp/index.html` file (located on the Storage Server) into the repository.
- Add and commit this file on the `devops` branch.
- Merge the `devops` branch into the `master` branch.
- Push both branches to the remote repository.

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

### 3. Create and Switch to the `devops` Branch

```bash
git checkout -b devops
```

---

### 4. Copy `index.html` into the Repo

```bash
cp /tmp/index.html .
```

---

### 5. Add and Commit the File

```bash
git add index.html
git commit -m "Add index.html to devops branch"
```

---

### 6. Switch Back to `master` and Merge `devops`

```bash
git checkout master
git merge devops
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
