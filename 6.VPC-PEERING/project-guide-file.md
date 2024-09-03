
![image](https://github.com/user-attachments/assets/4f4c9fd9-7ba6-471d-9feb-1469a232421e)



# Setting up VPC Peering in AWS:
Task 1: Create two Custom VPCs in your AWS account within the same region

1. Create the first Custom VPC

Name = custom-vpc-01

CIDR block = 10.1.0.0/16

Tenancy = Default

IPV6 CIDR Block = Select “No IPV6 CIDR Block”

2. Create a public subnet for custom-vpc-01

Name = vpc-01-pub-subnet

VPC = custom-vpc-01

Availability Zone = <Select an AZ>

CIDR block = 10.1.1.0/24

3. Create the second Custom VPC (custom-vpc-02) with following parameters

CIDR block = 10.2.0.0/16

Tenancy = Default

IPV6 CIDR Block = Select “No IPV6 CIDR Block”

Make the subnet public by modifying the auto-assign IP settings

4. Create a public subnet for custom-vpc-02

Name = vpc-02-pub-subnet

VPC = custom-vpc-02

Availability Zone = <Select an AZ>

CIDR block = 10.2.1.0/24

Make the subnet public by modifying the auto-assign IP settings

5. Create two Internet Gateways and attach them to created VPCs respectively.

IGW for vpc-01-pub-subnet = custom-vpc-01-igw

IGW for vpc-02-pub-subnet = custom-vpc-02-igw

6. Add Route entries (0.0.0.0/0 for IGWs) to two Route Tables.

7. Create two EC2 instances in each public subnets in each custom VPCs. SSH into both the public subnets (in both VPCs) and see whether each EC2 instance have the access to the Internet. If they have you have successfully created both the VPCs with two public subnets with two EC2 instances.

8. Using Bastian hosts try to SSH into from custom-vpc-01 to custom-vpc-02 using the VPC2 private IP address. You can see you are not able to do it mainly because theoretically two VPCs cannot communicate with each other unless you have VPC Peering Connection.

Task 2: Create a VPC Peering Connection

1. Go to VPC → Peering Connections

2. Click “Create Peering Connection”

3. Select the following parameters

Peering connection name tag = peering-con

VPC (Requester) = custom-vpc-01

Select My Account and the Same Region

VPC (Accepter) = custom-vpc-02

4. After creating the Peering Connection you can see the status of the connection as “Pending Acceptance”

In order to confirm this you are required to select “Actions” → “Accept Request”.

5. Add two Routing Entries to both the Route Tables of each VPC

For custom-vpc-01, add the following entry

Destination = 10.2.0.0/16

Target = <Select the Peering Connection>


custom-vpc-01 routing entries

For custom-vpc-02, add the following entry

Destination = 10.1.0.0/16

Target = <Select the Peering Connection>


custom-vpc-02 routing entries

6. Finally, SSH into custom-vpc-01 EC2 instance and try to SSH to custom-vpc-02 and see whether you are able to do it. If you can, you have done the VPC Peering successfully!. Well done!

Multiple VPC peering connections
A VPC peering connection is a one to one relationship between two VPCs. You can create multiple VPC
peering connections for each VPC that you own, but transitive peering relationships are not supported.
You do not have any peering relationship with VPCs that your VPC is not directly peered with.
The following diagram is an example of one VPC peered to two diﬀerent VPCs. There are two VPC
peering connections: VPC A is peered with both VPC B and VPC C. VPC B and VPC C are not peered, and
you cannot use VPC A as a transit point for peering between VPC B and VPC C. If you want to enable
routing of traﬃc between VPC B and VPC C, you must create a unique VPC peering connection between
them.


VPC Peering Rules & Limitations

VPC peering connection cannot be created between VPCs that have matching or overlapping CIDR blocks.


(NOTE — VPC Peering is now supported inter-region.)

VPC peering connection are limited on the number active and pending VPC peering connections that you can have per VPC.


VPC peering does not support transitive peering relationships. In a VPC peering connection, the VPC does not have access to any other VPCs that the peer VPC may be peered with even if established entirely within your own AWS account.


