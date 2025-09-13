# Day 34 Git Hook

## Scenario

The Nautilus application development team was working on a Git repository located at `/opt/official.git`, which is cloned under `/usr/src/kodekloudrepos` directory on the Storage server in Stratos DC. The team was tasked to merge a feature branch into the `master` branch, but **before pushing the changes**, you must complete the following:

> **Create a `post-update` hook in this Git repository so that whenever any changes are pushed to the `master` branch, it creates a release tag named `release-YYYY-MM-DD`, where `YYYY-MM-DD` is the current date. If a tag with the same name already exists, do not create it again.**

**Finally, remember to push your changes.**

> **Note:** Perform this task using the `natasha` user, and ensure the repository or existing directory permissions are not altered.

---

## Task

- Merge the `feature` branch into the `master` branch.
- Set up a `post-update` Git hook to create a dated release tag on every push to `master`.
- Push your changes.
- Ensure everything is done as the `natasha` user, without altering permissions.

---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Merge the Branches

```bash
cd /usr/src/kodekloudrepos/official
git checkout master
git merge feature
```

---

### 3. Create the `post-update` Hook

```bash
cd /opt/official.git/hooks
vi post-update
```

**Add the following content to `post-update`:**

```sh
#!/bin/sh
BRANCH=$(git rev-parse --abbrev-ref HEAD)

if [ "$BRANCH" = "master" ]; then
  DATE=$(date +%Y-%m-%d)
  TAG_NAME="release-$DATE"

  if ! git tag -l | grep -q "$TAG_NAME"; then
    git tag "$TAG_NAME"
    echo "Created tag: $TAG_NAME"
  else
    echo "Tag $TAG_NAME already exists. Skipping..."
  fi
fi
```

---

### 4. Make the Hook Executable

```bash
chmod +x post-update
chown natasha:natasha post-update
```

---

### 5. Push Changes and Verify the Hook

```bash
cd /usr/src/kodekloudrepos/official
git push origin master
```

---

### 6. Confirm the Tag's Existence

```bash
git ls-remote --tags origin
```

---

## Result

- The `feature` branch is merged into `master`.
- On each push to `master`, a tag named `release-YYYY-MM-DD` is created (if it does not already exist).
- All actions are performed as the `natasha` user, with permissions preserved.
