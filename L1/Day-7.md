# Instructions

The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:

Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

# Solution

Generate SSH Key on Jump Server:

ssh-keygen -t rsa

Copy Public Key to App Servers

ssh-copy-id tony@172.16.238.10
ssh-copy-id steve@172.16.238.11
ssh-copy-id banner@172.16.238.12

# Explanation:

ssh-copy-id to install thor's public key on each app server

<img width="830" height="466" alt="image" src="https://github.com/user-attachments/assets/3e6946d6-73a6-482d-b46b-54eeab8925a2" />


Check the result 
