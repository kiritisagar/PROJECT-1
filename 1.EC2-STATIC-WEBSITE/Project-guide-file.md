# Step1 : Launch an EC2 Instance
Search for “EC2” in the AWS Management Console and select it.
Click “Launch Instance.”
Give your EC2 instance a name.
Choose Amazon Linux 2 as the Amazon Machine Image.
Select t2.micro as the instance type.
Create a new key pair and choose the .pem format.
Select your key pair and the security group you created.
Launch the instance and wait for it to pass the status check.

![image](https://github.com/user-attachments/assets/acd049b6-4941-4c30-82b0-5e4fe30c5bc9)

# step2:
connect to the instance && update
![image](https://github.com/user-attachments/assets/c2fe75c1-1d02-4058-bd8a-4e1d36ad7e13)

![Screenshot (197)](https://github.com/user-attachments/assets/8ad989e2-e4b6-4e25-bf0a-07b707ae8672)


# Step 3: Install Required Software

-- Install the Apache service:
sudo apt-get install apache2 -y

# -- check status of apace2
![Screenshot (198)](https://github.com/user-attachments/assets/d765b165-90a4-4db1-a5a8-1fcad8170a2b)

# if require 
         -systemctl enable apache2
         -systemctl start apache2


# step4:
Add a rule for SSH (port 22) with the source set to “My IP” for added security.
Under Inbound rules, add a rule for HTTP (port 80) with the source set to “anywhere IPv4.”

![image](https://github.com/user-attachments/assets/8315c797-6de3-4a16-a684-7d007222d4c0)

# step5:
Access Your default page
![image](https://github.com/user-attachments/assets/b56f2ef3-da43-4aa0-8958-15ef1b7cba6f)

