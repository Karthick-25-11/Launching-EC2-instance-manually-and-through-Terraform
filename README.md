# Launching-EC2-instance-manually-and-through-Terraform


This project demonstrates two different approaches to deploying an EC2 instance in AWS. In the first part, I manually created and configured an EC2 instance using the AWS Management Console with the default VPC, subnet, and security group, and connected to it using SSH. In the second part, I automated the EC2 creation process using Terraform, following infrastructure as code principles.

Project Overview

The goal of this project was to understand how EC2 instances work at a networking and security level, and then implement the same setup using Terraform for automation and repeatability. This helped me clearly understand the differences between manual configuration and infrastructure as code.

Part 1: Manual EC2 Configuration Using AWS Console

I started by using the AWS Management Console to launch an EC2 instance. I selected the default VPC provided by AWS and chose a public subnet. During instance creation, I enabled auto-assign public IPv4 so the instance could be accessed from the internet.

I used the default security group and added an inbound rule to allow SSH traffic on port 22 from anywhere.

Once the instance was running, I connected to it from my local machine using SSH and the key pair associated during launch. This helped me understand how public IPs, security groups work together to allow external access to EC2.

Part 2: EC2 Deployment Using Terraform

After completing the manual setup, I automated the EC2 deployment using Terraform. I configured the AWS provider with the required region and used Terraform resources to create an EC2 instance.

Instead of hardcoding values wherever possible, I focused on clean and simple configuration. I specified the instance type, key pair, and tags, and ensured the AMI architecture matched the instance type to avoid deployment errors.

I used terraform init to initialize the working directory, terraform plan to review the changes, and terraform apply to create the EC2 instance. This allowed me to deploy the same infrastructure repeatedly in a consistent way.

Issues Faced and How I Resolved Them

One of the main issues I faced was an SSH connection timeout even though the security group allowed port 22. I later understood that creating only a subnet does not make it public. The subnet needed to be associated with a route table that had a default route to an Internet Gateway, and the EC2 instance needed a public IP.

Another issue I encountered during Terraform deployment was an InvalidParameterValue error related to architecture mismatch. This happened because I used an ARM-based AMI with an x86_64 instance type. I resolved this by selecting an Amazon Linux 2 x86_64 AMI that matched the instance type.

These issues helped me gain a strong understanding of AWS networking concepts such as public vs private subnets, Internet Gateways, route tables, and EC2 architecture compatibility.

Learnings :

Through this project, I learned how EC2 networking works in AWS, including the role of VPCs, subnets, route tables, and security groups. I understood how SSH access depends not only on security groups but also on proper routing and public IP configuration.

I also learned how Terraform simplifies infrastructure management by allowing resources to be defined as code, making deployments more reliable and repeatable. This project helped me understand real-world issues and how to troubleshoot them effectively.

Conclusion

This project gave me hands-on experience with both manual EC2 configuration and automated EC2 deployment using Terraform. It strengthened my understanding of AWS core services and infrastructure as code, and helped me build confidence in debugging networking and deployment issues in cloud environments.

