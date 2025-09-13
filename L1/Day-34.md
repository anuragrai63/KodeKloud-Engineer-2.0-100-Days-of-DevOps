# Day 34: 

## Scenario

The Nautilus application development team was working on a git repository /opt/official.git which is cloned under /usr/src/kodekloudrepos directory present on Storage server in Stratos DC. The team want to setup a hook on this repository, please find below more details:



Merge the feature branch into the master branch`, but before pushing your changes complete below point.

Create a post-update hook in this git repository so that whenever any changes are pushed to the master branch, it creates a release tag with name release-2023-06-15, where 2023-06-15 is supposed to be the current date. For example if today is 20th June, 2023 then the release tag must be release-2023-06-20. Make sure you test the hook at least once and create a release tag for today's release.

Finally remember to push your changes.
Note: Perform this task using the natasha user, and ensure the repository or existing directory permissions are not altered.

---

## Task


---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Merging the Branches

```bash
cd /usr/src/kodekloudrepos/official
sudo git checkout master
sudo git merge feature
```

---

### 3. Creating the post-update Hook

```bash
cd /opt/official.git/hooks
sudo vi post-update
```
Add Script Content

#!/bin/sh
DATE=$(date +%Y-%m-%d)
TAG_NAME="release-$DATE"

if ! git tag -l | grep -q "$TAG_NAME"; then
  git tag "$TAG_NAME"
  echo "Created tag: $TAG_NAME"
else
  echo "Tag $TAG_NAME already exists. Skipping..."
fi

---

### 4. Make the script executable and set ownership:

```bash
sudo chmod +x post-update
sudo chown natasha:natasha post-update
```


---

### 5. Pushing Changes and Verifying the Hook

cd /usr/src/kodekloudrepos/official
sudo git push origin master


### 6. Confirm the tag's existence:

```bash
sudo git ls-remote --tags origin
```

---


## Result

