# Setting-Up-The-Infrastructure-To-Installing-Software
This is a infrastructure project and install software package using configuration management tool.
## Overview
It is a infrastrucuture project.here we have installed a software by doing a setup for infrastructure.In this infrastrucutre we have created two unbuntu instances and there we have installed 6 types of software packages using shell script tool.For creating ubuntu instance first we created one vpc then we have created two subnet in two different available zones.We have also created internet gateway for communication between vpc and internet.We have created route table for traffic flow with that subnet and internet gateway.Then we have installed one ubuntu 16.04 LTS ec2 instance in each subnet.Then in that instance we have installed software  package using shell script tool.
### Create two EC2 Instances in AWS Cloud using
- Instance Type of both instance is t2.micro .

- Operating System for both instances Ubuntu Server 16.04 LTS.

- Hostname of Instance 1 : MSR-test-Instance-1.

- Hostname of Instance 2 : MSR-test-Instance-2.
### Install Software Package
- NVM – Version 0.33.2

- Node – 8.12.0

- Docker – 18.09

- Docker Compose – 1.17

- Openssl – 1.0.2q

- Git – 2.7.4
## Getting Started
## Configure own VPC(Virtual Private Cloud) in AWS
### Step-1:Create VPC
1. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
2. In the navigation pane, choose Your VPCs.then click on **Create VPC**.Specify your VPC Name and CIDR (Classless Inter-Domain Routing), In my case I am using the followings

- VPC Name = MSR-test-VPC
- IPV4 CIDR = 10.0.0.0/16

![screenshot 53 _li](https://user-images.githubusercontent.com/45427666/50373056-075f5b80-05ff-11e9-8e2b-0b9d742a3983.jpg)

Click on **Create** option
### Step-2: Create Subnet
In this step we will create two private subnets, MSR-test-Subnet-1 (10.0.1.0/24) and MSR-test-Subnet-2 (10.0.2.0/24) across the availability zones.
1. From the **VPC Dashboard** click on **Subnets** option and then click on **Create Subnet**

Specify the followings
- Subnet name as **MSR-test-Subnet-1**
- VPC **MSR-test-VPC**
- Availability zone as **ap-south-1a**
- IPV4 CIDR **10.0.1.0/24**

![screenshot 54 _li](https://user-images.githubusercontent.com/45427666/50373242-abe29d00-0601-11e9-83c9-80b26bbc7012.jpg)

click on **Create**

2.  Similarly  Create **MSR-test-Subnet-2** with IPV4 CIDR **10.0.2.0/24** and Availability zone as **ap-south-1b**

![screenshot 55 _li](https://user-images.githubusercontent.com/45427666/50373273-52c73900-0602-11e9-804f-c622e75fffcc.jpg)

click on **Create**

 ### step-3: Create a Route table and associate it with Subnet
 1. From **VPC Dashboard**  there is an option create a Route table. Click on **Create Route Table**,Specify the Name of Route Table **MSR-test-RT** and Select your VPC, In my case VPC is **MSR-test-VPC**
 
 ![screenshot 58 _li](https://user-images.githubusercontent.com/45427666/50373360-ef3e0b00-0603-11e9-949c-d8a56c3fa852.jpg)

click on **Create**

2. Once the Route table is created, associated it with Subnet, Select and Right Click Your Route table and then  Select the **Subnet Associations** option, Then choose both the subnets.

![screenshot 60 _li](https://user-images.githubusercontent.com/45427666/50373556-d8e57e80-0606-11e9-91dd-42e0d00c70d3.jpg)

click on **Save**

### step-4: Create Internet Gateway (igw) and attached it to your VPC
1. From **VPC dashboard** there is an option to create Internet gateway. Click on **Create Internet gateway**,Specify the Name of Internet gateway **MSR-test-IGW**

![screenshot 56 _li](https://user-images.githubusercontent.com/45427666/50373413-1517df80-0605-11e9-82ec-adaa26d5daf4.jpg)

click on **Create**

2. Once the Internet gateway is created, attached it to your VPC, Select and Right Click Your Internet gateway and then  Select the **Attach to VPC** option

![screenshot 57 _li](https://user-images.githubusercontent.com/45427666/50373450-6e800e80-0605-11e9-8408-076a612ab444.jpg)

click on **Attach**

3. Now Add Route to your route Table for Internet, go to **Route Tables**  Option, Select your Route Table, In my case it is **MSR-test-RT**, click on Route Tab and Click on **Edit** and  the click on **add another route**

Mention Destination IP of Internet as **0.0.0.0/0** and in the target option your Internet gateway will be populated automatically as shown below

![screenshot 59 _li](https://user-images.githubusercontent.com/45427666/50373607-a9834180-0607-11e9-835a-895dd95f13b4.jpg)

click on **Save routes**

## Launch EC2 instances using VPC
### Launch MSR-test-Instance-1 Using Ubuntu Server 16.04 LTS
1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. Choose **Launch Instance**.

3. In **Step 1: Choose an Amazon Machine Image (AMI)**, find an **Ubuntu Server 16.04 LTS** and choose **Select**.

![screenshot 61 _li](https://user-images.githubusercontent.com/45427666/50373925-c752a580-060b-11e9-962a-89973c1259fc.jpg)

4. In **Step 2: Choose an Instance Type**, Select **t2.micro** for free tier.choose **Next: Configure Instance Details**.

![screenshot 62 _li](https://user-images.githubusercontent.com/45427666/50373953-316b4a80-060c-11e9-87cd-e61574a5f119.jpg)

choose **Next: Configure Instance Details**

5.


