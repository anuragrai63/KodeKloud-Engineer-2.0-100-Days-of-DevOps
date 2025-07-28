# Instructions

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 2 within the Stratos Datacenter.

Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 2. Additionally, ensure that all users have the capability to execute it.


# Solution

ssh into the App Server 2: `ssh steve@172.16.238.11`

chmod +x  /tmp/xfusioncorp.sh 

# Explanation:

chmod +x sets executable permission.

<img width="1426" height="258" alt="image" src="https://github.com/user-attachments/assets/a928b466-450c-4ecb-a886-51d628e62a71" />

Check the result 
