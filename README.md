# SAP NetWeaver Migration from On-Prem (simulated) to AWS

This repository provides the necessary resources and documentation for migrating a simulated deployment of SAP NetWeaver on AWS to a different AWS environment.

## Overview

The migration process involves the following high-level steps:

1. Launch an EC2 instance and install SAP NetWeaver on it.
2. Create a simulation as in on-prem, the SAP NetWeaver deployment in the AWS environment.
3. Convert the EC2 instance into an OVA file and store it in Amazon S3.
4. Create an Amazon Machine Image (AMI) and EBS snapshot from the OVA file.
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
<img width="971" alt="Snipaste_2023-03-22_22-12-43" src="https://user-images.githubusercontent.com/116753469/226989811-7f6426ac-9cd9-4665-aba9-bfab87eea4c8.png">
<img width="521" alt="Snipaste_2023-03-22_22-13-54" src="https://user-images.githubusercontent.com/116753469/226989817-3364f1ac-a951-4171-b0c9-1501b3585272.png">
<img width="1439" alt="Snipaste_2023-03-22_22-33-32" src="https://user-images.githubusercontent.com/116753469/226989822-82439067-e569-4e12-85b8-79b9cef7e505.png">
<img width="486" alt="Snipaste_2023-03-22_22-33-58" src="https://user-images.githubusercontent.com/116753469/226989825-8c79c419-cb99-48f8-bab7-8f0bdfc71c74.png">
<img width="1004" alt="Snipaste_2023-03-22_22-36-44" src="https://user-images.githubusercontent.com/116753469/226989826-a46a8739-bc13-437b-bb24-5593283ea1b6.png">
<img width="1004" alt="Snipaste_2023-03-22_22-37-53" src="https://user-images.githubusercontent.com/116753469/226989832-aad551a6-14be-47ca-89ac-84228ca7818c.png">
<img width="1004" alt="Snipaste_2023-03-22_22-41-20" src="https://user-images.githubusercontent.com/116753469/226989844-4291705a-c8f0-4797-8951-8f3ac24b54ef.png">
<img width="1439" alt="Snipaste_2023-03-22_23-12-28" src="https://user-images.githubusercontent.com/116753469/226989846-3ff75a43-3d41-4202-b653-9126f260e564.png">
<img width="750" alt="Snipaste_2023-03-22_23-25-10" src="https://user-images.githubusercontent.com/116753469/226989856-a50edff2-9548-49a6-961d-26d9db376ab4.png">
<img width="1017" alt="Snipaste_2023-03-22_23-26-11" src="https://user-images.githubusercontent.com/116753469/226989859-4eb2e3ce-fa1c-4871-90df-001c8d3857aa.png">
<img width="510" alt="Snipaste_2023-03-22_23-26-32" src="https://user-images.githubusercontent.com/116753469/226989862-7a5c4d97-5913-43c5-8a34-7c55e9d1bb24.png">
<img width="420" alt="Snipaste_2023-03-22_23-31-02" src="https://user-images.githubusercontent.com/116753469/226989865-c2807310-07b4-4f09-9546-d464450b9780.png">
<img width="693" alt="Snipaste_2023-03-22_23-36-22" src="https://user-images.githubusercontent.com/116753469/226989868-3baddaac-117c-4516-aa1a-3088030e5026.png">
<img width="541" alt="Snipaste_2023-03-22_23-39-54" src="https://user-images.githubusercontent.com/116753469/226989870-8c455c5e-1602-4338-9386-6d424e19cede.png">
<img width="1190" alt="Snipaste_2023-03-22_23-47-08" src="https://user-images.githubusercontent.com/116753469/226989873-bec0a957-4196-459c-b7f3-19e34aa0d5aa.png">
<img width="840" alt="Snipaste_2023-03-22_23-56-19" src="https://user-images.githubusercontent.com/116753469/226989875-be08c515-1fc8-4d19-b2d3-b479c2f90bfe.png">
<img width="1437" alt="Snipaste_2023-03-23_01-25-24" src="https://user-images.githubusercontent.com/116753469/226989878-6d6408e7-496f-4719-a353-78b5ee7f016b.png">


### Step 3: Convert the EC2 instance into an OVA file and store it in Amazon S3

Use the AWS CLI to convert the EC2 instance into an OVA file and store it in Amazon S3. Ensure that the OVA file is stored in a secure and accessible location.
(Upcoming)
### Step 4: Create an Amazon Machine Image (AMI) and EBS snapshot from the OVA file

Use the AWS Management Console to create an AMI and EBS snapshot from the OVA file stored in Amazon S3. Ensure that the AMI and EBS snapshot are properly configured and tagged for easy identification.
(Upcoming)
### Step 5: Launch a new EC2 instance from the AMI and EBS snapshot in the new AWS environment

Launch a new EC2 instance from the AMI and EBS snapshot in the new AWS environment. Ensure that the instance is properly configured and that SAP NetWeaver is running correctly.
(Upcoming)
