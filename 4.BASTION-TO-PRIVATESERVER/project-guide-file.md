![image](https://github.com/user-attachments/assets/cf94cd22-8ff9-4866-8e09-2a8aa32332b6)

# VPC and components setup
# one VPC.
one (1) public subnets (baston server).
one (1) private subnets (private instance).
One (1) public route table that connects the public subnets to an internet gateway.
One (1) private route table that will connect the Application Tier private subnets and a NAT gateway.
one (1) internet gateway


## setup vpc

Open the AWS account, search VPC in the search bar and click on VPC
![image](https://github.com/user-attachments/assets/9a7ec14c-78af-455e-8c41-1f673ab33cb7)

# step1:
# select the ‘VPC’ and name our project ‘3tier-App’ with a CIDR block of 10.0.0.0/16
![image](https://github.com/user-attachments/assets/0d788af1-a92d-4704-9200-dc5c8985796a)

# Create an Internet Gateway
Navigate to Internet Gateways under the VPC section. Click Create internet gateway. Enter a name tag: (e.g., MyInternetGateway). Click Create internet gateway. Attach the Internet Gateway to your VPC: Select the newly created internet gateway.

![image](https://github.com/user-attachments/assets/ae35b502-4c82-4dd8-92e7-4b2b47d18e19)

# Click Actions and then Attach to VPC.
Choose your VPC and click Attach internet gateway. image image

![image](https://github.com/user-attachments/assets/53b00079-9625-4ca0-99cd-4a7644dd1fef)

![image](https://github.com/user-attachments/assets/87314fe2-69af-44b8-b0ef-7c2fea6c08c5)


# step2:
# Create a 2 Public Subnet in your Custom VPC
Enter the subnet details: Name tag: PublicSubnet1. VPC: Select the VPC you created. Availability Zone: us-east-1a. IPv4 CIDR block: Enter 10.0.1.0/24. Click Create subnet.
![image](https://github.com/user-attachments/assets/7de2b877-733c-43c8-a14a-e623a6520e76)

# Private Subnets:
Private Subnet 1: CIDR Block: 10.0.2.0/24 Availability Zone: us-east-1a Private Subnet 2: CIDR Block: 10.0.4.0/24 Availability Zone: us-east-1a
![image](https://github.com/user-attachments/assets/a2c76b0b-1c83-4c2f-af60-bff3ebb439c8)

# step3
Create Route Tables

# A.Public Route Table
Navigate to Route Tables under the VPC section. Click Create route table. Enter the route table details: Name tag: PublicRouteTable. VPC: Select the VPC you created. Click Create route table

# Private Route Table
Click Create route table. Enter the route table details: Name tag: PrivateRouteTable. VPC: Select the VPC you created. Click Create route table
![image](https://github.com/user-attachments/assets/9a8aab5f-fb8a-46ec-8b44-9d9fd2f5d8fe)

# step4:
Associate the route tables with the subnets:
Click Subnet Associations tab and then Edit subnet associations. Select the public subnets and click Save associations.

![image](https://github.com/user-attachments/assets/a606b301-d0c2-4267-becc-dab6725288e7)
![image](https://github.com/user-attachments/assets/9d4b3206-15b4-4301-8172-f7bee0ce4d96)

# step5: edit routes in route tables:
elect the Route Table:

Choose the route table you want to edit from the list. Edit Routes for public subnet attach internet gateway and for private nat gateway:

![image](https://github.com/user-attachments/assets/939f91db-a059-4c76-a99b-dabfff2a84d2)

![image](https://github.com/user-attachments/assets/49687892-4400-41d5-a4ed-4daf5ef3bdbb)
![image](https://github.com/user-attachments/assets/992632c3-e2b3-4bfd-9765-8d7ab4c7cf8f)


## launch one bastion server with ip enable 
# launch one server in private without ip

# Start the SSH Agent: eval "$(ssh-agent -s)"
Add the SSH Key to the Agent
ssh-add ./jj.pem

 connect to the bastion server by agant forwording
 ssh -A -i "jj.pem" ubuntu@172.16.30.7

 then you connect private server 
 ssh user@privateip
