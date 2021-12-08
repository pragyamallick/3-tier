# 3-tier
This is for creating a 3-tier environment using AWS cloud.

# Network layer
Create a VPC, 1 public subnet for web , 1 private subnet for app and 1 private subnet for database in two availibility zones.

Create an internet gateway with the vpc.

Create NAT gateway in the public subnet and allocate elastic ip address.

Create route tables in web app and DB using the same VPC.

Associate route table with subnet in subnet asssociation.

Add route in web,app,DB route table: Inbound rules --> 0.0.0.0/0

# Application layer
Create EC2 instance which will be used as jump server: using ami linux

Attach the same VPC

Attach the public subnet created

Create new security group

Launch instance: Create Key pair and download the pem keys

Create another EC2 instance: App server1 in the private app subnet with new security group for app layer.

Allow ssh only from jump server

Create another EC2 instance: App server2 in same private app subnet.

Login to jump server and then login to app server

Install PHP and apache

Install httpd

Start httpd services

Give ec2 user correct permissions

Install phpmy admin and restart apache

# Load Balancer
Create an ALB in the same VPC in the public subnet with new security group.

Create a target group with type: instance and register targets.

Edit security group of App servers by adding security group of load balancer.

# Test
Create index.html inside /var/www/html and put sample text from both the app servers and test on browser.

# Database layer
Create a new subnet group in RDS inside same VPC and using private subnet of database with new security group.

Choose Mysql standard and save credentials.

Change security group inbound rules and connect it to application security group on port 3306.
copy the end point.

Go to app server and change config file and replace host by endpoint.

Test on Browser.

# Architecture Diagram
Network:
![myaws](https://user-images.githubusercontent.com/95772594/145276170-b5d2fc18-8484-45e5-a1f9-60afa69ecc84.png)

Application:
![deployaws drawio](https://user-images.githubusercontent.com/95772594/145276215-8b65608d-c48d-4266-ba9b-5750ca6fa563.png)




