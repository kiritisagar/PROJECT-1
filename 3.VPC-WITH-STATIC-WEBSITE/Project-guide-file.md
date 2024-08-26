
# Step 1 — Open the AWS account, search VPC in the search bar and click on VPC

![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*fIrk-zLWEb4mepZjY1kiRw.png)

# Step 2 — Click on create VPC, select VPC only and enter IPv4.

![image](https://github.com/user-attachments/assets/554938be-d729-477e-bf1e-137f12995ee3)

· A Main Route table will be created automatically but it has only local in the target group.
![image](https://github.com/user-attachments/assets/821c91fe-afb7-42ac-a2f4-6cbdabd87938)


A.. Create a Public Subnet in your Custom VPC

--  Click on Create subnet, select your custom VPC, Give a name to the subnet, select Availability zone according to your convince and assign IPV4 CDIR block to this subnet.

![image](https://github.com/user-attachments/assets/c461c26d-ea92-4e46-9b00-5f9c8bd1f133)

Step 2 — Make Auto-assign IP enable because as name suggests it is a Public subnet.
![image](https://github.com/user-attachments/assets/ec499caa-935c-425a-8b24-93e86f2663d2)


Step 3 — Create an Internet gateway to your Custom VPC
![image](https://github.com/user-attachments/assets/9a53eb7b-9a78-4c70-aa60-506b35cc5be5)
· Click on Create internet gateway, give a name to it and create an internet gateway



· Now, Attach this internet gate to your custom VPC




Step 4 — Add Internet way id to main route table


Select route table and go to edit routes in that add destination as 0.0.0.0/0 and past your internet gateway id in target and save the changes.


· Create an Ec2 instance in the public subnet of a custom VPC
Give a name to that instance, select instance type, create a key pair, and in the network setting ,select your custom VPC and public subnet it.


