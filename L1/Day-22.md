# Day 22: Cloning a Local Git Repository

## Scenario

The DevOps team has set up a new Git repository, which is currently unused. The Nautilus application development team now needs a copy of this repository on the Storage Server for further development and collaboration.

- The existing repository is located at: `/opt/cluster.git`
- You need to clone this repository to: `/usr/src/kodekloudrepos`
- Perform this task as the `natasha` user.
- Do not modify the repository or any existing directories during this process.

---

## Tasks

- Clone the Git repository `/opt/cluster.git` to `/usr/src/kodekloudrepos` as the `natasha` user.
- Ensure no modifications are made to the repository or existing directories.

---

## Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@ststor01
```

---

### 2. Clone the Local Git Repository

```bash
sudo -u natasha test -d /usr/src/kodekloudrepos || sudo -u natasha mkdir -p /usr/src/kodekloudrepos
sudo -u natasha git clone /opt/cluster.git /usr/src/kodekloudrepos
```

---

## Explanation

- `git clone /opt/cluster.git /usr/src/kodekloudrepos` clones the bare repository located at `/opt/cluster.git` into the `/usr/src/kodekloudrepos` directory.
- This creates a working copy of the repository for the development team, without making any changes to the original repository or other directories.

---

**Result:**  
The repository `/opt/cluster.git` has been successfully cloned to `/usr/src/kodekloudrepos` on the Storage Server under the `natasha` user, ready for use by the application development team.
