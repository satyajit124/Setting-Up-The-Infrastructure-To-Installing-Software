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

5. In **Step 3: Configure Instance Details**
- choose **Network**, then choose your vpc,In my case VPC is **MSR-test-VPC**
- Choose **Subnet**, then choose a subnet, In my case subnet is **MSR-test-Subnet-1**.
- choose **Auto-assign Public IP**, then choose **Enable** 
- (**Optional**) In **Advanced details**,choose **User Data** and paste here **shell Script** file.(This file available on the above README.md).Here **shell script** used only for installing above software package automatically.

![screenshot 63 _li](https://user-images.githubusercontent.com/45427666/50374220-cf611400-0610-11e9-943f-d3e295f64541.jpg)

Choose **Next: Add Storage** 

6. In **Step 4: Add Storage**
 
 ![screenshot 65 _li](https://user-images.githubusercontent.com/45427666/50374265-64fca380-0611-11e9-91f1-7d452c63fc26.jpg)

Choose **Next: Add Tag**

7. In **Step 5: Add Tag ** Here we have tagged the instance Name as a **MSR-test-Instance-1**.

![screenshot 64 _li](https://user-images.githubusercontent.com/45427666/50374294-03890480-0612-11e9-851c-554368352139.jpg)

Choose **Next: Configure Security Group**

8. In **Step 6: Configure Security Group**, review the contents of this page, ensure that **Assign a security group** is set to **Create a new security group**, and verify that the inbound rule being created has the following default values.
- **Type:** SSH
- **Protocol:** TCP
- **Port Range:** 22
- **Source:** Anywhere 0.0.0.0/0

![gs-review-security-group-600w](https://user-images.githubusercontent.com/45427666/50374407-c7ef3a00-0613-11e9-8f9f-68983ffb5e4d.png)

Choose **Review and Launch**

9. Choose **Launch**

10. Select the check box for the key pair that you created, and then choose **Launch Instances**.

12. Choose **View Instances**

### Connect Ubuntu Instance
1. Come back to your instances screen, you'll see that instance has received **Public IP**.

2. Now open putty from your programs list and add same **Public IP** in Host Name.

![screenshot 70](https://user-images.githubusercontent.com/45427666/50375166-10f8bb80-061f-11e9-9ca1-774cdbf4a30e.png)

3. In this step,

Add your private key in putty for secure connection.

Go to **Auth**
Add your private key in **.ppk** (putty private key) format. You will need to convert pem file from AWS to ppk using puttygen
Once done click on **Open** button.

![screenshot 71](https://user-images.githubusercontent.com/45427666/50375190-70ef6200-061f-11e9-9080-135c3dae1a8e.png)

Once you **connect**, you will successfully see the **ubuntu** prompt.

### Launch MSR-test-Instance-2 Using Ubuntu Server 16.04 LTS
Similarly,Launch **MSR-test-Instance-2** as the same step, 

1. Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

2. Choose **Launch Instance**.

3. In **Step 1: Choose an Amazon Machine Image (AMI)**, find an **Ubuntu Server 16.04 LTS** and choose **Select**.

![screenshot 61 _li](https://user-images.githubusercontent.com/45427666/50373925-c752a580-060b-11e9-962a-89973c1259fc.jpg)

4. In **Step 2: Choose an Instance Type**, Select **t2.micro** for free tier.choose **Next: Configure Instance Details**.

![screenshot 62 _li](https://user-images.githubusercontent.com/45427666/50373953-316b4a80-060c-11e9-87cd-e61574a5f119.jpg)

choose **Next: Configure Instance Details**

5. In **Step 3: Configure Instance Details**
- choose **Network**, then choose your vpc,In my case VPC is **MSR-test-VPC**
- Choose **Subnet**, then choose a subnet, In my case subnet is **MSR-test-Subnet-2**.
- choose **Auto-assign Public IP**, then choose **Enable** 
- (**Optional**) In **Advanced details**,choose **User Data** and paste here **shell Script** file.(This file available on the above README.md).Here **shell script** used only for installing above software package automatically.

![screenshot 63 _li](https://user-images.githubusercontent.com/45427666/50374220-cf611400-0610-11e9-943f-d3e295f64541.jpg)

Choose **Next: Add Storage** 

6. In **Step 4: Add Storage**
 
 ![screenshot 65 _li](https://user-images.githubusercontent.com/45427666/50374265-64fca380-0611-11e9-91f1-7d452c63fc26.jpg)

Choose **Next: Add Tag**

7. In **Step 5: Add Tag** Here we have tagged the instance Name as a **MSR-test-Instance-2**.

![screenshot 66 _li](https://user-images.githubusercontent.com/45427666/50375468-c299eb80-0623-11e9-8440-5a34c36340c5.jpg)

Choose **Next: Configure Security Group**

8. In **Step 6: Configure Security Group**, review the contents of this page, ensure that **Assign a security group** is set to **Create a new security group**, and verify that the inbound rule being created has the following default values.
- **Type:** SSH
- **Protocol:** TCP
- **Port Range:** 22
- **Source:** Anywhere 0.0.0.0/0

![gs-review-security-group-600w](https://user-images.githubusercontent.com/45427666/50374407-c7ef3a00-0613-11e9-8f9f-68983ffb5e4d.png)

Choose **Review and Launch**

9. Choose **Launch**

10. Select the check box for the key pair that you created, and then choose **Launch Instances**.

12. Choose **View Instances**

### Connect Ubuntu Instance
1. Come back to your instances screen, you'll see that instance has received **Public IP**.

2. Now open putty from your programs list and add same **Public IP** in Host Name.

![screenshot 70](https://user-images.githubusercontent.com/45427666/50375166-10f8bb80-061f-11e9-9ca1-774cdbf4a30e.png)

3. In this step,

Add your private key in putty for secure connection.

Go to **Auth**
Add your private key in **.ppk** (putty private key) format. You will need to convert pem file from AWS to ppk using puttygen
Once done click on **Open** button.

![screenshot 71](https://user-images.githubusercontent.com/45427666/50375190-70ef6200-061f-11e9-9080-135c3dae1a8e.png)

Once you **connect**, you will successfully see the **ubuntu** prompt.





### Verify the Software Package Installation
Now,We check Both the **ubuntu** instance our software package install or not,

1. We can quickly verify that NVM is now installed and working properly with the following command:
```shell
nvm --version
```
2. We can quickly verify that Node is now installed and working properly with the following command:
```shell
node -v
```

3. We can quickly verify that Docker is now installed and working properly with the following command:
```shell
docker --version
```

4. We can quickly verify that Docker-Compose is now installed and working properly with the following command:
```shell
docker-compose --version
```

5. We can quickly verify that Openssl is now installed and working properly with the following command:
```shell
openssl version
```

4. We can quickly verify that Git is now installed and working properly with the following command:
```shell
git --version
```

**Verify Result MSR-test-instance-1**

![screenshot 69](https://user-images.githubusercontent.com/45427666/50375595-dcd4c900-0625-11e9-987b-43505d0a5600.png)

**Verify Result MSR-test-instance-1**

![screenshot 68](https://user-images.githubusercontent.com/45427666/50375605-13124880-0626-11e9-82f7-c2c7eca5cd49.png)


## Manually Software Package Install 
### NVM – Version 0.33.2 Installation

**Step #1: Install a C++ Compiler**
1. update our packages:
```shell
apt-get update
```
2. build-essential package installation
```shell
apt-get install build-essential libssl-dev
```
**Install NVM (Node Version Manager)**
Use the following curl command to kick-off the install script:
```shell
curl https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```
After installation,run the following command:
```shell
source ~/.profile
```
**Verify the Installation**
```shell
nvm --version
```

### Node – 8.12.0 Installation
 **Add Node.js PPA**
 ```shell
 sudo apt-get install curl python-software-properties
 ```
 ```shell
 curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
 ```
**Install Node.js on Ubuntu**
```shell
sudo apt-get install nodejs
```
**Test Node.js**
- After installing node.js verify and check the installed version
```shell
node -v
```

### Docker – 18.09 Installation
1. Install few **pre-requisite** packages by using the below command, if not installed.
```shell
apt-get install apt-transport-https ca-certificates curl software-properties-common
```
2. **Docker** package is available in the official ubuntu 16.04 itself, but in order to install the latest docker, we will use the official docker repository. Lets first add the GPG key of the official docker repository so that we can fetch the package from there.
```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
3. Add the docker repository to the apt source.
```shell
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
4. Lets update the repository from the added docker repository
```shell
apt-get update
```
5. To make sure that the  docker is installed from the docker repository, not from the local ubuntu 16.04 repository, lets cache it by using below command
```shell
apt-cache policy docker-ce
```
6. Now we are all set to install docker
```shell
apt-get install docker-ce -y
```
7. Check whether the docker service is running or not.
```shell
systemctl status docker.service
```
8. If the Docker Service is not running, make sure to start it
```shell
systemctl start docker.service
```
9. Verify it by checking its version.
```shell
docker -version
```
### Docker Compose – 1.17 Installation

1. Run this command to download the latest version of Docker Compose:
```shell
 curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
 ```
 2. Apply executable permissions to the binary:
 ```shell
 chmod +x /usr/local/bin/docker-compose
 ```
 3.Test the installation.
 ```shell
 docker-compose --version
 ```
 
 ### Openssl – 1.0.2q Installation
 1. Before starting the installation of **OpenSSL**, get the current version of OpenSSL by using the following command.
```shell
openssl version
```
2. After that, download the latest version of **OpenSSL** by deploying the following command.
```shell
cd /usr/src
```
```shell
wget https://www.openssl.org/source/openssl-1.0.2-latest.tar.gz
```
3. Once it is downloaded, extract the downloaded **OpenSSL** tar file as follows.
```shell
tar -zxf openssl-1.0.2-latest.tar.gz
```
4. To manually compile OpenSSL and install/upgrade OpenSSL, make use of the following command.
```shell
cd openssl-1.0.2q
```
```shell
./config 
```
5. After it is done, prepare the installation of OpenSSL by runninng the make command.
```shell
make
```
6. After it, run the make test command as follows.
```shell
make test
```
7. Once the command is executed, run the make install command which triggers the installation process.
```shell
make install
```
8. If the old version is still displayed or installed before, please make a copy of openssl bin file.
```shell
mv /usr/bin/openssl /root/
```
```shell
ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl
```
9. Now verify the OpenSSL version.
```shell
openssl version
```

### Git – 2.7.4 Installation (Latest)
1. For package updates
```shell
apt-get update
```
2.Install **Git**
```shell
apt-get install git-core
```
3. Confirm Git the **installation**
```shell
git --version
```





    


