# requirements:
1 vpc
2 Public Subnets
1 Internet Gateway
1 Public Route Table

# Open the AWS account, search VPC in the search bar and click on VPC

![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fIrk-zLWEb4mepZjY1kiRw.png)

# step1:
 # elect the ‘VPC and more’ option and name our project ‘3tier-App’ with a CIDR block of 10.0.0.0/16

![image](https://github.com/user-attachments/assets/554938be-d729-477e-bf1e-137f12995ee3)

# step2:
# Create a 2 Public Subnet in your Custom VPC
Enter the subnet details: Name tag: PublicSubnet1. 
VPC: Select the VPC you created. 
Availability Zone: us-east-1a. 
IPv4 CIDR block: Enter 10.0.1.0/24. Click Create subnet.

![image](https://github.com/user-attachments/assets/405d93de-f939-4e70-aef5-d6839c69c574)

# B..Repeat the above steps to create a public subnet:
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
Private Subnet 3:
CIDR Block: 10.0.5.0/24
Availability Zone: us-east-1b
Private Subnet 4:
CIDR Block: 10.0.6.0/24
Availability Zone: us-east-1b

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


# step5: Create Route Tables
# Public Route Table

Navigate to Route Tables under the VPC section.
Click Create route table.
Enter the route table details:
Name tag: PublicRouteTable.
VPC: Select the VPC you created.
Click Create route table

![image](https://github.com/user-attachments/assets/bbcfc989-799c-40ea-91a7-b08aa2b95c34)

# step6: Associate the  route tables with the subnets:
Click Subnet Associations tab and then Edit subnet associations.
Select the public subnets and click Save associations.

##  Make Auto-assign IP enable because as name suggests it is a Public subnet.
![image](https://github.com/user-attachments/assets/a431f026-89b3-4719-bf65-123a23f71372)

# step7: edit routes
Select the Route Table:

Choose the route table you want to edit from the list. This should be the one associated with your public subnets.
Edit Routes:

Click on the Routes tab.
Click Edit routes.

Add or Modify Routes
Destination: Enter 0.0.0.0/0 for all IPv4 traffic (or ::/0 for all IPv6 traffic).
Target: Select Internet Gateway and choose the appropriate Internet Gateway (e.g., igw-12345678).
![image](https://github.com/user-attachments/assets/567e2feb-8600-49a5-ad4b-711c623af1f5)


