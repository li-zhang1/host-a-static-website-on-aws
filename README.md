## Architecture Diagram
![Static_Website Architecture](Host_a_Static_Website_on_AWS.png)

# Host a Static Website on AWS

## Project Overview
This project demonstrates how to host a static HTML web application on AWS using various AWS services and best practices. The repository includes a reference diagram and deployment scripts for setting up the web application on an EC2 instance.

## Architecture Overview
The infrastructure is deployed within an AWS Virtual Private Cloud (VPC) that spans two Availability Zones (AZs) for high availability and fault tolerance. The architecture consists of the following components:

### 1. Networking & Subnet Configuration
- **VPC**: The main networking environment for hosting the website.
- **Public Subnets**: Located in both Availability Zones for internet-facing resources (e.g., Internet Gateway).
- **Private Subnets**: Further divided into:
  - **Application Subnets**: Hosts EC2 instances running the web application.
  - **Data Subnets**: Secures databases or other backend services.
- **Route Tables**:
  - **Public Route Table**: Routes internet traffic via the Internet Gateway.
  - **Main Route Table**: Manages internal routing for private subnets.

### 2. Internet Access & Security
- **Internet Gateway**: Allows resources in public subnets to connect to the internet.
- **NAT Gateway**: Enables private subnets to access the internet securely.
- **Security Groups**: Acts as a firewall for traffic control.

### 3. Compute & Load Balancing
- **EC2 Instances**: Deployed within private subnets to host the static website.
- **Application Load Balancer (ALB)**: Distributes traffic across EC2 instances.
- **Auto Scaling Group (ASG)**: Ensures scalability and fault tolerance.

### 4. Additional Services
- **Amazon Route 53**: Manages the domain name system (DNS) configuration.
- **AWS Certificate Manager**: Secures website communications with SSL/TLS.
- **Amazon SNS**: Sends notifications about scaling activities.

## Deployment Steps
To deploy the project, follow these steps:

1. **Set up AWS resources** as outlined above.
2. **Use the provided Bash script** to install necessary packages and deploy the website:

```bash
# Switch to root user
sudo su  

# Update installed packages
yum update -y  

# Install Apache HTTP Server
yum install -y httpd  

# Navigate to Apache web root
cd /var/www/html  

# Install Git
yum install git -y  

# Clone the GitHub repository
git clone https://github.com/li-zhang1/host-a-static-website-on-aws.git  

# Copy all website files
cp -R host-a-static-website-on-aws/. /var/www/html/  

# Remove the cloned repository
rm -rf host-a-static-website-on-aws  

# Enable Apache to start on boot
systemctl enable httpd  

# Start Apache server
systemctl start httpd  
```

3. **Access the website** using the public IP or domain name registered with Route 53.

## Repository Contents
- **VPC Architecture Diagram** – Visual representation of the AWS setup.
- **Bash Script** – Automates deployment of the static website.
- **Configuration Files** – Defines security groups, VPC settings, and EC2 instance setup.

## Contributions
Feel free to fork the repository and submit pull requests for improvements.


