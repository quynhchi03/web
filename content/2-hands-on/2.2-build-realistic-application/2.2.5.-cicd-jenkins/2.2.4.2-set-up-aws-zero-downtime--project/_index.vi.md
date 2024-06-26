---
title : "Set up AWS Zero Downtime Project Jenkins Pipeline"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.2.5.2 </b> "
---

## Introduce
Dự án thương mại điện tử là sự tích hợp với Cơ sở hạ tầng AWS và ứng dụng microservice được viết bằng Java, chúng tôi đang sử dụng Spring Boot
Phát triển API lấy dữ liệu từ Client để lưu dữ liệu vào cơ sở dữ liệu AWS Aurora, lấy dữ liệu từ cơ sở dữ liệu để trả về cho khách hàng
và cập nhật dữ liệu hiện có, xóa dữ liệu, v.v.

Cấu trúc dự án:

![project_stucture.png](/images/2.3_project/project_stucture.png)

Tham khảo kho Github của tôi: https://github.com/daotq2000/aws-spring-sqs-queue.git

Trong pipeline này, chúng ta  sẽ hoàn thành các hạng mục sau:

1. Kiểm tra kho git và kéo máy chủ jenkins
2. Sử dụng lệnh [maven](https://maven.apache.org/) để xây dựng ứng dụng spring boot
2. Lệnh Docker để nén ứng dụng dưới dạng hình ảnh vùng chứa và đẩy nó vào Amazon Container Register (ECR)
3. Tận dụng cấu hình biểu đồ trợ giúp của dự án tại [previous step](../2.2.4.1-set-up-helmchart-project) để lấy khóa bí mật biến môi trường và mẫu biểu đồ trợ giúp.
4. Using helm chart command to apply for create kubernetes object on Elastic Kubernetes Service(EKS) Cluster
## Getting Amazon Container Registry Push Command
To get ECR push command, we are follow these step:
1. Login to Amazon Console
2. Go to Amazon Container Registry
3. Click to detail project
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/ecr.png)
4. View push command
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/view-push-command.png)
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/push-command.png)

### Setup pipeline
Using pipeline below:

      def isJava = true;  
      // git repo
      def gitUrl = 'git@github.com:daotq2000/aws-spring-sqs-queue.git'
      def gitBranch = 'main'
      // project
      def projectGroup = 'aws'
      def projectName = "aws-zero-downtime"
      def namespace = "ciaws"
      def helmValues = "project-values/aws-zero-down-time/values-dev.yaml"
      /// DO NOT CHANGE BELOW
      // key login
      def gitCredential = 'jenkins-git'
      def deployDirectory = '/var/lib/jenkins/workspace/AWS/AWS-DEV/helm-values/helm-values'
      def mavenBuild = 'echo 1'
      dockerBuildCommand = './'
      def version = 'dev-0.0.${BUILD_NUMBER}'
      if (isJava == true) {
      mavenBuild = '/bin/bash ./mvnw -DskipTests clean package'
      }
      pipeline {
      agent any
      tools {
      jdk 'jdk11'
      }
      environment {
      DOCKER_REGISTRY = 'https://846338211683.dkr.ecr.us-east-1.amazonaws.com'
      DOCKER_IMAGE_NAME = "eks-project"
      DOCKER_IMAGE = "846338211683.dkr.ecr.us-east-1.amazonaws.com/${DOCKER_IMAGE_NAME}"
      }
      stages {
      // stage('Update helm  value') {
      //   steps {
      //     build job: "AWS/AWS-DEV/helm-values", wait: true
      //   }
      // }
      stage('Checkout project') {
      steps {
      git branch: gitBranch,
      credentialsId: gitCredential,
      url: gitUrl
      }
      }
      stage('Build And Push Docker Image') {
      steps {
      script {
      sh "git reset --hard"
      sh "git clean -f"
      sh "${mavenBuild}"
      sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 846338211683.dkr.ecr.us-east-1.amazonaws.com"
      sh "docker build -t ${DOCKER_IMAGE_NAME}:${version} ./"
      sh "docker tag ${DOCKER_IMAGE_NAME}:${version} ${DOCKER_IMAGE}:${version}"
      sh "docker push ${DOCKER_IMAGE}:${version}"
      sh "docker rmi ${DOCKER_IMAGE_NAME}:${version} -f"
      sh "docker rmi ${DOCKER_IMAGE}:${version} -f"
      }
      }
      }
      stage('Apply k8s') {
      steps {
      script {
      sh "helm upgrade $projectName $deployDirectory/chart-template/ -f $deployDirectory/$helmValues --namespace=$namespace -i --atomic --cleanup-on-fail --wait --timeout=5m --set fullnameOverride=$projectName,image.repository=${DOCKER_IMAGE},image.tag=${version}"
      }
      }
      }
      }
      } 
![zero-downtime-pipeline.png](/images/2.2-jenkins/zero-downtime-pipeline.png)

### Testing pipeline
After done all, we have received result below:
![zero-downtime-pipeline.png](/images/2.2-jenkins/build-success.png)

### Monitoring service on Kubernetes Cluster
#### Install K9s monitoring client tools
[What is K9s?](https://github.com/derailed/k9s)
- K9s provides a terminal UI to interact with your Kubernetes clusters. The aim of this project is to make it easier to navigate, observe and manage your applications in the wild. K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

[Install K9s] (https://github.com/derailed/k9s)
After done, we can monitoring kubernetes cluster any where.
![k9s](/images/2.3_project/k9s.png)

