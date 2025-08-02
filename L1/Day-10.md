# Instructions

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 1 in Stratos Datacenter, and they need to create a bash script named beta_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 1).

a. Create a zip archive named xfusioncorp_beta.zip of /var/www/html/beta directory.

b. Save the archive in /backup/ on App Server 1. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.

c. Copy the created archive to Nautilus Backup Server server in /backup/ location.

d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

# Solution

Log in to the App & Backup server using SSH:

ssh tony@172.16.238.10

ssh clint@172.16.238.16

On App Server

sudo mkdir -p /scripts

sudo chown tony:tony /scripts

sudo vi /scripts/beta_backup.sh

Populate below

#!/bin/bash

SOURCE_DIR="/var/www/html/beta"

ARCHIVE_NAME="xfusioncorp_beta.zip"

LOCAL_BACKUP="/backup"

REMOTE_BACKUP="/backup"

REMOTE_USER="clint"    

REMOTE_HOST="172.16.238.16"    

zip -r "${LOCAL_BACKUP}/${ARCHIVE_NAME}" "$SOURCE_DIR"

scp "${LOCAL_BACKUP}/${ARCHIVE_NAME}" "${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_BACKUP}/"

chmod +x /scripts/beta_backup.sh

Generate key and copy pub key in backup server

ssh-keygen -t rsa

ssh-copy-id clint@172.16.238.16

Test the Script

/scripts/beta_backup.sh

# Explanation:

To meet the backup requirements for the static website on App Server 1, here's how to create the beta_backup.sh script and configure password-less file transfer to the Nautilus Backup Server.

<img width="1498" height="248" alt="image" src="https://github.com/user-attachments/assets/a5f71508-7d3e-4b2b-8f72-2f1548f22ed0" />

Check the result 
