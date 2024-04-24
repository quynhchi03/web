---
title : "Testing Connection"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.2.2.5 </b> "
---
## Verify Connection 
Next, we need verify connection to make sure if container(It's application develop by any programing language such as Java, Python, NodeJS...) running, 
it can connect to rds database and redis cache.

There are categories we need verify to make sure connection always available:

1. Connection SSH from Internet to Bastion Host
2. **Bastion Host** can connect to **RDS Database**, **Redis Cache**, **Elastic Kubernetes Cluster** from VPC
3. **Bastion Host** can SSH to Worker Node from VPC
4. Worker Node can connect to  **RDS Database**, **Redis Cache**, **Elastic Kubernetes Cluster**, **Elastic Container Registry** from VPC

## Hands-on
### 1. SSH to Bastion Host from Internet

Step 1: Download keypair you have generated at `aws-resources/variables.tf`. this is [ssh_access_key](https://github.com/daotq2000/aws-iaac-terraform/blob/main/aws-resources/variables.tf) variable

Step 2: Using command below to ssh server

    $ chmod 400 public-bastion-host.pem
    $ ssh -i public-bastion-host.pem ec2-user@{Your Bastion Host IP}
If you received result as image below , you are successfully ssh to server.
![AWS SSH](/images/2.2/ssh-bastion-host.png?featherlight=false&width=100pc)

### 2. Ping connection from Bastion Host to Rds Database, Redis Cache, EKS cluster
After ssh successfully into bastion host, next we need instal [telnet](https://www.ionos.com/digitalguide/server/tools/telnet-commands/) tool to ping connection

Install telnet tool at Bastion Host using command below

    sudo yum install telnet
If you received result below, you are successfully installed telnet tools
![AWS SSH](/images/2.2/installed_telnet.png?featherlight=false&width=100pc)

If you haven't received result as image below, please check with your nat, internet gateway maybe connection to Internet has failed
#### 2.1 Ping connection from Bastion Host to RDS Database
Using command below to ping 

    telnet {host-aurora-postgres} {port-running}

- {host-aurora-postgres} and {port-running} you can get it at Amazon Console like below
  ![AWS SSH](/images/2.2/auroraping.png?featherlight=false&width=100pc)

If you received result below , you have connected to RDS Database from Bastion host
![AWS SSH](/images/2.2/telnet_ok_aurora.png?featherlight=false&width=100pc)

Or if you received result below, you haven't connected to RDS Database, need to check Security Group, Inbound traffic from Bastion Host to RDS datbase
![AWS SSH](/images/2.2/telnet_failed_aurora.png?featherlight=false&width=100pc)

#### 2.2 Ping connection from Bastion Host to Redis Cache Cluster
Using command below to ping
    
    telnet {host-redis-cluster} {port-running}

If you received result below , you have connected to Redis Cache from Bastion host
![AWS SSH](/images/2.2/telnet_ok_redis.png?featherlight=false&width=100pc)

#### 2.3 Ping connection from Bastion Host to Elastic Kubernetes Cluster(EKS)
Using command below to ping

    telnet {host-eks-cluster} {port-running}

If you received result below , you have connected to Redis Cache from Bastion host
![AWS SSH](/images/2.2/telnet_ok_eks.png?featherlight=false&width=100pc)

### 3. Bastion Host can SSH to Worker Node from VPC
Now, we need to ssh to Worker Node to monitoring, troubleshoot issue

Step 1: Copy your pem file generate at `1. SSH to Bastion Host from Internet` to Bastion Host , using command below

    vi public-basion-host.pem
Copy pem content file into this and using `Ecs + wq` to save file

Step 2: we need to permission this file for only system can access, using command below

    chmod 400 public-basion-host.pem
Step 3: Test ssh to Worker node using command below

    ssh -i public-basion-host.pem ec2-user@{your-private-worker-node-ip}

- {your-private-worker-node-ip} you can get this value at Amazon Console, why we need get private IP? Because of when provisioning resources with terraform.
We have configured worker node inside private subnet, mean which can't access by internet. It's internal communication, 
it help connection is safely and more effective because of save money charge for outbound traffic

#### 4. Worker Node can connect to  **RDS Database**, **Redis Cache**, **Elastic Kubernetes Cluster**, **Elastic Container Registry** from VPC
As mentions, all resources need to avoid access from Internet, now we need ping connection from Worker Node to that resources,
It's ensure when new deployment have been deploy to kubernetes, which work fine, no any element loss connection to require resources.

