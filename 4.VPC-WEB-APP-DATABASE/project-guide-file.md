![image](https://github.com/user-attachments/assets/67a769c2-eee1-4abf-92e5-71715c5b2036)


# SET-1: VPC and components setup
# one VPC.
# Two (2) public subnets spread across two availability zones (Web Tier) & (baston server).
# Two (2) private subnets spread across two availability zones (Application Tier) & (Database Tier).
# One (1) public route table that connects the public subnets to an internet gateway.
# One (1) private route table that will connect the Application Tier private subnets and a NAT gateway.

![image](https://github.com/user-attachments/assets/c7536f26-d253-4b64-aff4-aa1141993694)

# Open the AWS account, search VPC in the search bar and click on VPC

![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fIrk-zLWEb4mepZjY1kiRw.png)

# step1:
 # select the ‘VPC’ and name our project ‘3tier-App’ with a CIDR block of 10.0.0.0/16

![image](https://github.com/user-attachments/assets/91443521-3f9d-4146-b51d-2c0676403c9f)

# step2:
# Create a 2 Public Subnet in your Custom VPC
Enter the subnet details: Name tag: PublicSubnet1. 
VPC: Select the VPC you created. 
Availability Zone: us-east-1a. 
IPv4 CIDR block: Enter 10.0.1.0/24. Click Create subnet.

![image](https://github.com/user-attachments/assets/405d93de-f939-4e70-aef5-d6839c69c574)

# B..Repeat the above steps to create a public subnet2:
Name tag: PublicSubnet2
Availability Zone: Choose a different availability zone (e.g., us-east-1b).
IPv4 CIDR block: Enter 10.0.2.0/24.
![image](https://github.com/user-attachments/assets/c461c26d-ea92-4e46-9b00-5f9c8bd1f133)


# step 3:
# Private Subnets:
Private Subnet 1:
CIDR Block: 10.0.3.0/24
Availability Zone: us-east-1a
Private Subnet 2:
CIDR Block: 10.0.4.0/24
Availability Zone: us-east-1a

![image](https://github.com/user-attachments/assets/c059f2d2-bae5-4c18-a825-cc91c7a3a467)


# STEP4:
# Create an Internet Gateway
Navigate to Internet Gateways under the VPC section.
Click Create internet gateway.
Enter a name tag: (e.g., MyInternetGateway).
Click Create internet gateway.
Attach the Internet Gateway to your VPC:
Select the newly created internet gateway.

![image](https://github.com/user-attachments/assets/9a53eb7b-9a78-4c70-aa60-506b35cc5be5)

# Click Actions and then Attach to VPC.
Choose your VPC and click Attach internet gateway.
![image](https://github.com/user-attachments/assets/e19b64fe-c804-4934-9792-47ad9b608ef9)
![image](https://github.com/user-attachments/assets/eeed7d1f-7ae9-4647-b589-04c6e91f064f)


# step5:
Create the NAT Gateway
Name: MyNATGateway
Create NAT Gateway in Public Subnet 1:
Allocate Elastic IP for the NAT Gateway.
Create the NAT Gateway in Public Subnet 1.

![Screenshot (205)](https://github.com/user-attachments/assets/3448d4aa-3b4f-4c58-bc2b-e600b3439254)


# step5: Create Route Tables
# A.Public Route Table

Navigate to Route Tables under the VPC section.
Click Create route table.
Enter the route table details:
Name tag: PublicRouteTable.
VPC: Select the VPC you created.
Click Create route table

# B.Private Route Table
Click Create route table.
Enter the route table details:
Name tag: PrivateRouteTable.
VPC: Select the VPC you created.
Click Create route table

![image](https://github.com/user-attachments/assets/bbcfc989-799c-40ea-91a7-b08aa2b95c34)

# step6: Associate the  route tables with the subnets:
Click Subnet Associations tab and then Edit subnet associations.
Select the public subnets and click Save associations.

![Screenshot (203)](https://github.com/user-attachments/assets/b5c497c8-fde4-4862-af77-09830348f1f6)

![Screenshot (202)](https://github.com/user-attachments/assets/04c9d1d5-edae-474c-911d-443434842f17)

# after Associate the  route tables with the subnets check the dashbord of route tables

![Screenshot (204)](https://github.com/user-attachments/assets/7b441cf5-6d82-4bbb-9d2a-cfedefe8efd7)


##  Make Auto-assign IP enable because as name suggests it is a Public subnet.
![image](https://github.com/user-attachments/assets/a431f026-89b3-4719-bf65-123a23f71372)

# step7: edit routes in route tables:
Select the Route Table:

Choose the route table you want to edit from the list. Edit Routes for public subnet attach internet gateway and for private nat gateway:

![Screenshot (206)](https://github.com/user-attachments/assets/7d67a844-2b9f-48de-b0c2-11b03d282bb5)
![Screenshot (207)](https://github.com/user-attachments/assets/4768b727-2e25-47c5-bf36-39a7d5389444)
![Screenshot (208)](https://github.com/user-attachments/assets/538da2f4-69a0-424a-ac87-7eff5e2b7edd)


# Tier 1: Web tier (Frontend):
1.A web server launch template to define what kind of EC2 instances will be provisioned for the application.
2.An Auto Scaling Group (ASG) that will dynamically provision EC2 instances.
3.An Application Load Balancer (ALB) to help route incoming traffic to the proper targets.

![image](https://github.com/user-attachments/assets/fd3b739b-a7fc-4604-bc0d-60a5bf91035a)


# Tier 2: Application tier (Backend)

A Bastion host to securely connect to our application servers.
![image](https://github.com/user-attachments/assets/898a921a-03ba-425a-bcc0-55f3be09455b)


# 4. Create a Bastion host

# Tier 3: Database tier (Data storage & retrieval):



