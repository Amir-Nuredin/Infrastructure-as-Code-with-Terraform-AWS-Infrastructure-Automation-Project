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

### Part 3: Creating Terraform Project

Now that I had all the tools for this project, I was ready to work. First, I needed to create the Terraform project I would be using. I first created the project folder in PowerShell by using the commands in IM13. I then opened VS Code to confirm the folder was created, and it was. I then created the six main files I would be using in the folder. Those being main.tf (main codebase), variables.tf (variable names for different AWS resources), outputs.tf, versions.tf, .gitignore (any sensitive information), and a README.md file as well (IM14). 

<img width="643" height="312" alt="Screenshot 2026-08-31 184351" src="https://github.com/user-attachments/assets/8ae54bc0-98cd-405b-99bb-24b35b7a4783" />

IM13: Creating Terraform Project Folder

<img width="1453" height="213" alt="Screenshot 2026-08-31 184821" src="https://github.com/user-attachments/assets/d7da88d1-265f-42d2-bb79-c3eb9631f030" />

IM14: Creating Terraform Project files

### Part 4: Configuring AWS Provider

This step was important because Terraform needed to know which infrastructure provider needed to be used; otherwise, the code wouldn't be applied to anything. First, I went to the versions..tf file and added the code shown in IM15. This told Terraform that I would use the official AWS provider from HashiCorp. Next I went to the main.tf file and wrote the code for which region the provider was in (us-east-1). 

<img width="309" height="184" alt="Screenshot 2026-08-31 185111" src="https://github.com/user-attachments/assets/43aac616-31b9-4069-83c8-4f499f35c127" />

IM15: Configuring AWS Provider in Terraform

### Part 5: Terraform Initialization

Now I needed to initialize the Terraform Project so that it could actually be used and also so that the AWS provider is referenced as well. I ran the command "terraform init" inside the VS Code terminal, and I got a message saying that initialization was complete (IM16). Now my Project was ready to be worked on. 

<img width="577" height="184" alt="Screenshot 2026-08-31 185810" src="https://github.com/user-attachments/assets/34acf6b8-dc40-40c2-b889-389161274c7a" />

IM16: Terraform Project Initialized 

### Part 6: Creating VPC with Terraform

Now I could start actually working with Terraform and create the AWS Infrastructure with code. I planned to create a basic VPC with all the necessary components, then also created an EC2 instance and attached the VPC and Security Group to it. All of this main code would go into the "main.tf" file. First is the VPC. The code for the VPC can be seen in IM17. I defined the resource being created, the private IP range for the VPC, and the name for it in AWS as well. 

<img width="350" height="300" alt="Screenshot 2026-09-01 181003" src="https://github.com/user-attachments/assets/62f64caf-83cd-4048-ac39-bc8b6c6c3f81" />

IM17: VPC Terraform Code

### Part 7: Creating Subnet with Terraform

Next, I created the subnet for the VPC. The code for the subnet can be seen in IM18. For the subnet, I needed to reference the VPC associated with this subnet, the CIDR block for this subnet, the availability zone, and a tag at the end as well. 

<img width="315" height="290" alt="Screenshot 2026-09-01 181012" src="https://github.com/user-attachments/assets/68808932-9d31-4a4a-aaea-f79e1130d221" />

IM18: Subnet Terraform Code

### Part 8: Creating an Internet Gateway with Terraform

The next step was to create an Internet Gateway so the subnet, and eventually the instance, would have internet connectivity. The code can be seen in IM19. I associated the gateway with the VPC and gave it a tag/name.

<img width="313" height="200" alt="Screenshot 2026-09-01 181540" src="https://github.com/user-attachments/assets/1c06fb03-98e1-4434-883f-7710250eadb5" />

IM19: Internet Gateway Terraform Code. 

### Part 9: Creating a Route Table with Terraform

Next up was to create a route table so that how network traffic was being routed could be defined. The code for the route table can be seen in IM20&21. Again, I associated the route table with the VPC, gave the route a CIDR block, associated it with the internet gateway, and gave it a tag. I then associated the route table with my subnet as well. 

<img width="357" height="252" alt="Screenshot 2026-09-01 181548" src="https://github.com/user-attachments/assets/1997b30a-2ba4-4f23-bfe7-6b83dd859fe9" />
<img width="395" height="95" alt="Screenshot 2026-09-01 181909" src="https://github.com/user-attachments/assets/5d49b844-9689-45bc-9599-19c1eb0bb8bc" />

IM20&21: Route Table and Route Table Association Terraform Code

### Part 10: Creating Security Group with Terraform

Now I needed to create the Security group so that the EC2 instance could have outbound traffic and restrict SSH access to only my IP address. The code for the security Group can be seen in IM22. I named the Security Group, associated it with the VPC, created the inbound and outbound rules, as well as giving it a tag. 

<img width="446" height="491" alt="Screenshot 2026-09-01 182640" src="https://github.com/user-attachments/assets/08a67a9a-930e-4028-a7a0-e60d09d237f5" />

IM22: Security Group Terraform Code

### Part 11: Creating EC2 Instance with Terraform

The last main resource to create was the EC2 instance. The code for the instance can be seen in IM23&24. In the code, I defined the type of OS, the name of the instance, the AMI data source, and the instance details, including the instance type. I also added the subnet and security group to it so they could be associated with the instance as well. Now I had the full Terraform code for this Project (IM25).

<img width="594" height="292" alt="Screenshot 2026-09-01 183003" src="https://github.com/user-attachments/assets/3c2b6e5c-978a-4253-ab33-a601943b13cb" />
<img width="446" height="491" alt="Screenshot 2026-09-01 182640" src="https://github.com/user-attachments/assets/5bf3c5f0-5329-488b-aa5b-21523872f334" />

IM23&24: EC2 Instance Terraform Code

<img width="594" height="968" alt="Screenshot 2026-09-01 183108" src="https://github.com/user-attachments/assets/806cd8c5-28bf-435e-9904-83a09cbdc2f5" />

IM25: Full Terraform Project Code

### Part 12: Creating Terraform Variables

Now that I have finished the Terraform code, I wanted to do a few extra things to optimize the code. One of them is creating variables for the different AWS resources I created. This is so that the code can be reusable and updated as necessary. To do this, I went to the "variables.tf" file and entered the code seen in IM26. I created a variable for each main AWS resource (region, VPC, Subnet, Instance, and environment) and put the information for that resource in the variable. I then updated those variables in the "main.tf" file for each resource I created a variable for (IM27-30). 

<img width="440" height="574" alt="Screenshot 2026-09-01 183337" src="https://github.com/user-attachments/assets/d899def9-1647-4f53-81c7-3ecf07fb4165" />

IM26: Creating Variables for AWS resources

<img width="208" height="58" alt="Screenshot 2026-09-01 183458" src="https://github.com/user-attachments/assets/7dfef2f2-02f5-4746-a0a6-c2e7965c49e8" />
<img width="226" height="134" alt="Screenshot 2026-09-01 183551" src="https://github.com/user-attachments/assets/9bd7bee7-2e0e-4499-aa53-857835a7fb08" />
<img width="304" height="168" alt="Screenshot 2026-09-01 183656" src="https://github.com/user-attachments/assets/01189613-babf-449b-b2d3-f155c4492382" />
<img width="336" height="71" alt="Screenshot 2026-09-01 183741" src="https://github.com/user-attachments/assets/dfa4ab17-98d9-4085-81bc-ae6762af856a" />


IM27-30: Updating main.tf Code with Variables

### Part 13: Creating Terraform outputs

Now I need to create Terraform outputs as well. These are used to display info after deployment. The code for the outputs can be seen in IM31. 

<img width="436" height="485" alt="Screenshot 2026-09-01 184354" src="https://github.com/user-attachments/assets/b6cb633d-a827-4f07-9484-ae1d87324d53" />

IM31: Outputs Terraform Code

### Part 14: Formatting Configuration

Next, I needed to use the command "terraform fmt" in the VS Code terminal to format the code so that it stays clean and consistent (IM32). 

<img width="458" height="75" alt="Screenshot 2026-09-01 184442" src="https://github.com/user-attachments/assets/77b29c73-d221-4fc0-b27f-b0cf8b80aea5" />

### Part 15: Validating Configuration

I also needed to validate the configuration so Terraform understands the configuration before I deploy anything. I used the command "terraform validate" to check, and it was successful (IM32). 

<img width="490" height="80" alt="Screenshot 2026-09-01 185206" src="https://github.com/user-attachments/assets/10fb8754-a464-42a8-8218-9d6afe30f9ba" />

IM32: Validating Terraform Code

### Part 16: Terraform Plan

Next, I needed to run the command "terraform plan" to show me exactly what Terraform plans to create (IM33). It showed me a summary of all the AWS resources it will create. 

<img width="999" height="729" alt="Screenshot 2026-09-01 185402" src="https://github.com/user-attachments/assets/ea14a275-3009-458f-af15-72a9b8130453" />

IM33: Terraform Plan Output

### Part 17: Deploying AWS Infrastructure

Now I can finally deploy the AWS infrastructure using the command "Terraform apply." This showed the plan once again and asked me to confirm I wanted to deploy this, and I said yes (IM34). I then waited for the deployment to finish, and I then got a message saying that the apply was complete (IM35). 

<img width="408" height="132" alt="Screenshot 2026-09-01 185804" src="https://github.com/user-attachments/assets/73e5bca5-a86b-4310-a120-2a09b1d9bca0" />

IM34: Using Terraform Apply Command

<img width="675" height="319" alt="Screenshot 2026-09-01 185900" src="https://github.com/user-attachments/assets/9dfb7bc3-bd17-4d98-beca-491e8b460ec2" />

IM35: Terraform Deployment Complete

### Part 18: Verifying Infrastructure in AWS

Now that I created the AWS resources with Terraform, I now wanted to check in AWS to see if everything was created. I checked if the following were created: VPC, Subnet, Internet Gateway, Route Table, Subnet Association, Security Group, and EC2. They were all working and functional (IM36-42).

<img width="1189" height="52" alt="Screenshot 2026-09-01 190041" src="https://github.com/user-attachments/assets/61443849-6382-478d-82e8-6fe8e17daf25" />
<img width="1659" height="476" alt="Screenshot 2026-09-01 190121" src="https://github.com/user-attachments/assets/bdbdc868-9b29-450a-af37-4a80b1ad154e" />
<img width="1084" height="49" alt="Screenshot 2026-09-01 190148" src="https://github.com/user-attachments/assets/1cb6c12d-b0e0-4460-a782-05c18b4ee802" />
<img width="1667" height="596" alt="Screenshot 2026-09-01 190219" src="https://github.com/user-attachments/assets/48218041-977e-45cf-a15a-5e59ba74778c" />
<img width="1033" height="136" alt="Screenshot 2026-09-01 190237" src="https://github.com/user-attachments/assets/2e3e2ab2-d72b-45a7-af3a-26182c5114b0" />
<img width="1661" height="214" alt="Screenshot 2026-09-01 190326" src="https://github.com/user-attachments/assets/df3fb72c-bbce-4417-b44f-c052b7ed4e20" />
<img width="1587" height="582" alt="Screenshot 2026-09-01 190405" src="https://github.com/user-attachments/assets/d360e72d-1363-41fd-98d2-a2dbcdee7248" />

IM36-42: Confirming all AWS resources were correctly created

### Part 19: Infrastructure Security Review

Now that I created everything, I wanted to review all the resources and make sure they were secure. The table below summarizes the findings (TB1). 

| Security Area    | Finding                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Network Exposure | The EC2 instance has a public IPv4 address because it is located in the public subnet and requires connectivity for the lab. |
| Open Ports       | Only SSH TCP port 22 is permitted inbound.                                                                                   |
| SSH Source       | SSH is restricted to my authorized public IPv4 address using `/32`, instead of allowing `0.0.0.0/0`.                         |
| Security Group   | The inbound rule follows least privilege by allowing only the required protocol, port, and source.                           |
| Credentials      | AWS credentials are stored outside the Terraform configuration and are not hard-coded in `.tf` files.                        |
| Terraform State  | terraform.tfstate is excluded from Git because state may contain sensitive infrastructure information.                       |
| Secrets          | AWS keys, passwords, private keys, and other credentials are not stored in GitHub.                                           |
| Least Privilege  | The environment exposes only the network access needed for the lab.                                                          |

TB1: Terraform Security Review Findings

### Part 20: Terraform Destroy

Now that I finished the Lab, I wanted to destroy the AWS infrastructure in Terraform. This was done using the command "terraform destroy." It confirmed that I wanted to delete the infrastructure, and I confirmed it (IM43). I then went into AWS to see if the Resources were gone, and they were (IM44). 

<img width="1080" height="583" alt="Screenshot 2026-09-02 190835" src="https://github.com/user-attachments/assets/e713294d-d8b0-40fc-bdc5-0b2b9d61eb47" />

IM43: Destorying AWS Infrastructure with Terraform

<img width="1565" height="25" alt="Screenshot 2026-09-02 191000" src="https://github.com/user-attachments/assets/2d4cec14-7c7e-47ce-8729-4c2b05767569" />

IM44: Confirming Resources were Terminated

### Part 21: Terraform Architecture and Final Report

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/2825d56d-7e23-49ce-8812-4f817a44f8a1" />

## Conclusion

This lab successfully demonstrated the core concepts of Infrastructure as Code (IaC), Terraform, AWS infrastructure automation, cloud networking, and security configuration. Throughout the project, I used Terraform and the AWS CLI to provision and manage a VPC, public subnet, Internet Gateway, route table, security group, and EC2 instance. I also validated, planned, deployed, modified, and verified the infrastructure within AWS.

Overall, this project strengthened my understanding of Terraform variables, outputs, state management, resource dependencies, reproducibility, and cloud security best practices. The hands-on experience gained from this lab provides a strong foundation for future work in cloud infrastructure, DevOps, cloud security, automation, and enterprise cybersecurity.











































































