# Day 29: 

## Scenario

Max want to push some new changes to one of the repositories but we don't want people to push directly to master branch, since that would be the final version of the code. It should always only have content that has been reviewed and approved. We cannot just allow everyone to directly push to the master branch. So, let's do it the right way as discussed below:


SSH into storage server using user max, password Max_pass123 . There you can find an already cloned repo under Max user's home.


Max has written his story about The 🦊 Fox and Grapes 🍇


Max has already pushed his story to remote git repository hosted on Gitea branch story/fox-and-grapes


Check the contents of the cloned repository. Confirm that you can see Sarah's story and history of commits by running git log and validate author info, commit message etc.


Max has pushed his story, but his story is still not in the master branch. Let's create a Pull Request(PR) to merge Max's story/fox-and-grapes branch into the master branch


Click on the Gitea UI button on the top bar. You should be able to access the Gitea page.


UI login info:

- Username: max

- Password: Max_pass123

PR title : Added fox-and-grapes story

PR pull from branch: story/fox-and-grapes (source)

PR merge into branch: master (destination)

Before we can add our story to the master branch, it has to be reviewed. So, let's ask tom to review our PR by assigning him as a reviewer

Add tom as reviewer through the Git Portal UI

Go to the newly created PR

Click on Reviewers on the right

Add tom as a reviewer to the PR

Now let's review and approve the PR as user Tom

Login to the portal with the user tom

Logout of Git Portal UI if logged in as max

## Task


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

### 3. Run git log to inspect commit history:

```bash
git log --oneline --author="sarah"
git log --oneline --author="max"

```

---

### 4. Create a Pull Request in Gitea UI

```bash
Open the Gitea portal via the Gitea UI button on the top bar.

Log in with:

Username: max

Password: Max_pass123

Navigate to the repository.

Click Pull Requests → New Pull Request.

Fill in:

Title: Added fox-and-grapes story

Source Branch: story/fox-and-grapes

Target Branch: master

Submit the PR.

---

### 5.Assign Tom as Reviewer

Log out from Max’s account.

Log in with:

Username: tom

Password: (you may need to retrieve this if not provided)

Open the PR.

Review the changes.

Click Approve.

Once approved, the PR can be merged into master — ensuring only reviewed content makes it to the final branch.

---


```

---

## Result

