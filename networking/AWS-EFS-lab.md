## Amazon Elastic File System (EFS) Hands-On Lab

This lab was designed to give some experiences with console. 
In this especific one, interacting with the EC2 instances, also creating VPC's to work together with the EFS 


This repository demonstrate the conclusion of the following steps:

• Create a Virtual Private Cloud (VPC) with two Public Subnets\
• Create Security Groups for EC2 and EFS\
• Create an Elastic File system (EFS)\
• Create the first EC2 Instance and Mount our EFS drive\
• Create the second EC2 Instance and Mount our EFS drive\
• Connect to both EC2 instances using Instance Connect\
• Create a file on EFS drive\
• Demonstrate the EFS mount from the second instance\
• Clean up

## VPC and Public Subnets created:
![AWS Console](images/VPC.jpg)
![AWS Console](images/Subnet.jpg)

## Creating the EFS:

![AWS Console](images/EF2-new.jpg)



## EFS-1 and EF-2 running already with the Security Groups parameters 


![AWS Confirmation C2 Conect to S3](images/EFS-EC2.jpg)

## EFS-1 running connected


![AWS Confirmation C2 Conect to S3](images/EFS-connect1.jpeg)

## EFS-2 running connected


![AWS Confirmation C2 Conect to S3](images/EF2-connect2.jpg)

##  Create a file on EFS drive


![AWS Confirmation C2 Conect to S3](images/EFS-created-file.jpg)


to end the task, was ask to shut down the services we used today by deleting all. 
