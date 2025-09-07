# Instructions
xFusionCorp Industries is planning to host two static websites on their infra in Stratos Datacenter. The development of these websites is still in-progress, but we want to get the servers ready. Please perform the following steps to accomplish the task:

a. Install httpd package and dependencies on app server 1.

b. Apache should serve on port 3002.

c. There are two website's backups /home/thor/ecommerce and /home/thor/apps on jump_host. Set them up on Apache in a way that ecommerce should work on the link http://localhost:3002/ecommerce/ and apps should work on link http://localhost:3002/apps/ on the mentioned app server.

d. Once configured you should be able to access the website using curl command on the respective app server, i.e curl http://localhost:3002/ecommerce/ and curl http://localhost:3002/apps/

# Solution
ssh app1 hosts:

sudo yum install -y httpd

sudo systemctl enable httpd

Configure Apache to Serve on Port 3002

sudo vi /etc/httpd/conf/httpd.conf

Change the Listen directive:

Listen 3002

Restart:-

sudo systemctl restart httpd

Set Up Static Sites from Jump Host:-

scp -r /home/thor/ecommerce tony@stapp01:/tmp/

scp -r /home/thor/apps tony@stapp01:/tmp/

On app server 1, move them to Apache's root:

sudo mv /tmp/ecommerce /var/www/html/

sudo mv /tmp/apps /var/www/html/

Set proper permissions:

sudo chown -R apache:apache /var/www/html/ecommerce

sudo chown -R apache:apache /var/www/html/apps

Verify with curl:- 

curl http://localhost:3002/ecommerce/

curl http://localhost:3002/apps/

Check the result 
