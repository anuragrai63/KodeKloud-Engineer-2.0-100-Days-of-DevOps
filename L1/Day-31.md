# Day 31: Git Stash

## Scenario

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/media present on Storage server in Stratos DC. One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:



Look for the stashed changes under /usr/src/kodekloudrepos/media git repository, and restore the stash with stash@{1} identifier. Further, commit and push your changes to the origin.

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

### 3. Check the stash list to confirm stash@{1} exists:

```bash
git stash list

```

You should see something like:
stash@{0}: WIP on main: ...
stash@{1}: WIP on main: ...

---

### 4. Apply the stash@{1}:

```bash
git stash apply stash@{1}

```


---

### 5. Stage the restored changes:

```bash
git add .

```

---

### 6. Commit the changes:

```bash
git commit -m "Restored stash@{1} changes"

```

---

### 7. Push the commit to the origin:

git push origin master


## Result

