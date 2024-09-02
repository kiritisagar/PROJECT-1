A. Connecting to a private EC2 instance with a terminal via Bastion Host

Creating an EC2 instance in a public subnet as a Bastion Host:
Select “Amazon Linux 2 AMI”,
Instance type “t2.micro”,
Select your custom VPC and public subnet,
Add tag “Name = Bastion_Host”
In the security group section, select My IP as the source for the SSH connection.
Select your key pair and launch your instance.
2. Creating an EC2 instance in a private subnet:

Select “Amazon Linux 2 AMI”,
Instance type “t2.micro”,
Select your custom VPC and private subnet,
Add tag “Name = Private_Instance”
In the security group section, select custom and paste the security group of the public instance (Bastion Host).
Select your key pair and launch your instance.
Edit your “config” file under ~/.ssh/ folder and paste the content below:

vi ~/.ssh/config
Host bastion-host
HostName <Public IP address of Bastion Host>
User ec2-user
Port 22
IdentityFile ~/.ssh/<key pair>
IdentitiesOnly yes
Host private-ec2
HostName <Private IP address of private EC2 instance>
User ec2-user
Port 22
IdentityFile ~/.ssh/<key pair>
IdentitiesOnly yes
ProxyJump bastion-host
We can connect to the private EC2 instance with the following command due to the ProxyJump in the config file:

ssh private-ec2
B. Connecting to a private RDS DB instance with the terminal from Bastion Host:

Creating an EC2 instance in a public subnet as a Bastion Host:
Select “Amazon Linux 2 AMI”,
Instance type “t2.micro”,
Select your custom VPC and public subnet,
Add tag “Name=Public_Instance”
In the security group section, select My IP as the source for the SSH connection.
Select your key pair and launch your instance.
2. Creating a MySQL RDS DB instance in a private subnet:

Master username = “admin”
Master password = “12345678”
DB instance class “db.t2.micro”,
Select your custom VPC,
Public Access = No
Select default VPC security group
Select your RDS DB instance, click the “VPC security groups”, change the inbound rule’s source option to “Custom”, enter the private IP address of the Bastion Host and click “Save rules”.

Open your terminal and run the command below for SSH tunneling:

ssh -i “<key pair>” -N -L 3306:<DB endpoint>:3306 -p 22 ec2-user@<Public IP address or DNS of Bastion Host>

ssh -i "adesso.cer" -N -L 3306:database-1.ccswxi20cprx.us-east-1.RDS.amazonaws.com:3306 -p 22 ec2-user@44.201.66.76
After running this command, open a new terminal and try to connect to the MySQL RDS DB instance with the below command:

mysql -u admin -h 127.0.0.1 -p
Enter the password of the MySQL RDS DB instance and connect to the database.

Another option to connect the MySQL RDS DB instance from a terminal is using the config file. Open ~/.ssh/config file and paste the content below:

vi ~/.ssh/config
Host tunnel-to-RDS
User ec2-user
Port 22
Hostname <Public IP address of Bastion Host>
LocalForward 3306 <DB endpoint>:3306
IdentityFile ~/.ssh/<key pair>
Host tunnel-to-RDS
User ec2-user
Port 22
Hostname 44.201.66.76
LocalForward 3306 database-1.ccswxi20cprx.us-east-1.RDS.amazonaws.com:3306
IdentityFile ~/.ssh/adesso.cer
Open your terminal and run the command below for ssh tunneling:

ssh tunnel-to-RDS
This command will open an SSH tunnel and you can connect the database with the below command:

mysql -u admin -h 127.0.0.1 -p
Enter the password of the MySQL RDS DB instance and connect the database.

C. Connecting to a private RDS DB instance with MySQL Workbench from Bastion Host:

Open your MySQL Workbench and click MySQL New Connection “+” icon.


Enter a name for your connection and select “Standard TCP/IP over SSH” as the Connection Method. Then fill in the fields according to the information below:

SSH Hostname = <Public IP address of Bastion Host>,
SSH Username = ec2-user,
SSH Key File = Select your key file from your local computer,
MySQL Hostname = <DB Endpoint>,
MySQL Server Port = 3306,
Username = admin,
Password = 12345678
Click the “Test Connection” button. You need to see “Successfully made the MySQL connection” on the pop-up window. Choose “OK” for saving connection. Then you can connect your database using an SSH tunnel.


Congrats. You have access to your private resources in the AWS account from your local computer.

Conclusion
Some resources must have limited access to the Internet, especially in terms of security. Therefore, these resources are created in private subnets and do not have Public IPs. If there are no services such as VPN or Direct Connect that allow us to access resources over Private IP, we can generally access these resources through Bastion Hosts. In our article, we have shown several ways how we can access an EC2 instance and RDS created in a private subnet from our local computer through Bastion Host.


