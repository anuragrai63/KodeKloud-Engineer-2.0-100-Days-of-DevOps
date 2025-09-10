# Day 30: Git hard reset

## Scenario

The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/media present on Storage server in Stratos DC. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the HEAD and the branch itself to a commit with message add data.txt file. Find below more details:

In /usr/src/kodekloudrepos/media git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and add data.txt file.

Also make sure to push your changes.


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
/usr/src/kodekloudrepos/media
```

---

### 3. Identify the commit hash for "add data.txt file":

```bash
git log --oneline

```
Look for the commit with the message add data.txt file and copy its hash

---

### 4. Create a temporary branch from that commit:

```bash
git checkout -b clean-history <commit-hash>

```

---

### 5. Reset the branch to that commit, keeping only the initial and target commit:
git rebase -i --root

Delete all lines except the initial commit and add data.txt file.

Save and exit the editor.

### 6. Force push the cleaned history to the remote:
git checkout master
git reset --hard clean-history
git push origin master --force


## Result

