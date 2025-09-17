# Day 33: Resolve Git Merge Conflicts

## Scenario

Sarah and Max are working on writing some stories which they have both pushed to the repository. Max has recently added new changes and is trying to push them to the repository, but he is facing some merge conflicts.

You need to SSH into the storage server using the following credentials:

- **Username:** max  
- **Password:** Max_pass123

Once connected, navigate to the `/home/max/story-blog` repository. Try to push Max's changes to the origin repository and resolve any merge conflicts that occur, especially in the `story-index.txt` file.

Additionally, you can use the Gitea UI to verify and manage repository changes:

- Click on the **Gitea UI** button on the top bar.
- Login to the Gitea server using:
  - **Username:** sarah / **Password:** Sarah_pass123  
  - **or**
  - **Username:** max / **Password:** Max_pass123

**Note:** For scenarios requiring changes in a web UI, please take screenshots as proof of your work in case your task is marked incomplete. You may also contact the support team if you face any issues.

---

## Task

1. SSH into the storage server as user `max`.
2. Navigate to the `story-blog` repository.
3. Attempt to push changes to the origin repository.
4. Resolve any Git merge conflicts that arise.
5. Verify the changes using the Gitea web UI.

---

## Solution

### 1. SSH into the Storage Server

```bash
ssh max@ststor01
```

---

### 2. Navigate to the Repository Directory

```bash
cd /home/max/story-blog
```

---

### 3. Check the Remote Repository

```bash
git remote -v
```

---

### 4. Pull the Latest Changes from Remote

```bash
git pull
```

If you encounter merge conflicts, proceed to the next step.

---

### 5. Resolve Merge Conflicts in `story-index.txt`

Open the conflicting file in an editor:

```bash
vi story-index.txt
```

Manually edit the file to remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) and keep the correct content.  
**Example cleaned-up content:**

```
The Lion and the Mouse
The Fox and the Grapes
The Tortoise and the Hare
The Ant and the Grasshopper
```

Save and exit the editor.

---

### 6. Add, Commit, and Push the Changes

```bash
git add .
git commit -m "Resolved merge conflict in story-index.txt"
git push
```

---

### 7. Login to Gitea UI and Verify Changes

- Access the Gitea UI.
- Login as `sarah` or `max`.
- Verify that the latest changes have been pushed and merged.

---

## Result

You have successfully resolved the Git merge conflict, pushed the changes, and verified them via the Gitea web UI.
