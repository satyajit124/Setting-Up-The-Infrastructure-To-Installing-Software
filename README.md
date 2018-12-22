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
#### Step-1:Create VPC
1. Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.
2. In the navigation pane, choose Your VPCs.then click on **Create VPC**.Specify your VPC Name and CIDR (Classless Inter-Domain Routing), In my case I am using the followings

- VPC Name = MSR-test-VPC
- IPV4 CIDR = 10.0.0.0/16

![screenshot 53 _li](https://user-images.githubusercontent.com/45427666/50373056-075f5b80-05ff-11e9-8e2b-0b9d742a3983.jpg)

Click on **Yes,Create** option
#### Step-2: Create Subnet
In this step we will create two private subnets, MSR-test-Subnet-1 (10.0.1.0/24) and MSR-test-Subnet-2 (10.0.2.0/24) across the availability zones.
1. From the **VPC Dashboard** click on **Subnets** option and then click on **Create Subnet**

Specify the followings
- Subnet name as **MSR-test-Subnet-1**
- VPC **MSR-test-VPC**
- Availability zone as **ap-south-1a**
- IPV4 CIDR **10.0.1.0/24**

![screenshot 54 _li](https://user-images.githubusercontent.com/45427666/50373242-abe29d00-0601-11e9-83c9-80b26bbc7012.jpg)

click on **Yes, Create**

2.  Similarly  Create **MSR-test-Subnet-2** with IPV4 CIDR **10.0.2.0/24** and Availability zone as **ap-south-1b**

![screenshot 55 _li](https://user-images.githubusercontent.com/45427666/50373273-52c73900-0602-11e9-804f-c622e75fffcc.jpg)

click on **Yes, Create**

