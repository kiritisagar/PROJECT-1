
# Step 1 — Open the AWS account, search VPC in the search bar and click on VPC

![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fIrk-zLWEb4mepZjY1kiRw.png)

Before creating your own VPC, let's understand about default VPC

By default, when you create a new AWS account, a default VPC (Virtual Private Cloud) is created for you in each AWS region. The default VPC is a logically isolated virtual network within the AWS Cloud that you can use to launch your AWS resources, such as EC2 instances, RDS databases, and more.

The default VPC comes preconfigured with several default settings, including an Internet Gateway and a default subnet in each Availability Zone within the region. This means that you can launch your resources in the default VPC without having to worry about configuring networking settings.


Step 2 — Click on create VPC, select VPC only and enter IPv4.


· A Main Route table will be created automatically but it has only local in the target group.


· Create a Public Subnet in your Custom VPC
What is Public Subnet?

A public subnet is a portion of a computer network that is accessible from the Internet, meaning it has a public IP address that can be reached by anyone on the Internet. In a public subnet, resources like web servers, email servers, and other services that need to be publicly accessible are typically deployed.

Public subnets are often used in cloud computing environments like Amazon Web Services (AWS), where they are paired with a private subnet to create a virtual private cloud (VPC). The private subnet is used to host resources that should not be accessible from the Internet, such as databases, backend servers, and internal applications.


In the above pic, you can see subnets that are created by AWS when default VPC is created.

Step 1 — Click on Create subnet, select your custom VPC, Give a name to the subnet, select Availability zone according to your convince and assign IPV4 CDIR block to this subnet.


Step 2 — Make Auto-assign IP enable because as name suggests it is a Public subnet.


Step 3 — Create an Internet gateway to your Custom VPC

What is an Internet Gateway?

An Internet Gateway (IGW) is a horizontally scaled, redundant, and highly available component in Amazon Web Services (AWS) that allows communication between resources in a VPC and the internet.

An Internet Gateway is a virtual router that connects a VPC to the internet. It provides a target for traffic destined for the public internet from instances in the VPC and a source for traffic originating from the internet and intended for instances in the VPC.

It is an AWS-managed component attached to your VPC and Its acts as a gateway between your VPC & the internet, basically the outside world.


In the above pic, you can see an internet gateway already create which is created by AWS when default VPC is created.

· Click on Create internet gateway, give a name to it and create an internet gateway


· Now, Attach this internet gate to your custom VPC




Step 4 — Add Internet way id to main route table

What is Route table ?

In Amazon Web Services (AWS), the main route table is the default route table that is created when you create a VPC. Every subnet that you create in the VPC is associated with this default route table unless you explicitly associate it with a custom route table.

The main route table contains rules that define how traffic is directed within the VPC. It is used to route traffic between subnets within the VPC and to control access to and from the internet. By default, the main route table has a route that sends all traffic to a local route for communication within the VPC.

You can add, modify or delete the routes in the main route table to control the flow of traffic within your VPC. For example, you can add a route that sends traffic to an Internet Gateway to allow resources in a public subnet to access the internet. You can also add a route that sends traffic to a NAT Gateway to allow resources in a private subnet to access the internet.


Select route table and go to edit routes in that add destination as 0.0.0.0/0 and past your internet gateway id in target and save the changes.


· Create an Ec2 instance in the public subnet of a custom VPC
Give a name to that instance, select instance type, create a key pair, and in the network setting ,select your custom VPC and public subnet it.


This
