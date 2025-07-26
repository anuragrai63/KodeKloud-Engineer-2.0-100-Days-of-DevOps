# Instructions

As part of the temporary assignment to the Nautilus project, a developer named javed requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:

Create a user named javed on App Server 2 in Stratos Datacenter. Set the expiry date to 2024-01-28, ensuring the user is created in lowercase as per standard protocol.

# Solution

ssh into the App Server 2: `ssh steve@172.16.238.11`

sudo useradd -e 2024-01-28 javed

# Explanation:

useradd: creates a new user

-e 2024-01-28: sets the account's expiry date to January 28, 2024

javed: username, lowercase as per protocol

<img width="1380" height="356" alt="image" src="https://github.com/user-attachments/assets/379c5ed5-ec54-4cc0-99e8-39d2496affa3" />


Check the result 
