## Terraform AWS Setup: Nginx Web Server

This Terraform script sets up a basic AWS infrastructure to deploy a web server running Nginx. Below is a breakdown of the resources and configurations defined in the code:

## Prerequisites

Before running the script, make sure you have completed the following steps:

#### 1. **Install Terraform**

#### 2. **Ensure that the AWS CLI is installed and configured with your AWS credentials**

#### 3. **Create an SSH Key Pair**

## How to Run the Script

```bash
terraform init



### 1. AWS Provider Configuration
- Specifies AWS as the cloud provider.
- Sets the region to `us-east-1`.

### 2. VPC (Virtual Private Cloud)
- Creates a VPC with CIDR block `10.0.0.0/16`.
- Enables DNS support and DNS hostnames.
- Tags the VPC with the name `"main-vpc"`.

### 3. Public Subnet
- Creates a public subnet with CIDR block `10.0.1.0/24` in the availability zone `us-east-1a`.
- Configures the subnet to automatically assign public IP addresses to instances launched in it.
- Tags the subnet with the name `"public-subnet"`.

### 4. Internet Gateway
- Creates an internet gateway and attaches it to the VPC.
- Tags the gateway with the name `"internet-gateway"`.

### 5. Route Table (Public Route Table)
- Defines a route table for the VPC with a route to the internet (`0.0.0.0/0`) via the internet gateway.

### 6. Route Table Association
- Associates the public subnet with the public route table, allowing instances in the subnet to access the internet.

### 7. Security Group (Allow Nginx)
- Creates a security group allowing inbound HTTP traffic (port 80) from any IP address (`0.0.0.0/0`).
- Allows all outbound traffic.
- Tags the security group with the name `"allow-nginx"`.

### 8. EC2 Instance (Nginx Web Server)
- Launches an EC2 instance with Amazon Linux 2 AMI (`ami-063d43db0594b521b`) and instance type `t2.micro`.
- Places the instance in the public subnet with the `allow-nginx` security group.
- The instance is assigned a public IP address.
- Uses a `user_data` script to install and start Nginx, set up a "Hello World Terraform" page, and restart Nginx.
- Tags the instance with the name `"nginx-server"`.

### 9. Output
- Outputs the public IP address of the created EC2 instance (`web_public_ip`).

---

### Summary:
This Terraform script automates the creation of a simple web server infrastructure in AWS, including a VPC, public subnet, internet gateway, security group, and an EC2 instance running Nginx. The EC2 instance serves a static "Hello World" page, accessible via HTTP from the internet.
