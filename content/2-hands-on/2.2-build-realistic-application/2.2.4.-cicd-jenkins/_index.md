---
title : "Integration CI/CD Automate Tools"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.2.4 </b> "
---
## 1. CI/CD Tools

#### What is CI/CD tools?
CI/CD stands for Continuous Integration and Continuous Delivery/Deployment, which are methodologies that enable teams to consistently integrate new code and reliably deliver updates of their software.

**Continuous Integration (CI):**

This is a development practice where developers integrate code into a shared repository frequently, typically multiple times a day. Each integration can then be verified by an automatic build and automated tests. The key goals of CI are to find and address bugs quicker, improve software quality, and reduce the time it takes to validate and release new software updates.

**Continuous Delivery (CD):**

Following CI, Continuous Delivery automates the delivery of applications to selected infrastructure environments. Most teams work with multiple environments other than the production, such as development and testing environments, and CD ensures there is an automated way to push code changes to them.

**Continuous Deployment (CD):**

A step beyond Continuous Delivery, Continuous Deployment goes further by releasing every change that passes through the production pipeline to customers with no human intervention. It requires a highly developed culture of monitoring, automated testing, and quality assurance to work effectively.

#### Most Popular CI/CD tools
![CICD Tools](/images/2.2/cicd_tools.png?featherlight=false&width=50pc)
As image above, there are most popular CI/CD tools, pricing and the complexity, you can refer:

- **Jenkins:** An open-source automation server providing an impressive plugin ecosystem to support building, deploying, and automating any project.

- **GitLab CI/CD:** Integrated into the GitLab platform for source code management, it provides a rich set of features for automating different phases of the application lifecycle.
- **CircleCI:** Cloud-native CI/CD service that provides infrastructure for automating the software development process.
- **Travis CI:** A hosted, distributed continuous integration service to build and test software projects hosted at GitHub and Bitbucket.
- **GitHub Actions:** Enables workflows for continuous integration and continuous deployment directly in the GitHub platform.
- **Bamboo:** A CI/CD server from Atlassian, it offers automated building, testing, and deploying of applications.
- **Spinnaker:** An open-source, multi-cloud continuous delivery platform for releasing software changes with high velocity and confidence.
- **Azure Pipelines:** Part of Microsoft's Azure DevOps Services, this cloud service is used to automatically build and test code projects and make it available to other users.
## 2. Install Jenkins on Bastion Host
We will install Jenkins on Bastion Host.

#### 2.1 SSH to Bastion Host
    ssh -i public-bastion-host.pem ec2-user@YourEC2PublicIPV4
![SSH Successfully to Bastion Host](/images/2.2/ssh-bastion-host.png?featherlight=false&width=50pc)
#### 2.2 Configure Security for Jenkins
At [terraform source code](https://github.com/daotq2000/aws-iaac-terraform), we have configured inbound security group for Jenkins allow access from Internet to Jenkins server via port **8080**

    ingress {
    from_port   = 8080
    to_port     = 8080
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # Warning: This allows traffic from any IP which might not be secure.
    }

detail: https://github.com/daotq2000/aws-iaac-terraform/blob/main/aws-resources/05_sg.tf

#### 2.3 Downloading and installing Jenkins

Completing the previous steps enables you to download and install Jenkins on AWS. To download and install Jenkins:

Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:

    [ec2-user ~]$ sudo yum update –y

Add the Jenkins repo using the following command:

    [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

Import a key file from Jenkins-CI to enable installation from the package:

    [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
    [ec2-user ~]$ sudo yum upgrade
    Install Java (Amazon Linux 2023):

    [ec2-user ~]$ sudo dnf install java-17-amazon-corretto -y

**Install Jenkins:**

    [ec2-user ~]$ sudo yum install jenkins -y
Enable the Jenkins service to start at boot:

    [ec2-user ~]$ sudo systemctl enable jenkins
Start Jenkins as a service:

    [ec2-user ~]$ sudo systemctl start jenkins
You can check the status of the Jenkins service using the command:

    [ec2-user ~]$ sudo systemctl status jenkins

#### Configuring Jenkins
Jenkins is now installed and running on your EC2 instance. To configure Jenkins:
1. Connect to http://<your_server_public_DNS>:8080 from your browser. You will be able to access Jenkins through its management interface:
[Jenkins Password](https://www.jenkins.io/doc/book/resources/tutorials/AWS/unlock_jenkins.png)
2. As prompted, enter the password found in /var/lib/jenkins/secrets/initialAdminPassword.

Use the following command to display this password:

    [ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
3. The Jenkins installation script directs you to the Customize Jenkins page. Click Install suggested plugins.

4. Once the installation is complete, the Create First Admin User will open. Enter your information, and then select Save and Continue.
   [Jenkins Password](https://www.jenkins.io/doc/book/resources/tutorials/AWS/create_admin_user.png)
5. On the left-hand side, select Manage Jenkins, and then select Manage Plugins.

6. Select the Available tab, and then enter Amazon EC2 plugin at the top right.

7. Select the checkbox next to Amazon EC2 plugin, and then select Install without restart.
   [Jenkins Password](https://www.jenkins.io/doc/book/resources/tutorials/AWS/install_ec2_plugin.png)
8. Once the installation is done, select Back to Dashboard.

Select Configure a cloud if there are no existing nodes or clouds.