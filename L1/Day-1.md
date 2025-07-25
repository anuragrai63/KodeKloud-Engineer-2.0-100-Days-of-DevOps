# Instructions

To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell. Here's your task: 
Create a user named john with a non-interactive shell on App Server 3.


# Solution

ssh into the App Server 3: `ssh banner@172.16.238.12`

sudo useradd -m -s /sbin/nologin john

# Explanation:

sudo: Runs the command with administrative privileges.

useradd: Command to create a new user.

-m: Creates a home directory for the user.

-s /sbin/nologin: Sets the shell to /sbin/nologin, which prevents interactive login.

<img width="1214" height="154" alt="image" src="https://github.com/user-attachments/assets/39d90d15-48e7-4e70-90df-e896afdc4e63" />


Check the result 
