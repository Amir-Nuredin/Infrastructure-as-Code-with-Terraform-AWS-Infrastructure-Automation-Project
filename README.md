# Infrastructure as Code with Terraform: AWS Infrastructure Automation Project

## Objective

This lab/project aims to develop practical skills in Infrastructure as Code (IaC), Terraform, AWS infrastructure automation, cloud networking, security configuration, and infrastructure lifecycle management. In this lab, I used Terraform and the AWS CLI to provision an AWS environment consisting of a VPC, public subnet, Internet Gateway, route table, security group, and EC2 instance. I also used Terraform variables and outputs to make the configuration more reusable and easier to manage.

To gain hands-on experience with automated cloud infrastructure management, I initialized, formatted, validated, planned, and deployed the Terraform configuration, then verified the resources in AWS. I modified the infrastructure and observed how Terraform identified and applied the change, reviewed Terraform state and security considerations, and tested infrastructure reproducibility. Finally, I used terraform destroy to remove the environment and verified that the AWS resources were successfully cleaned up. This project provided practical experience with the Infrastructure as Code lifecycle, including provisioning, validation, deployment, change management, security review, reproducibility, and cleanup.

### Skills Learned

This project provided hands-on experience with the following Infrastructure as Code, Terraform, and AWS infrastructure management skills:

- Terraform installation, configuration, initialization, formatting, validation, planning, and deployment
- AWS infrastructure provisioning using Terraform, including VPCs, subnets, Internet Gateways, route tables, security groups, and EC2 instances
- Terraform variables and outputs for creating reusable configurations and displaying infrastructure information
- AWS networking concepts, including CIDR addressing, public subnets, routing, Internet Gateways, and security group access controls
- Cloud infrastructure security assessment, including least privilege, network exposure, restricted SSH access, credential protection, and state security

### Tools Used

- Terraform
- Amazon Web Services (AWS)
- AWS CLI
- Amazon VPC
- Amazon EC2
- AWS Security Groups
- Visual Studio Code
- PowerShell

## Current Lab Environment Architecture/Setup

Below are screenshots of my current lab architecture before and after this week's lab/project (IM1&2). I worked in the cloud this week, so there were no changes to the VMs/virtual environment.

<img width="1535" height="1024" alt="image" src="https://github.com/user-attachments/assets/a0eef7d8-f3d0-4feb-97da-0c4670ab4fb9" />
<img width="1535" height="1024" alt="image" src="https://github.com/user-attachments/assets/0355e551-ace5-4a6d-ae26-8f591de2005e" />

IM1&2: Current Lab Environment/Architecture Before and After This Week's Project

## Steps/Procedure

### Part 1: Installing VS Code & Terraform

The first part of this project was to install the necessary resources. I needed to install VS Code to write my source code. I also needed to install the Terraform extension in VS Code so I could use Terraform. And lastly, I needed to install Terraform as my main IAC tool. I first installed VS Code by going to the official website (https://code.visualstudio.com/download?_exp_download=fb315fc982) and went through the installer (IM3). Once that was installed, I went to the Extensions tab and installed the "HashiCorp Terraform" Extension so that I could actually use Terraform in VS Code (IM4). Lastly, I went to the official HashiCorp website to install Terraform (IM5). After that was finished, I needed to extract the downloaded files, as it was downloaded as a ZIP file. I extracted it, then created a new folder to put the .exe file in (C:\terraform) (IM6). I then added Terraform to PATH by editing its environment variable. To confirm that Terraform was installed correctly, I went into PowerShell and ran the command "terraform version," and it worked (IM7). 

<img width="591" height="457" alt="Screenshot 2026-08-31 180816" src="https://github.com/user-attachments/assets/9c4ff146-70fb-40f1-b21f-2b9bc9e22471" />

IM3: Installing VS Code

<img width="697" height="188" alt="Screenshot 2026-08-31 181041" src="https://github.com/user-attachments/assets/02702273-e406-4975-bec3-0780586e9968" />

IM4: Installing HashiCorp VS Code Extension

<img width="1009" height="690" alt="image" src="https://github.com/user-attachments/assets/4cad7f08-bb46-47ab-ae5f-1f865367439e" />

IM5: Installing Terraform

<img width="574" height="217" alt="Screenshot 2026-08-31 181705" src="https://github.com/user-attachments/assets/1a11d2f6-c6ea-48f8-9020-4266df100c9a" />

IM6: Creating Terraform Folder and Extracting ZIP File

<img width="438" height="157" alt="Screenshot 2026-08-31 181949" src="https://github.com/user-attachments/assets/6320cf18-1b93-4d4f-991b-a077788c796c" />

IM7: Confirming Terraform Installed 

### Part 2: Installing and Configuring AWS CLI

Next up was configuring the AWS CLI. This needed to be installed so that VS Code and Terraform could interact and work with AWS to create and adjust infrastructure. To do this, I downloaded the official CLI for Windows and went through the installer (IM8). I then used the command "aws --version" to confirm the installation (IM9). I then needed to configure the CLI to my AWS account. I used the command "aws configure" and was then asked for my Access Key, Secret Access Key, Region, and output format. I didn't have an access key, so I had to go into AWS to create one. I did this by going to IAM in AWS, then Users, then the user I wanted to give the access key to (Admin-User), then under Security credentials to create the access key. I created it (IM10), then went back into PowerShell to finish the configuration (IM11). I then used the command "aws sts get-caller-identity" to confirm that the CLI was linked to my AWS account, and it was.

<img width="489" height="376" alt="Screenshot 2026-08-31 182248" src="https://github.com/user-attachments/assets/a467acf7-a52f-47e7-91a4-d9771499eaa3" />

IM8: Installing AWS CLI

<img width="459" height="83" alt="Screenshot 2026-08-31 182428" src="https://github.com/user-attachments/assets/58f5d9af-8291-43da-9f51-83fe56816d15" />

IM9: Confirming AWS CLI Installed

<img width="1452" height="292" alt="Screenshot 2026-08-31 183455" src="https://github.com/user-attachments/assets/dc3485e9-bc5f-40ca-90b2-6b3cce0d44f2" />

IM10: Access Key Created

<img width="638" height="97" alt="Screenshot 2026-08-31 183726" src="https://github.com/user-attachments/assets/177259cf-27a0-42d2-9380-51b28f50f4fb" />

IM11: Configuring AWS CLI with Account Info

<img width="496" height="164" alt="Screenshot 2026-08-31 183948" src="https://github.com/user-attachments/assets/cda51da7-9175-48a7-9598-ad37ba6f0ffd" />

IM12: Confirming AWS CLI was Correctly Configured and Connected to AWS Account 

### Part 4: Creating Terraform Project

Now that I had all the tools for this project, I was ready to work. First, I needed to create the Terraform project I would be using. I first created the project folder in PowerShell by using the commands in IM13. I then opened VS Code to confirm the folder was created, and it was. I then created the six main files I would be using in the folder. Those being main.tf (main codebase), variables.tf (variable names for different AWS resources), outputs.tf, versions.tf, .gitignore (any sensitive information), and a README.md file as well (IM14). 

<img width="643" height="312" alt="Screenshot 2026-08-31 184351" src="https://github.com/user-attachments/assets/8ae54bc0-98cd-405b-99bb-24b35b7a4783" />

IM13: Creating Terraform Project Folder

<img width="1453" height="213" alt="Screenshot 2026-08-31 184821" src="https://github.com/user-attachments/assets/d7da88d1-265f-42d2-bb79-c3eb9631f030" />

IM14: Creating Terraform Project files

### Part 5: Configuring AWS Provider

This step was important because Terraform needed to know which infrastructure provider needed to be used; otherwise, the code wouldn't be applied to anything. First, I went to the versions..tf file and added the code shown in IM15. This told Terraform that I would use the official AWS provider from HashiCorp. Next I went to the main.tf file and wrote the code for which region the provider was in (us-east-1). 

<img width="309" height="184" alt="Screenshot 2026-08-31 185111" src="https://github.com/user-attachments/assets/43aac616-31b9-4069-83c8-4f499f35c127" />

IM15: Configuring AWS Provider in Terraform

### Part 6: Terraform Initialization

Now I needed to initialize the Terraform Project so that it could actually be used and also so that the AWS provider is referenced as well. I ran the command "terraform init" inside the VS Code terminal, and I got a message saying that initialization was complete (IM16). Now my Project was ready to be worked on. 

<img width="577" height="184" alt="Screenshot 2026-08-31 185810" src="https://github.com/user-attachments/assets/34acf6b8-dc40-40c2-b889-389161274c7a" />

IM16: Terraform Project Initialized 

### Part 7: Creating VPC with Terraform

Now I could start actually working with Terraform and create the AWS Infrastructure with code. I planned to create a basic VPC with all the necessary components, then also created an EC2 instance and attached the VPC and Security Group to it. All of this main code would go into the "main.tf" file. First is the VPC. The code for the VPC can be seen in IM17. I defined the resource being created, the private IP range for the VPC, and the name for it in AWS as well. 

<img width="350" height="300" alt="Screenshot 2026-09-01 181003" src="https://github.com/user-attachments/assets/62f64caf-83cd-4048-ac39-bc8b6c6c3f81" />

IM17: VPC Terraform Code

### Part 8: Creating Subnet with Terraform

Next, I created the subnet for the VPC. The code for the subnet can be seen in IM18. For the subnet, I needed to reference the VPC associated with this subnet, the CIDR block for this subnet, the availability zone, and a tag at the end as well. 

<img width="315" height="290" alt="Screenshot 2026-09-01 181012" src="https://github.com/user-attachments/assets/68808932-9d31-4a4a-aaea-f79e1130d221" />

IM18: Subnet Terraform Code

### Part 9: Creating an Internet Gateway with Terraform

The next step was to create an Internet Gateway so the subnet, and eventually the instance, would have internet connectivity. The code can be seen in IM19. I associated the gateway with the VPC and gave it a tag/name.

<img width="313" height="200" alt="Screenshot 2026-09-01 181540" src="https://github.com/user-attachments/assets/1c06fb03-98e1-4434-883f-7710250eadb5" />

IM19: Internet Gateway Terraform Code. 

### Part 10: Creating a Route Table with Terraform

Next up was to create a route table so that how network traffic was being routed could be defined. The code for the route table can be seen in IM20&21. Again, I associated the route table with the VPC, gave the route a CIDR block, associated it with the internet gateway, and gave it a tag. I then associated the route table with my subnet as well. 

<img width="357" height="252" alt="Screenshot 2026-09-01 181548" src="https://github.com/user-attachments/assets/1997b30a-2ba4-4f23-bfe7-6b83dd859fe9" />
<img width="395" height="95" alt="Screenshot 2026-09-01 181909" src="https://github.com/user-attachments/assets/5d49b844-9689-45bc-9599-19c1eb0bb8bc" />

IM20&21: Route Table and Route Table Association Terraform Code

### Part 11: Creating Security Group with Terraform

Now I needed to create the Security group so that the EC2 instance could have outbound traffic and restrict SSH access to only my IP address. The code for the security Group can be seen in IM22. I named the Security Group, associated it with the VPC, created the inbound and outbound rules, as well as giving it a tag. 

<img width="446" height="491" alt="Screenshot 2026-09-01 182640" src="https://github.com/user-attachments/assets/08a67a9a-930e-4028-a7a0-e60d09d237f5" />

IM22: Security Group Terraform Code

### Part 12: Creating EC2 Instance with Terraform

The last main resource to create was the EC2 instance. The code for the instance can be seen in IM23&24. In the code, I defined the type of OS, the name of the instance, the AMI data source, the instance details, including the instance type. I also added the subnet and security group to it so they could be associated with the instance as well. Now I had the full Terraform code for this Project (IM25).

<img width="594" height="292" alt="Screenshot 2026-09-01 183003" src="https://github.com/user-attachments/assets/3c2b6e5c-978a-4253-ab33-a601943b13cb" />
<img width="446" height="491" alt="Screenshot 2026-09-01 182640" src="https://github.com/user-attachments/assets/5bf3c5f0-5329-488b-aa5b-21523872f334" />

IM23&24: EC2 Instance Terraform Code

<img width="594" height="968" alt="Screenshot 2026-09-01 183108" src="https://github.com/user-attachments/assets/806cd8c5-28bf-435e-9904-83a09cbdc2f5" />

IM25: Full Terraform Project Code



























































