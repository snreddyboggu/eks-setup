step1:
create a vpc from console or aws command:  when you lanuch a vpc ,default security group ,nacl,route table will create
command:
------------------------------------------------------------------------------------------------------------------
VPC_ID=$(aws ec2 create-vpc --cidr-block 10.0.0.0/16 --region ap-south-1 --query 'Vpc.VpcId' --output text)
aws ec2 create-tags --resources $VPC_ID --tags Key=Name,Value=Prod-Vpc
--------------------------------------------------------------------------------------------------------------------
aws ec2 modify-vpc-attribute --vpc-id $VPC_ID --enable-dns-support
aws ec2 modify-vpc-attribute --vpc-id $VPC_ID --enable-dns-hostnames

step2:  subnet creation:

Variables (Example Setup)
VPC CIDR: 10.0.0.0/16
Public Subnets:
10.0.1.0/24 (AZ: ap-south-1a)
10.0.2.0/24 (AZ: ap-south-1b)
10.0.3.0/24 (AZ: ap-south-1c)
Private Subnets:
10.0.4.0/24 (AZ: ap-south-1a)
10.0.5.0/24 (AZ: ap-south-1b)
10.0.6.0/24 (AZ: ap-south-1c)

commands:
------------------------------------------------------------------------------------------------------------------------------
PUB_SUBNET1=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 10.0.1.0/24 --availability-zone ap-south-1a --query 'Subnet.SubnetId' --output text)
PUB_SUBNET2=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 10.0.2.0/24 --availability-zone ap-south-1b --query 'Subnet.SubnetId' --output text)
PUB_SUBNET3=$(aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 10.0.3.0/24 --availability-zone ap-south-1c --query 'Subnet.SubnetId' --output text)
------------------------------------------------------------------------------------------------------------------------------------

