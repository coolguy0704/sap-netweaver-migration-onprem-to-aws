# SAP NetWeaver Migration from On-Prem (simulated) to AWS

This repository provides the necessary resources and documentation for migrating a simulated deployment of SAP NetWeaver on AWS to a different AWS environment.

## Overview

The migration process involves the following high-level steps:

1. Launch an EC2 instance and install SAP NetWeaver on it.
2. Create a simulation as in on-prem, the SAP NetWeaver deployment in the AWS environment.
3. Convert the EC2 instance into an OVA file and store it in Amazon S3.
4. Create an Amazon Machine Image (AMI) and EBS snapshot.
5. Launch a new EC2 instance from the AMI and EBS snapshot in the new AWS environment.

## Prerequisites

Before you can begin the migration process, you will need to have the following:

- An AWS account with sufficient privileges to create and manage the necessary resources.
- Access to the AWS Management Console and AWS CLI.
- Familiarity with AWS services and concepts such as EC2, S3, and VPC.

## Migration Process

### Step 1,2: Launch an EC2 instance and install SAP NetWeaver on it

Launch an EC2 instance in the AWS environment and install SAP NetWeaver on it. Ensure that the instance is properly configured and that SAP NetWeaver is running correctly.
<img width="891" alt="Snipaste_2023-03-22_22-03-37_1" src="https://user-images.githubusercontent.com/116753469/226990388-5b6efaee-7709-4275-8725-18a54bfef55e.png">

<img width="730" alt="Snipaste_2023-03-22_22-07-22" src="https://user-images.githubusercontent.com/116753469/226989804-964111b6-2b1a-40d4-93eb-3ed12f8b78fe.png">
<img width="438" alt="Snipaste_2023-03-22_22-10-07" src="https://user-images.githubusercontent.com/116753469/226989807-65ce330c-d258-4552-8400-09a3019adcfc.png">

Now, let's install the necessary packages require for the SAP:
```
sudo apt-get install libaio1
sudo apt-get install csh
sudo apt install libc6
sudo apt-get install uuid
sudo service uuidd start
sudo update-locale LANG=”en_US.UTF-8"
```

For setting up VNC:
```
sudo apt update && sudo apt upgrade
sudo sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
sudo /etc/init.d/ssh restart
sudo passwd ubuntu
sudo apt install xrdp xfce4 xfce4-goodies tightvncserver
echo xfce4-session> /home/ubuntu/.xsession
sudo cp /home/ubuntu/.xsession /etc/skel
sudo sed -i '0,/-1/s//ask-1/' /etc/xrdp/xrdp.ini
sudo service xrdp restart
tightvncserver
```

For downloading the SAP netweaver let's install firefox:
```
sudo add-apt-repository ppa:ubuntu-mozilla-security/ppa
sudo apt-get update
sudo apt-get install firefox
```

<img width="971" alt="Snipaste_2023-03-22_22-12-43" src="https://user-images.githubusercontent.com/116753469/226989811-7f6426ac-9cd9-4665-aba9-bfab87eea4c8.png">
<img width="521" alt="Snipaste_2023-03-22_22-13-54" src="https://user-images.githubusercontent.com/116753469/226989817-3364f1ac-a951-4171-b0c9-1501b3585272.png">
<img width="1439" alt="Snipaste_2023-03-22_22-33-32" src="https://user-images.githubusercontent.com/116753469/226989822-82439067-e569-4e12-85b8-79b9cef7e505.png">
<img width="486" alt="Snipaste_2023-03-22_22-33-58" src="https://user-images.githubusercontent.com/116753469/226989825-8c79c419-cb99-48f8-bab7-8f0bdfc71c74.png">
<img width="1004" alt="Snipaste_2023-03-22_22-36-44" src="https://user-images.githubusercontent.com/116753469/226989826-a46a8739-bc13-437b-bb24-5593283ea1b6.png">
<img width="1004" alt="Snipaste_2023-03-22_22-37-53" src="https://user-images.githubusercontent.com/116753469/226989832-aad551a6-14be-47ca-89ac-84228ca7818c.png">
<img width="1004" alt="Snipaste_2023-03-22_22-41-20" src="https://user-images.githubusercontent.com/116753469/226989844-4291705a-c8f0-4797-8951-8f3ac24b54ef.png">
<img width="1439" alt="Snipaste_2023-03-22_23-12-28" src="https://user-images.githubusercontent.com/116753469/226989846-3ff75a43-3d41-4202-b653-9126f260e564.png">

Now let's edit system configuration needed for SAP:
```
Update Hostname
sudo vim /etc/hostname

Check the IP Address
sudo ip addr show
sudo vim /etc/hosts
sudo cat /etc/hosts


Check Hosts and Hostname
sudo cat /etc/hosts
sudo cat /etc/hostname

Restart System after changes and validate the changes
sudo reboot
```
<img width="750" alt="Snipaste_2023-03-22_23-25-10" src="https://user-images.githubusercontent.com/116753469/226989856-a50edff2-9548-49a6-961d-26d9db376ab4.png">
<img width="1017" alt="Snipaste_2023-03-22_23-26-11" src="https://user-images.githubusercontent.com/116753469/226989859-4eb2e3ce-fa1c-4871-90df-001c8d3857aa.png">
<img width="510" alt="Snipaste_2023-03-22_23-26-32" src="https://user-images.githubusercontent.com/116753469/226989862-7a5c4d97-5913-43c5-8a34-7c55e9d1bb24.png">
<img width="420" alt="Snipaste_2023-03-22_23-31-02" src="https://user-images.githubusercontent.com/116753469/226989865-c2807310-07b4-4f09-9546-d464450b9780.png">
<img width="693" alt="Snipaste_2023-03-22_23-36-22" src="https://user-images.githubusercontent.com/116753469/226989868-3baddaac-117c-4516-aa1a-3088030e5026.png">
<img width="541" alt="Snipaste_2023-03-22_23-39-54" src="https://user-images.githubusercontent.com/116753469/226989870-8c455c5e-1602-4338-9386-6d424e19cede.png">
<img width="1190" alt="Snipaste_2023-03-22_23-47-08" src="https://user-images.githubusercontent.com/116753469/226989873-bec0a957-4196-459c-b7f3-19e34aa0d5aa.png">
<img width="840" alt="Snipaste_2023-03-22_23-56-19" src="https://user-images.githubusercontent.com/116753469/226989875-be08c515-1fc8-4d19-b2d3-b479c2f90bfe.png">
<img width="1437" alt="Snipaste_2023-03-23_01-25-24" src="https://user-images.githubusercontent.com/116753469/226989878-6d6408e7-496f-4719-a353-78b5ee7f016b.png">

Now the installation of netWeaver is completed, let's install SAP frontend GUI to access the netweaver.

<img width="589" alt="Snipaste_2023-03-23_10-43-29" src="https://user-images.githubusercontent.com/116753469/227099695-dee58325-2a04-4811-ba94-0e3dc5cb5720.png">

Let's add a new connection
<img width="363" alt="Snipaste_2023-03-23_10-44-40" src="https://user-images.githubusercontent.com/116753469/227099829-d3c68c8d-583a-4d34-98ee-0407d62647a9.png">

Give the connection a name, and add the public ip address assigned to the SAP and save it.

<img width="404" alt="Snipaste_2023-03-23_10-47-53" src="https://user-images.githubusercontent.com/116753469/227099874-dda82ae1-e7df-42a5-bd81-f9c341963e74.png">

Now add the credentials, generally if it is developer ABAP SPO2 7.52 version, the default details are
Client: 001
username: SAP*
password: Appl1ance

<img width="633" alt="Snipaste_2023-03-23_10-48-42" src="https://user-images.githubusercontent.com/116753469/227101634-5b325494-e593-47e0-8cb9-bf52f39d2b20.png">

Now, let's add a user, type SU01 in the searchbox, Select create user
<img width="960" alt="Snipaste_2023-03-23_11-05-28" src="https://user-images.githubusercontent.com/116753469/227101764-b5e39e29-d2cc-4333-9bbd-c51b2f4e4a82.png">

<img width="453" alt="Snipaste_2023-03-23_11-09-12" src="https://user-images.githubusercontent.com/116753469/227101850-58936c4d-f1aa-4eae-8aba-615879414ef9.png">
<img width="960" alt="Snipaste_2023-03-23_11-12-34" src="https://user-images.githubusercontent.com/116753469/227101939-2eec86df-a603-4b57-85bf-ea8119bce67b.png">

<img width="960" alt="Snipaste_2023-03-23_11-15-23" src="https://user-images.githubusercontent.com/116753469/227101950-a71af954-0520-4105-94d0-dbcfbded7b9b.png">
<img width="960" alt="Snipaste_2023-03-23_11-16-48" src="https://user-images.githubusercontent.com/116753469/227101983-5aeab76f-472e-4b99-9a91-61f2eab3ffc1.png">
<img width="960" alt="Snipaste_2023-03-23_11-17-56" src="https://user-images.githubusercontent.com/116753469/227102018-1c12def2-00c0-46d4-8137-0c6858e08a6f.png">

Now the user is created.
<img width="960" alt="Snipaste_2023-03-23_11-18-20" src="https://user-images.githubusercontent.com/116753469/227102050-7f5c17e7-af27-40c1-a87e-e123b657ec8f.png">
we'll use this created user to login to SAP now
<img width="815" alt="Snipaste_2023-03-23_11-19-39" src="https://user-images.githubusercontent.com/116753469/227102173-5fdde8b7-ba3a-40af-bfc7-7d2bd364cda6.png">
<img width="686" alt="Snipaste_2023-03-23_11-20-01" src="https://user-images.githubusercontent.com/116753469/227102239-9614e649-12ca-438a-bf98-c1d099def97a.png">
Now we're logged in as created user.
<img width="960" alt="Snipaste_2023-03-23_11-20-31" src="https://user-images.githubusercontent.com/116753469/227102335-c8ffd253-fe13-4238-9f42-afeac41c34f9.png">


### Step 3: Convert the EC2 instance into an OVA file and store it in Amazon S3

Use the AWS CLI to convert the EC2 instance into an OVA file and store it in Amazon S3. Ensure that the OVA file is stored in a secure and accessible location. 

for this step if we want to convert manually to let's say to VMware platform we can use below cli to convert format and export it.
https://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html

But in my case to make it easier, I am just creating image from the current VM in next step utilizing AWS automation to reduce manual overhead.


### Step 4: Create an Amazon Machine Image (AMI) and EBS snapshot
Ensure that the AMI and EBS snapshot are properly configured and tagged for easy identification.

<img width="1196" alt="Snipaste_2023-03-23_11-49-32" src="https://user-images.githubusercontent.com/116753469/227102780-b4fd2b8d-8752-4858-8bfb-94f9e010446e.png">
<img width="1383" alt="Snipaste_2023-03-23_12-03-50" src="https://user-images.githubusercontent.com/116753469/227103152-a47a3848-5be3-4207-b6de-6b8cf698025f.png">

Wait until the AMI becomes available, it will take a while.
<img width="1194" alt="Snipaste_2023-03-23_11-50-57" src="https://user-images.githubusercontent.com/116753469/227103057-09a571d7-2e02-4cf9-9a34-b9e660e8bb32.png">
<img width="1200" alt="Snipaste_2023-03-23_12-39-10" src="https://user-images.githubusercontent.com/116753469/227103166-dc9b6509-bdd6-4d03-92b6-3ec18cd224d2.png">



### Step 5: Launch a new EC2 instance from the AMI and EBS snapshot in the new AWS environment

Now, let's Launch a new EC2 instance from the AMI and EBS snapshot in the new AWS environment with same config as previous instance. 

<img width="989" alt="Snipaste_2023-03-23_12-40-12" src="https://user-images.githubusercontent.com/116753469/227103374-ed5c29ba-26d5-40f6-9c0b-3463fea70976.png">
wait until it comes to active status
<img width="1185" alt="Snipaste_2023-03-23_12-40-43" src="https://user-images.githubusercontent.com/116753469/227103457-d0d02de3-5723-4f86-8df7-273a4a2e17c9.png">
<img width="1191" alt="Snipaste_2023-03-23_12-40-57" src="https://user-images.githubusercontent.com/116753469/227103471-de5d175d-e355-44a1-8b59-fd98f8f8bcc8.png">

Now note down the new public ip of the migrated instance
<img width="1186" alt="Snipaste_2023-03-23_12-42-07" src="https://user-images.githubusercontent.com/116753469/227103569-4dd8ba29-47c0-4180-bbe2-e73ae3d1af0c.png">
Now let's create a new connection to the new instance with the noted ip address.
<img width="400" alt="Snipaste_2023-03-23_12-44-43" src="https://user-images.githubusercontent.com/116753469/227103729-78ba223f-912a-4f66-aeeb-47c4a4f03905.png">

Now instead of default login credentials, let's use the user and it's credentials we created to check if the migrated VM is same as the previous VM.

<img width="799" alt="Snipaste_2023-03-23_12-53-00" src="https://user-images.githubusercontent.com/116753469/227103875-ad941a1e-9eb1-4d3b-afdd-f0a77ddc2205.png">
<img width="892" alt="Snipaste_2023-03-23_12-54-05" src="https://user-images.githubusercontent.com/116753469/227103905-69b5cf05-a9b3-4220-936d-c101cecd423e.png">

Now we Ensured that the instance is properly configured and that SAP NetWeaver is running correctly.


### Step 6: Cleanup

Now to reduce any further costs, delete the EC2 instances launched, deregister AMI and delete the snapshot.
