# AWS-terraform

Summary:
This Terraform script sets up a simple web server infrastructure in AWS, including a VPC, a public subnet, an internet gateway, a security group, and an EC2 instance running Nginx. The instance serves a static "Hello World" page, accessible via HTTP from the internet.

This Terraform code defines infrastructure in AWS to create a simple VPC setup with a web server running Nginx. Here's a summary of the resources and configurations:

AWS Provider Configuration:

Specifies AWS as the cloud provider and sets the region to us-east-1.
VPC (Virtual Private Cloud):

Creates a VPC with CIDR block 10.0.0.0/16 and enables DNS support and hostnames.
Tags the VPC with the name "main-vpc".
Subnet (Public Subnet):

Creates a public subnet with CIDR block 10.0.1.0/24 in the us-east-1a availability zone.
Configures the subnet to automatically assign public IP addresses to instances launched within it.
Tags the subnet with the name "public-subnet".
Internet Gateway:

Creates an internet gateway and attaches it to the VPC.
Tags the gateway with the name "internet-gateway".
Route Table (Public Route Table):

Defines a route table for the VPC, including a route to the internet (0.0.0.0/0) through the internet gateway.
Route Table Association:

Associates the public subnet with the public route table, enabling instances in the subnet to access the internet.
Security Group (Allow Nginx):

Creates a security group allowing inbound HTTP (port 80) traffic from any IP address (0.0.0.0/0).
Allows all outbound traffic (egress set to 0.0.0.0/0).
Tags the security group with the name "allow-nginx".
EC2 Instance (Nginx Web Server):

Launches an EC2 instance using the Amazon Linux 2 AMI (ami-063d43db0594b521b) with instance type t2.micro (a small, free-tier eligible instance).
The instance is launched in the public subnet, with the allow-nginx security group and a public IP address.
A user_data script installs and starts Nginx, sets up a simple "Hello World Terraform" page, and restarts Nginx.
Tags the instance with the name "nginx-server".
Output:

Outputs the public IP address of the created EC2 instance (web_public_ip).
