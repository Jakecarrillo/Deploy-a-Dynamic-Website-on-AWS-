## Dynamic Ecommerce Website Deployment on AWS

This repository contains scripts and a reference diagram for deploying a dynamic ecommerce web application on Amazon Web Services (AWS) using various resources such as VPC, EC2 instances, RDS database, Application Load Balancer, Route 53, IAM roles, and more. Below is an overview of the architecture and deployment process.

### Architecture Overview:

- **VPC Configuration**: Utilizes a VPC with public and private subnets spread across two availability zones (AZs) for high availability and fault tolerance.
- **Internet Gateway**: Enables communication between instances in the VPC and the internet.
- **NAT Gateway**: Allows instances in private subnets to access the internet.
- **Bastion Host**: Provides secure access to instances in private subnets.
- **MySQL RDS Database**: Managed relational database service for storing application data.
- **EC2 Instances**: Hosts the ecommerce website.
- **Application Load Balancer (ALB)**: Distributes web traffic across an Auto Scaling Group of EC2 instances in multiple AZs.
- **Auto Scaling Group**: Dynamically scales EC2 instances to ensure high availability, fault tolerance, and elasticity.
- **Route 53**: Registers domain name and creates DNS record sets for routing traffic to the website.
- **AWS S3**: Stores web files for the website.
- **IAM Role**: Grants EC2 instances permission to download web files from AWS S3.
- **AMI Creation**: Once the website is installed on an EC2 instance, an AMI is created for future instance launches.

### Deployment Process:

1. **Update and Install Dependencies**: Update the system and install necessary packages like Apache HTTP Server (httpd).

```bash
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
```

2. **Download and Configure Web Files**: Download web files from GitHub repository and configure them for deployment.

```bash
cd /var/www/html
wget https://github.com/azeezsalu/jupiter/archive/refs/heads/main.zip
unzip main.zip
cp -r jupiter-main/* /var/www/html/
rm -rf jupiter-main main.zip
```

3. **Start HTTPD Service**: Enable and start the Apache HTTP Server service.

```bash
systemctl enable httpd 
systemctl start httpd
```

### Reference Diagram:
![Reference Architecture](Jupiter_Project_Reference_Architecture.jpg)

### Repository Contents:

- **Scripts**: Contains the deployment script for setting up the ecommerce website on an EC2 instance.
- **Reference Diagram**: Provides a visual representation of the architecture used for deploying the web application on AWS.

For detailed instructions and further customization, please refer to the scripts and diagram provided in this repository.

### Disclaimer:
Ensure to customize the deployment scripts and configurations according to your specific requirements and security best practices before deploying the ecommerce website on AWS.
