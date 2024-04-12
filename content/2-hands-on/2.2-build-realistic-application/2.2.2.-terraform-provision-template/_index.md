---
title : "Terraform Provision Resources"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.2.2 </b> "
---


## What is Terraform?
Terraform is an open-source infrastructure as code (IaC) software tool created by HashiCorp. It allows users to define and provision data center infrastructure using a declarative configuration language known as HashiCorp Configuration Language (HCL), or optionally JSON.
## Set up aws cil and configure credentials
##3 Install aws-cli with WINDOW

## Project Structure
There are source code architecture, we are separately component

    ├── aws-resources
    │   ├── 00_main.tf
    │   ├── 01_vpc.tf
    │   ├── 02_subnet.tf
    │   ├── 03_ig.tf
    │   ├── 04_routeTable.tf
    │   ├── 05_sg.tf
    │   ├── 06_bastionHost.tf
    │   ├── 07_nlb.tf
    │   ├── 08_nat.tf
    │   ├── 09_iam-role.tf
    │   ├── 10_eks-cluster.tf
    │   ├── 11_eks-nodes.tf
    │   ├── 12_registry.tf
    │   ├── 13_database.tf
    │   ├── 14_caching.tf
    │   ├── 15_sqs..tf
    │   ├── 16_s3.tf
    │   ├── 17_alb.tf
    │   ├── 18_cloudfront.tf
    │   ├── 19_waf.tf
    │   ├── 20_code-build.tf
    │   ├── deploy-out.tf
    │   └── variables.tf
    ├── deploy.tfplan
    ├── error.txt
    ├── Infastructure-Design.png
    ├── main.tf
    ├── provider.tf
    ├── readme.md
    ├── script
    │   ├── jenkins-install.sh
    │   └── terraform.tfstate
    ├── ssh
    ├── terraform
    ├── terraform-apply.sh
    ├── terraform-destroy.sh
    ├── terraform-plan.sh
    ├── terraform.tfstate
    └── terraform.tfstate.backup

1. **aws-resources** is directory contains .tf file to create resources on AWS like vpc, eks, waf, nat
2. **provider.tf** is file contains dependency like aws, kubernetes...
3. **terraform-plan.sh** we are using this file to run command terraform plan
4. **terraform-apply.sh** we are using this file to run command terraform apply
5. **terraform.tfstate** to store bindings between objects in a remote system and resource instances declared in your configuration.
6. **provider.tf** providers allow Terraform to interact with cloud providers, SaaS providers, and other APIs
## Hands-on 
### 1. Create file provider.tf

    terraform {
    required_providers {
    aws = {
    source = "hashicorp/aws"
    version = "5.44.0"
    }
    kubernetes = {
    source = "hashicorp/kubernetes"
    version = ">= 2.3.2"
    }
    kubectl = {
    source  = "gavinbunney/kubectl"
    version = ">= 1.11.2"
    }
    helm = {
    source = "hashicorp/helm"
    version = ">= 2.2.0"
    }
    }
    }
    provider "aws" {
    region = "us-east-1"
    }
**terraform block:**
This block defines the required providers for the Terraform configuration. Providers are responsible for understanding and interacting with APIs, such as AWS, Kubernetes, etc.

**required_providers block:**
Within the terraform block, there's another block called required_providers. This block specifies the providers required for this configuration along with their sources and versions.

**aws provider:**
It specifies that Terraform requires the AWS provider.
source = "hashicorp/aws": Indicates the source of the AWS provider. In this case, it's from HashiCorp's repository.
version = "5.44.0": Specifies the version of the AWS provider required. Here, version 5.44.0 is specified.

**kubernetes provider:**
It specifies that Terraform requires the Kubernetes provider.
source = "hashicorp/kubernetes": Indicates the source of the Kubernetes provider, which is from HashiCorp's repository.
version = ">= 2.3.2": Specifies that any version greater than or equal to 2.3.2 of the Kubernetes provider is acceptable.

**kubectl provider:**
It specifies that Terraform requires the kubectl provider.
source = "gavinbunney/kubectl": Indicates the source of the kubectl provider, which is from Gavin Bunney's repository.
version = ">= 1.11.2": Specifies that any version greater than or equal to 1.11.2 of the kubectl provider is acceptable.

**helm provider:**
It specifies that Terraform requires the Helm provider.
source = "hashicorp/helm": Indicates the source of the Helm provider, which is from HashiCorp's repository.
version = ">= 2.2.0": Specifies that any version greater than or equal to 2.2.0 of the Helm provider is acceptable.

**provider "aws" block:**
This block configures the AWS provider specifically.
region = "us-east-1": Specifies the AWS region to use for this provider. In this case, it's set to "us-east-1".

### 2. Create file main.tf

    module "aws-resources" {
    source = "./aws-resources"
    }
**module block:**
This block is used to declare a module. Modules are reusable packages of Terraform configurations that are used to encapsulate and organize resources. They can be stored locally or remotely and are referenced within your main Terraform configuration.

**"aws-resources":**
This is the name assigned to the module instance. It's used as a reference to interact with this module in other parts of the Terraform configuration.

**source = "./aws-resources":**
This line specifies the location of the module. In this case, the module is located in a directory named "aws-resources" relative to the root of the current Terraform configuration. The source argument can also be a URL pointing to a remote module in a version control system like GitHub or a Terraform Module Registry.

### 2. Create file main.tf