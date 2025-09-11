# Day 31: Git Stash – Restoring and Committing Stashed Changes

## Scenario

The Nautilus application development team was working on the `/usr/src/kodekloudrepos/media` Git repository on the Storage Server in Stratos DC. One of the developers stashed some in-progress changes, and now these changes need to be restored, committed, and pushed to the remote repository.

---

## Task

- Check for stashed changes in `/usr/src/kodekloudrepos/media`.
- Restore the stash with the identifier `stash@{1}`.
- Commit and push the restored changes to the remote repository (`origin`).

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

### 3. Check the Stash List to Confirm `stash@{1}` Exists

```bash
git stash list
```

- You should see entries like:
  ```
  stash@{0}: WIP on main: ...
  stash@{1}: WIP on main: ...
  ```

---

### 4. Apply the `stash@{1}`

```bash
git stash apply stash@{1}
```

---

### 5. Stage the Restored Changes

```bash
git add .
```

---

### 6. Commit the Changes

```bash
git commit -m "Restored stash@{1} changes"
```

---

### 7. Push the Commit to the Origin

```bash
git push origin master
```

---

## Result

- The changes from `stash@{1}` have been restored, committed, and pushed to the `master` branch on the remote repository.
