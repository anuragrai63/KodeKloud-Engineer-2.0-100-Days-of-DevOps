# Instructions

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 2 within the Stratos Datacenter.

Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 2. Additionally, ensure that all users have the capability to execute it.


# Solution

ssh into the App Server 2: `ssh steve@172.16.238.11`

chmod 755  /tmp/xfusioncorp.sh 

# Explanation:

chmod 755 sets executable permission for all user.

<img width="1102" height="94" alt="image" src="https://github.com/user-attachments/assets/3cb57c2e-2043-4555-bf57-a832b0f2b0c2" />


Check the result 
