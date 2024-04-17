---
title : "Create aws-resources directory"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.2.2.4 </b> "
---
## Create aws-resources directory
This directory contains many resources as VPC, Load Balancer, Ec2...
The structure similar as below:
    
    ├── 00_main.tf
    ├── 01_vpc.tf
    ├── 02_subnet.tf
    ├── 03_ig.tf
    ├── 04_routeTable.tf
    ├── 05_sg.tf
    ├── 06_bastionHost.tf
    ├── 07_nlb.tf
    ├── 08_nat.tf
    ├── 09_iam-role.tf
    ├── 10_eks-cluster.tf
    ├── 11_eks-nodes.tf
    ├── 12_registry.tf
    ├── 13_database.tf
    ├── 14_caching.tf
    ├── 15_sqs..tf
    ├── 16_s3.tf
    ├── 17_alb.tf
    ├── 18_cloudfront.tf
    ├── 19_waf.tf
    ├── 20_code-build.tf
    ├── deploy-out.tf
    └── variables.tf


### Create 00_main.tf

    provider "aws" {
    region = "us-east-1" # replace with your AWS region, e.g., "us-east-1"
    }
The main purpose of this file is declare resources aws used in project

### Create 01_vpc.tf
    
    resource "aws_vpc" "vpc-main" {
    vpc-main = var.vpc_cidr_block
    enable_dns_hostnames = true
    enable_dns_support = true
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }

The main purpose of this file is declare VPC, terraform will create VPC with name `vpc-main` and cidr_block we had declared at `variables.tf`.

At `variables.tf` we had define cidr_block

    variable "vpc_cidr_block" {
    type = string
    default = "10.0.0.0/16"
    }
After run terraform plan, apply , it's created vpc have name is `vpc-main` and `vpc_cidr_block` is `10.0.0.0/16`

[Description]

### Create 02_subnet.tf

    `resource "aws_subnet" "public-subnet-1a" {
    vpc_id     = aws_vpc.vpc-main.id
    cidr_block = "10.0.1.0/24" # example CIDR block
    availability_zone = "us-east-1a"  # use the availability zone in your region
    
    map_public_ip_on_launch = true # for the bastion host to be accessible from the internet
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    resource "aws_subnet" "private-subnet-1a" {
    vpc_id     = aws_vpc.vpc-main.id
    cidr_block = "10.0.2.0/24" # example CIDR block
    map_public_ip_on_launch = false
    availability_zone = "us-east-1a" # use the availability zone in your region
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    resource "aws_subnet" "private-subnet-1b" {
    vpc_id     = aws_vpc.vpc-main.id
    cidr_block = "10.0.3.0/24" # example CIDR block
    map_public_ip_on_launch = false
    availability_zone = "us-east-1b" # use a different availability zone
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    resource "aws_subnet" "private-subnet-1c" {
    vpc_id     = aws_vpc.vpc-main.id
    cidr_block = "10.0.4.0/24" # example CIDR block
    map_public_ip_on_launch = false
    availability_zone = "us-east-1c" # use another different availability zone
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    #Create subnets group for rds cluster
    resource "aws_db_subnet_group" "subnet_group" {
    name       = "rds-subnet-group"
    subnet_ids = [aws_subnet.private-subnet-1a.id,aws_subnet.private-subnet-1b.id,aws_subnet.private-subnet-1c.id]
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    # Create subnets group for elastic cache
    resource "aws_elasticache_subnet_group" "redis_subnet_group" {
    name       = "redis-subnet-group"
    subnet_ids = [aws_subnet.private-subnet-1a.id,aws_subnet.private-subnet-1b.id,aws_subnet.private-subnet-1c.id]
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }
    `
This Terraform configuration defines several AWS subnets within a specified VPC. Let's break down each part:

**1. Public Subnet (us-east-1a):** This block defines a public subnet named "public-subnet-1a" with CIDR block "10.0.1.0/24" in availability zone "us-east-1a".
   map_public_ip_on_launch is set to true, indicating that instances launched in this subnet should be assigned public IP addresses.
   It's tagged with descriptive metadata.

**2. Private Subnets (us-east-1a, us-east-1b, us-east-1c):** Similar to the public subnet, but map_public_ip_on_launch is set to false, indicating instances launched in these subnets won't have public IP addresses.

**3. DB Subnet Group:** This block creates a DB subnet group named "rds-subnet-group" for an RDS cluster.
It includes the private subnets created earlier in its subnet_ids.

**4. Elasticache Subnet Group:** Similar to the DB subnet group, this block creates an Elasticache subnet group named "redis-subnet-group".
It also includes the private subnets created earlier in its subnet_ids.

These resources are organized within a VPC and allow for the segmentation of resources based on their need for public accessibility or their association with specific services like RDS or Elasticache. Additionally, they are tagged for better management and identification within the AWS environment.
[Description]

### Create 03_ig.tf

    `
    resource "aws_internet_gateway" "gw" {
    vpc_id = aws_vpc.vpc-main.id
    tags = {
    name="terraform project"
    description = "managed by terraform provisioning"
    }
    }`

**Resource Type:** This block defines a resource of type aws_internet_gateway. In AWS, an internet gateway allows communication between instances in your VPC and the internet.

**Resource Name:** "gw" is the name given to this specific internet gateway resource block. It's used to refer to this resource elsewhere in the Terraform configuration.

**VPC Association:** vpc_id = aws_vpc.vpc-main.id associates this internet gateway with a specific VPC. aws_vpc.vpc-main.id references the ID of the VPC named "vpc-main", which must have been previously defined in the configuration.

**Tags:** This block defines tags for the internet gateway, providing metadata for identification and organization purposes. In this case, it has two tags: "name" and "description", both indicating that this resource is part of the "terraform project" and is "managed by terraform provisioning", respectively.

Overall, this configuration sets up an internet gateway within a specified VPC and applies descriptive tags for easier management and identification within the AWS environment.

### Create 04_routeTable.tf
    
    `resource "aws_route_table" "rtb-public" {
    vpc_id = aws_vpc.vpc-main.id
    route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
    }
    
    }
    resource "aws_route_table" "rtb-internal" {
    vpc_id = aws_vpc.vpc-main.id
    route {
    cidr_block = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.nat-gw.id
    }
    
    }
    
    # Associate the route table with the public subnet
    resource "aws_route_table_association" "associate_public_1a" {
    subnet_id      = aws_subnet.public-subnet-1a.id
    route_table_id = aws_route_table.rtb-public.id
    
    }
    resource "aws_route_table_association" "associate_private_1a" {
    subnet_id = aws_subnet.private-subnet-1a.id
    route_table_id = aws_route_table.rtb-internal.id
    
    }
    resource "aws_route_table_association" "associate_private_1b" {
    subnet_id = aws_subnet.private-subnet-1b.id
    route_table_id = aws_route_table.rtb-internal.id
    
    }
    resource "aws_route_table_association" "associate_private_1c" {
    subnet_id = aws_subnet.private-subnet-1c.id
    route_table_id = aws_route_table.rtb-internal.id
    
    }
    `
This Terraform configuration sets up route tables for managing network traffic within a VPC, associating different routes with specific subnets. Let's break down each part:

1. Public Route Table: This block defines a route table named "rtb-public" associated with the VPC named "vpc-main".
   It includes a route with CIDR block "0.0.0.0/0", which effectively represents all IP addresses. This route directs traffic to the internet gateway specified by `aws_internet_gateway.gw.id`
2. Internal Route Table: Similar to the public route table, this block defines a route table named "rtb-internal" associated with the VPC named "vpc-main".
   It includes a route with CIDR block "0.0.0.0/0", directing traffic to a NAT gateway specified by aws_nat_gateway.nat-gw.id. This setup is common for private subnets to allow outbound internet access while keeping instances private.
3. Route Table Associations: These blocks associate the previously defined route tables with specific subnets.

For example, "associate_public_1a" associates the "rtb-public" route table with the public subnet "public-subnet-1a".

Similarly, "associate_private_1a", "associate_private_1b", and "associate_private_1c" associate the "rtb-internal" route table with the private subnets "private-subnet-1a", "private-subnet-1b", and "private-subnet-1c", respectively.

### Create 05_sg.tf
    
    `resource "aws_security_group" "bastion_sg" {
    name        = "bastion_security_group"
    description = "Allow SSH inbound traffic bastion_sg"
    vpc_id      = aws_vpc.vpc-main.id
    
    ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = [
    "0.0.0.0/0", aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block
    ]
    }
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    }
    egress {
    from_port   = 6379
    to_port     = 6379
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    egress {
    from_port   = 5432
    to_port     = 5432
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    
    
    tags = {
    name        = "terraform project"
    description = "managed by terraform provisioning"
    }
    }
    resource "aws_security_group" "sg_private_eks_node" {
    name = "Security group private eks node"
    vpc_id = aws_vpc.vpc-main.id
    ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = [aws_vpc.vpc-main.cidr_block,aws_subnet.private-subnet-1a.cidr_block,aws_subnet.private-subnet-1b.cidr_block,aws_subnet.private-subnet-1c.cidr_block,]
    }
    egress {
    from_port   = 6379
    to_port     = 6379
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    egress {
    from_port   = 5432
    to_port     = 5432
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    }
    
    }
    resource "aws_security_group" "postgres_aurora_sg" {
    name   = "security_rds_cluster"
    vpc_id = aws_vpc.vpc-main.id
    
    ingress {
    from_port   = 6739
    to_port     = 6739
    protocol    = "tcp"
    cidr_blocks = [
    aws_vpc.vpc-main.cidr_block, aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block
    ]
    }
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    tags = {
    name        = "terraform project"
    description = "managed by terraform provisioning"
    }
    }
    resource "aws_security_group" "redis_sg" {
    name   = "redis_sg"
    vpc_id = aws_vpc.vpc-main.id
    ingress {
    from_port = 6379
    to_port = 6379
    protocol = "tcp"
    security_groups = [aws_security_group.bastion_sg.id]
    cidr_blocks = [aws_vpc.vpc-main.cidr_block,aws_subnet.public-subnet-1a.cidr_block,
    aws_subnet.private-subnet-1a.cidr_block,aws_subnet.private-subnet-1b.cidr_block,aws_subnet.private-subnet-1c.cidr_block,]
    }
    egress {
    from_port = 0
    to_port = 0
    protocol = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    }
    tags = {
    name        = "terraform project"
    description = "managed by terraform provisioning"
    }
    }
    #Create SG for Application Load Banlancer
    resource "aws_security_group" "alb_sg" {
    name   = "application_loadbalancer_sg"
    vpc_id = aws_vpc.vpc-main.id
    tags = {
    name        = "terraform project"
    description = "managed by terraform provisioning"
    }
    ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    }
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
    }
    egress {
    from_port   = 0
    to_port     = 0
    protocol    = "tcp"
    cidr_blocks = [aws_subnet.private-subnet-1a.cidr_block, aws_subnet.private-subnet-1b.cidr_block,
    aws_subnet.private-subnet-1c.cidr_block, aws_subnet.public-subnet-1a.cidr_block]
    }
    }
    `
This Terraform configuration creates several AWS security groups, each with specific inbound and outbound rules to control traffic within a VPC. Let's break down each part:

**Bastion Security Group:**

Named "bastion_sg", it allows SSH (port 22) inbound traffic from anywhere (0.0.0.0/0) as well as from the CIDR blocks of the private and public subnets.

It allows all outbound traffic (0.0.0.0/0) and also allows outbound traffic on ports 6379 (Redis) and 5432 (PostgreSQL) to the CIDR blocks of the private and public subnets.

**Private EKS Node Security Group:**

Named "sg_private_eks_node", it allows SSH (port 22) inbound traffic from the CIDR blocks of the VPC and private subnets.
It allows outbound traffic on ports 6379 (Redis) and 5432 (PostgreSQL) to the CIDR blocks of the private and public subnets and also to any destination.
RDS Cluster Security Group:

Named "postgres_aurora_sg", it allows inbound traffic on port 6739 (for RDS or Aurora) from the CIDR blocks of the VPC and subnets.
It allows outbound traffic to the CIDR blocks of the private and public subnets.
Redis Security Group:

Named "redis_sg", it allows inbound traffic on port 6379 (Redis) only from the security group "bastion_sg" and from the CIDR blocks of the VPC and subnets.
It allows all outbound traffic (0.0.0.0/0).

**Application Load Balancer (ALB) Security Group:**

Named "alb_sg", it allows all inbound and outbound traffic from and to anywhere (0.0.0.0/0) on all ports (-1 for all protocols).
It allows outbound traffic on all ports to the CIDR blocks of the private and public subnets.


##### All security groups are tagged for identification and management purposes. They control traffic flow between different types of resources within the VPC, ensuring security and compliance with network policies.


### Create 06_bastionHost.tf

      `resource "aws_instance" "bastion_host" {
      ami           = "ami-0c101f26f147fa7fd" # example AMI, update to the latest
      instance_type = "t2.micro" # example instance type, choose as per need
      subnet_id     = aws_subnet.public-subnet-1a.id
      key_name      = var.ssh_access_key # specify your key pair name
      security_groups = [aws_security_group.bastion_sg.id]
      user_data = <<EOF
      sudo yum update –y
      sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
      sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
      sudo yum upgrade
      sudo dnf install java-17-amazon-corretto -y
      sudo yum install jenkins -y
      sudo systemctl enable jenkins
      sudo systemctl start jenkins
      sudo systemctl status jenkins
      EOF
      
      tags = {
      name="terraform project"
      description = "managed by terraform provisioning"
      }
      }`

**Resource Type and Name:** It defines an AWS instance resource named "bastion_host". This resource type represents a virtual server in the Amazon Web Services (AWS) cloud.

**AMI and Instance Type:** The ami parameter specifies the Amazon Machine Image (AMI) ID to use for launching the instance. In this case, it's using a placeholder value (ami-0c101f26f147fa7fd). The instance_type parameter specifies the type of instance to launch, which in this case is a "t2.micro" instance.

**Subnet and Security:** The subnet_id parameter specifies the subnet in which the instance will be launched. It's using a variable (aws_subnet.public-subnet-1a.id), which should contain the actual subnet ID. The security_groups parameter defines the security group(s) associated with the instance, ensuring network security.

**Key Pair:** The key_name parameter specifies the name of the SSH key pair that will be used to connect to the instance. It's using a variable (var.ssh_access_key), which should contain the actual key pair name.

**User Data:** The user_data parameter contains the script that will be executed when the instance is launched. This script updates the system packages, installs Jenkins (a popular automation server), and starts the Jenkins service. It also installs Java 17 using the Amazon Corretto distribution.

**Tags:** Tags are key-value pairs used for organizing and managing AWS resources. In this block, tags are applied to the instance for identification and management purposes.

Overall, this block of code sets up an AWS EC2 instance (bastion host) with necessary configurations and software installations using Terraform. It's a part of an infrastructure provisioning process managed by Terraform.

### Create 07_nat.tf
Next, we need create NAT Gateway to ec2 instance can connect over internet.

      resource "aws_eip" "nat-eip" {
      vpc = true
      tags = {
      name="terraform project"
      description = "managed by terraform provisioning"
      }
      }
      resource "aws_nat_gateway" "nat-gw" {
      allocation_id = aws_eip.nat-eip.id
      subnet_id     = aws_subnet.public-subnet-1a.id
      depends_on = [aws_internet_gateway.gw]
      tags = {
      name="terraform project"
      description = "managed by terraform provisioning"
      }
      }

Elastic IP Resource:

      resource "aws_eip" "nat-eip" {
      vpc = true
      tags = {
      name        = "terraform project"
      description = "managed by terraform provisioning"
      }
      }

This block defines an AWS Elastic IP (EIP) resource named "nat-eip". The vpc = true line specifies that this EIP is to be associated with a VPC (Virtual Private Cloud). Tags are also assigned to the EIP for identification and management purposes.

NAT Gateway Resource:
      
      resource "aws_nat_gateway" "nat-gw" {
      allocation_id = aws_eip.nat-eip.id
      subnet_id     = aws_subnet.public-subnet-1a.id
      depends_on    = [aws_internet_gateway.gw]
      tags = {
      name        = "terraform project"
      description = "managed by terraform provisioning"
      }
      }

This block defines an AWS NAT Gateway resource named "nat-gw". The allocation_id parameter specifies the Elastic IP allocation ID associated with the NAT Gateway, which is obtained from the previously defined Elastic IP resource (aws_eip.nat-eip.id). The subnet_id parameter specifies the subnet in which the NAT Gateway will be deployed. The depends_on parameter ensures that the NAT Gateway is created only after the associated internet gateway (aws_internet_gateway.gw) is created. Tags are also applied to the NAT Gateway for identification and management purposes.

Overall, this block of code provisions an Elastic IP and a NAT Gateway in an AWS environment using Terraform. The NAT Gateway facilitates outbound internet access for resources in private subnets within the VPC.

## Create 08_iam-role.tf
      
      ### Create Role for EKS Cluster
      resource "aws_iam_role" "role-eks" {
      name = "eks_role"
      
      assume_role_policy = jsonencode({
      "Version": "2012-10-17",
      "Statement": [
      {
      "Effect": "Allow",
      "Principal": {
      "Service": [
      "eks.amazonaws.com"
      ]
      },
      "Action": "sts:AssumeRole"
      }
      ]
      })
      }
      #Attach Policies to the Role for EKS Cluster
      resource "aws_iam_role_policy_attachment" "eks_attach" {
      role       = aws_iam_role.role-eks.name
      policy_arn = "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
      
      }
      # Create Role for EKS Node
      resource "aws_iam_role" "nodes" {
      name = "eks-node-group-nodes"
      
      assume_role_policy = jsonencode({
      Statement = [{
      Action = "sts:AssumeRole"
      Effect = "Allow"
      Principal = {
      Service = "ec2.amazonaws.com"
      }
      }]
      Version = "2012-10-17"
      })
      
      }
      
      #Attach Policies to the Role for EKS Node
      resource "aws_iam_role_policy_attachment" "nodes-AmazonEKSWorkerNodePolicy" {
      policy_arn = "arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy"
      role       = aws_iam_role.nodes.name
      }
      
      resource "aws_iam_role_policy_attachment" "nodes-AmazonEKS_CNI_Policy" {
      policy_arn = "arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy"
      role       = aws_iam_role.nodes.name
      
      }
      
      resource "aws_iam_role_policy_attachment" "nodes-AmazonEC2ContainerRegistryReadOnly" {
      policy_arn = "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly"
      role       = aws_iam_role.nodes.name
      }

This block of Terraform code is used to define and configure IAM roles and policies for an Amazon Elastic Kubernetes Service (EKS) cluster and its associated nodes. Let's break down the main purposes of each block:

      resource "aws_iam_role" "role-eks" {
      name = "eks_role"
      
      assume_role_policy = jsonencode({
      "Version": "2012-10-17",
      "Statement": [
      {
      "Effect": "Allow",
      "Principal": {
      "Service": [
      "eks.amazonaws.com"
      ]
      },
      "Action": "sts:AssumeRole"
      }
      ]
      })
      }

2. 