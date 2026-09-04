# Infrastructure as Code with Terraform AWS Infrastructure Automation Project

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













































