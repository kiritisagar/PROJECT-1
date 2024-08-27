# requirements:
1 vpc
2 Public Subnets
1 Internet Gateway
1 Public Route Table

# Open the AWS account, search VPC in the search bar and click on VPC

![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fIrk-zLWEb4mepZjY1kiRw.png)

# step1:
 # Click on create VPC, select VPC only and enter IPv4.

![image](https://github.com/user-attachments/assets/554938be-d729-477e-bf1e-137f12995ee3)

# step2:
# A.. Create a Public Subnet in your Custom VPC
Enter the subnet details:
Name tag: PublicSubnet1.
VPC: Select the VPC you created.
Availability Zone: Choose an availability zone (e.g., us-east-1a).
IPv4 CIDR block: Enter 10.0.1.0/24.
Click Create subnet.

![image](https://github.com/user-attachments/assets/c461c26d-ea92-4e46-9b00-5f9c8bd1f133)

# B..Repeat the above steps to create a public subnet:
Name tag: PublicSubnet2
Availability Zone: Choose a different availability zone (e.g., us-east-1b).
IPv4 CIDR block: Enter 10.0.2.0/24.
![image](https://github.com/user-attachments/assets/c461c26d-ea92-4e46-9b00-5f9c8bd1f133)

# STEP3:
Create an Internet Gateway
Navigate to Internet Gateways under the VPC section.
Click Create internet gateway.
Enter a name tag: (e.g., MyInternetGateway).
Click Create internet gateway.
Attach the Internet Gateway to your VPC:
Select the newly created internet gateway.
Click Actions and then Attach to VPC.
Choose your VPC and click Attach internet gateway.

![image](https://github.com/user-attachments/assets/9a53eb7b-9a78-4c70-aa60-506b35cc5be5)


# step5: Create Route Tables
# Public Route Table

Navigate to Route Tables under the VPC section.
Click Create route table.
Enter the route table details:
Name tag: PublicRouteTable.
VPC: Select the VPC you created.
Click Create route table

# step6: Associate the  route tables with the subnets:
# a.Select the public route table.
Click Subnet Associations tab and then Edit subnet associations.
Select the public subnets and click Save associations.

# step7: edit routes
Select the Route Table:

Choose the route table you want to edit from the list. This should be the one associated with your public subnets.
Edit Routes:

Click on the Routes tab.
Click Edit routes.

Add or Modify Routes
Destination: Enter 0.0.0.0/0 for all IPv4 traffic (or ::/0 for all IPv6 traffic).
Target: Select Internet Gateway and choose the appropriate Internet Gateway (e.g., igw-12345678).


# step 8:
go to ec2 dashboard and select vpc and sub net custum and create static website
