![image](https://github.com/user-attachments/assets/67a769c2-eee1-4abf-92e5-71715c5b2036)


# SET-1: VPC and components setup
# one VPC.
# Two (2) public subnets spread across two availability zones (Web Tier).
# Two (2) private subnets spread across two availability zones (Application Tier).
# Two (2) private subnets spread across two availability zones (Database Tier).
# One (1) public route table that connects the public subnets to an internet gateway.
# One (1) private route table that will connect the Application Tier private subnets and a NAT gateway.

![image](https://github.com/user-attachments/assets/c7536f26-d253-4b64-aff4-aa1141993694)


# select the ‘VPC and more’ option and name our project ‘3tier-App’ with a CIDR block of 10.0.0.0/16.
![image](https://github.com/user-attachments/assets/89e71475-4072-4896-a128-37a3c5875165)

# two AZs (us-east-1a and us-east-1b), two public subnets, and four private subnets
![image](https://github.com/user-attachments/assets/5fcfa9e5-6e2f-4de0-8c1f-1e55057550f1)

## visualize the assets about to be created.
![image](https://github.com/user-attachments/assets/08084e90-5693-44a4-ac0c-2c21e3d2e102)


# we need to make sure we ‘Enable auto-assign public IPv4 address’ for BOTH public subnets so we can access its resources via the Internet.
![image](https://github.com/user-attachments/assets/c43c4cee-e45c-4f01-bfd7-4f41cde0dffc)

# public-rtb to serve as the main table, so select the public-rtb from the ‘Route tables’ dashboard and set it as the main table under the ‘Actions’ dropdown menu.

![image](https://github.com/user-attachments/assets/01c7bc63-74af-4f0d-a8c5-d754b8cc2d09)
![image](https://github.com/user-attachments/assets/d1e7f49f-1c37-47bf-9a56-4e7d3a56f3e5)


## Navigate to ‘NAT Gateways’ and create a new gateway called public-NAT-1. Select one of the public subnets, allocate an elastic IP, and create the gateway.
![image](https://github.com/user-attachments/assets/0546b00c-c570-4712-8fcb-ff5c91b93a76)

# Select private route tables and adjust the name
![image](https://github.com/user-attachments/assets/baa8e970-f9fd-476a-b8c3-717186a42654)


# Now let’s add a new route to our NAT gateway.
![image](https://github.com/user-attachments/assets/5799a3ec-1507-4507-a41e-cca266c3af88)

## there should be a total of two route tables, one with two associated, and one with four associated subnets.
![image](https://github.com/user-attachments/assets/577ee264-76f8-4075-94f5-3c99565ae8cd)


## Web tier (Frontend)
 1. Create a web server launch template

In the EC2 console, navigate to ‘Launch templates’ under the ‘Instances’ sidebar menu. We’re going to create a new template called ‘brainiac-webServer’ with the following provisions:

AMI: Amazon 2 Linux
Instance type: t2.micro (1GB – Free Tier)
A new or existing key pair
We’re not going to specify subnets, but we will create a new security group with inbound SSH, HTTP, and HTTPS rules. Make sure the proper brainiac VPC is selected.

![image](https://github.com/user-attachments/assets/f2296ba7-1cc9-4e70-ab51-0c3d8218ccce)
![image](https://github.com/user-attachments/assets/30ec6cf0-d0cb-41b2-a09d-dbd6c277658d)

# 2. Create an Auto scaling group (ASG)
ASG console from the sidebar menu and create a new group. The ASG will use the brainiac-webServer-template launch template we set up in the previous step.

Select the brainiac-vpc along with the two public subnets.

![image](https://github.com/user-attachments/assets/5030aef4-5b4a-4ac3-a17f-b093f035d00a)







checkkkkkkkkkkk

https://medium.com/@aaloktrivedi/building-a-3-tier-web-application-architecture-with-aws-eb5981613e30










2. Create an Auto scaling group (ASG)
To ensure high availability for the Brainiac web app and limit single points of failure, we will create an ASG that will dynamically provision EC2 instances, as needed, across multiple AZs in our public subnets.

Navigate to the ASG console from the sidebar menu and create a new group. The ASG will use the brainiac-webServer-template launch template we set up in the previous step.

Select the brainiac-vpc along with the two public subnets.


3. Application load balancer (ALB)
We’ll need an ALB to distribute incoming HTTP traffic to the proper targets (our EC2s). The ALB will be named, ‘brainiac-webServer-alb.’ We want this ALB to be ‘Internet-facing,’ so it can listen for HTTP/S requests.


Note: Creating an ALB From the ASG interface automatically attaches the default security group to our ALB. We need the brainiac-webServer-sg, so after the ASG is complete, we need to go back to the load balancer and make sure the proper security group is attached.

The ALB needs to ‘listen’ over HTTP on port 80 and a target group that routes to our EC2 instances.


We’ll also add a dynamic scaling policy that tells the ASG when to scale up or down EC2 instances. For this build, we’ll monitor the CPU usage and create more instances when the usage is above 50% (feel free to use whatever metric is appropriate for your application).


Group size
We want to set a minimum and maximum number of instances the ASG can provision:

Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 5
Review the ASG settings and create the group!

Once the ASG is fully initialized, we can go to our EC2 dashboard and see that two EC2 instances have been deployed.

To see if our ALB is properly routing traffic, let’s go to its public DNS. We should be able to access the website we implemented when creating our EC2 launch template.



Success!
SSH
Let's confirm that we can SSH into our EC2 server.


Success!
We’ve successfully built the architecture for the Web Tier for our Brainiac application! Remember, this is the ‘Presentation’ layer, where our users will directly interact with our app.

Tier 2: Application tier (Backend)
The Application Tier is essentially where the heart of our Brainiac app lives. This is where the source code and core operations send/retrieve data to/from the Web and Database tiers.

The structure is very similar to the Web Tier but with some minor additions and considerations.

What we will build:

A launch template to define the type of EC2 instances.
An Auto Scaling Group (ASG) to dynamically provision EC2 instances.
An Application Load Balancer (ALB) to route traffic from the Web tier.
A Bastion host to securely connect to our application servers.

1. Create an application server launch template
This template will define what kind of EC2 instances our backend services will use, so let’s create a new template called, ‘brainiac-appServer-template.’

We will use the same settings as the brainiac-webServer-template (Amazon 2 Linux, t2.micro-1GB, same key pair).

Our security group settings are where things will differ. Remember, this is a private subnet, where all of our application source code will live. We need to take precautions so it cannot be accessible from the outside.

We want to allow ICMP–IPv4 from the brainiac-webServer-sg, which allows us to ping the application server from our web server.



The application servers will eventually need to access the database, so we need to make sure the mySQL package is installed on each instance.

In the ‘User data’ field under ‘Advanced details,’ paste in this script:

#!/bin/bash
sudo yum install mysql -y
Review and create the template.

2. Create an Auto Scaling Group (ASG)
Similar to the Web Tier, we’ll create an ASG from the brainiac-appServer-template called, ‘brainiac-appServer-asg.’

Make sure to select the brainiac-vpc and the 2 private subnets (subnet-private1 and subnet-private2).


3. Application Load Balancer (ALB)
Now we’ll create another ALB that routes traffic from the Web Tier to the Application Tier. We’ll name it ‘brainiac-appServer-alb.’

This time, we want the ALB to be ‘Internal,’ since we’re routing traffic from our Web Tier, not the Internet.


We’ll also create another target group that will target our appServer EC2 instances.


Now we can review our settings and create the group.


It may take a few minutes for the ASG to fully initialize.
Great! We should see two more EC2 instances running from our private subnets.

Confirm connectivity from the Web Tier
Our application servers are up and running. Let’s verify connectivity by pinging the application server from one of the web servers.

SSH into the web server EC2 and ping the private IP address of one of the app server EC2s.

ssh -i "webServer_key.pem" ec2-user@ec2-54-209-250-120.compute-1.amazonaws.com

ping PRIVATE_IPV4_ADDRESS
If successful, you should get a repeating response like this:


type ^C to terminate the process
Woo! We’ve successfully pinged the app server and received a response!

4. Create a Bastion host
A bastion host is a dedicated server used to securely access a private network from a public network. We want to protect our Application Tier from potential outside access points, so we will create an EC2 instance in the Web Tier, outside of the ASG. This is the only server that will be used as a gateway to our app servers.

In the EC2 console, launch a new instance called, ‘brainiac-bastionHost.’ We’ll use the same provisions as before (Amazon Linux2, t2.micro). Make sure the brainiac-vpc is selected, as well as one of the public subnets.


Create a new security group called, ‘brainiac-bastionHost-sg,’ and only allow SSH through My IP.


Now we have to edit our inbound rules for the brainiac-appServer-sg to make sure we’re allowing SSH access ONLY from the bastion host server.


Test the connection
Let’s see if we can connect to our application server through our bastion host.

IMPORTANT: To SSH into our app server, we need to ‘forward’ our key pair from our web server through an SSH Agent. You can watch this video for a better explanation and demo on how to do this.

Once the key pair is added to the Agent, SSH into the bastion host.

ssh -A ec2-user@BASTIONHOST_PUBLIC_IP
And then SSH into our app server (remember, we need the private IPv4 address).

[ec2-user@ip-10-0-28-148 ~]$ ssh -A ec2-user@APPSERVER_PRIVATE_IP

Success!
We’ve successfully built the Application Tier architecture for our Brainiac application! Remember, this is the ‘Backend’ layer, where our source code lives and backend operations send/retrieve data to/from the Web Tier and Database Tier.

Tier 3: Database tier (Data storage & retrieval)
Almost there! Now it's time to build the last tier of our Brainiac application architecture: the Database. Every application needs a way to store important data, such as user login info, session data, transactions, application content, etc… Our application servers need to be able to read and write to databases to perform necessary tasks and deliver proper content/services to the Web Tier and users.

We are going to use a Relational Database Service (RDS) that uses MySQL.

What we’ll build:

A database security group that allows outbound and inbound mySQL requests to and from our app servers.
A DB subnet group to ensure the database is created in the proper subnets.
An RDS database with MySql.

1. Create a database security group
Our application servers need a way to access the database, so let’s first create a security group that allows inbound traffic from the application servers.

Create a new security group called, ‘brainiac-db-sg.’ Make sure the Brainiac vpc is selected.


Now, we need to add inbound AND outbound rules that allow MySQL requests to and from the application servers on port 3306.



We’ll need to do the same for the brainiac-appServer-sg.



2. Create a DB subnet group
In the RDS console, under the ‘Subnet groups’ sidebar menu, create a new subnet group called, ‘brainiac-db-subnetGroup.’ Make sure the brainiac-vpc is selected.


Remember from our diagram, we want the database located in -subnet-private3 and span multiple AZs and subnets, if necessary.

Select our two AZs (us-east-1 and us-east-2) and our private subnets (-subnet-private3 and -subnet-private4). Unfortunately, the selection dropdown, doesn't provide the subnet names, so we might have to navigate back to our main Subnets dashboard to get the right ids.



3. Create an RDS database
Under the RDS console and the ‘Databases’ sidebar menu, create a new database with a MySQL engine.


For our purposes, we’ll stick to the ‘Free tier’ option.

If we were to use this database for production/dev environments, it’s best practice to enable Multi-AZ deployment for higher availability, but this does incur a cost. Multi-AZ deployments allow us to create a ‘Standby’ or ‘Failover’ database that serves as a back-up, should something happen to our main instance or AZ. It also allows us to create a ‘read-replica’ database, which, essentially, is a read-only version of our DB and allows for more efficient queries from the Application Tier.


We’ll call this database, ‘brainiac-webApp-db,’ and create a master username and password (we’ll use this to log into our DB from the command line, so keep this info handy).


For ‘Instance configuration,’ we’ll use a db.t2.micro and leave the defaults for ‘Storage.’

For ‘Connectivity,’ we do not want to connect an EC2 instance but make sure the brainiac-vpc is selected.


Select the DB subnet group we created earlier. We also do not want to enable ‘Public access.’


Choose our brainiac-db-sg security group and select us-east-1a as the preferred AZ.


Under ‘Additional configuration,’ repeat the name of the database you created in the first step (without dashes).

Leave the defaults for everything else and create the database (this may take a few minutes to fully provision).


Connect to the Database
After the DB has been created, we’ll need the database endpoint to establish a connection from the app server.


If you haven't yet, SSH into the app server through our bastion host.

We should already have mySQL installed on the server, so we can run this command:

mysql -h YOUR_DB_ENDPOINT -P 3306 -u YOUR_DB_USERNAME -p
When prompted, enter the password you chose when creating the DB.


Great! We successfully connected to our database from our application server!
