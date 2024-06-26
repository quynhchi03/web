---
title : "Set up AWS Zero Downtime Project Jenkins Pipeline"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.2.5.2 </b> "
---

## Introduce 
The e-commerce project is an integration with AWS Infrastructure and microservice  application written in Java, we are using Spring Boot
Develop API to retrieve data from Client to save data into AWS Aurora database, retrieve data from database to return to customer
and update existing data, delete data, and more.

There is project structure:

![project_stucture.png](/images/2.3_project/project_stucture.png)

Refer my Github reposittory: https://github.com/daotq2000/aws-spring-sqs-queue.git

In this pipeline project, we will complete these categories:

1. Check out git repository and pull for jenkins server
2. Using [maven](https://maven.apache.org/) command to build spring boot application 
2. Docker command to compress application as container image and push it to Amazon Container Registry (ECR) 
3. Leverage project helm-chart configure at [previous step](../2.2.4.1-set-up-helmchart-project) to pull environment variable secret key and helm chart template.
4. Sử dụng lệnh biểu đồ helm để áp dụng tạo đối tượng kubernetes trên Cụm dịch vụ Kubernetes đàn hồi (EKS)
5. ## Getting Amazon Container Registry Push Command
Để nhận lệnh đẩy ECR, chúng ta làm theo bước sau:
1. Đăng nhập vào Bảng điều khiển Amazon
2. Truy cập Cơ quan đăng ký vùng chứa Amazon
3. Click để xem chi tiết dự án
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/ecr.png)
4. Xem push command
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/view-push-command.png)
   ![zero-downtime-pipeline.png](/images/2.2-jenkins/push-command.png)
   
### Cấu hình pipeline
Cấu hình pipeline bên dưới:

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
Sau khi thực hiện build xong chúng ta có kết quả như sau:
![zero-downtime-pipeline.png](/images/2.2-jenkins/build-success.png)

### Giám sát Dịch vụ trên Kubernetes Cluster
#### Cài đặt công cụ client giám sát K9s
[What is K9s?](https://github.com/derailed/k9s)
- K9s cung cấp giao diện người dùng đầu cuối để tương tác với các cụm Kubernetes của bạn. Mục đích của dự án này là giúp việc điều hướng, quan sát và quản lý các ứng dụng của bạn trong thực tế trở nên dễ dàng hơn. K9 liên tục theo dõi Kubernetes để phát hiện những thay đổi và đưa ra các lệnh tiếp theo để tương tác với các tài nguyên được quan sát của bạn.
[Install K9s] (https://github.com/derailed/k9s)
  Sau khi hoàn tất, chúng ta có thể theo dõi cụm kubernetes ở bất kỳ đâu.
![k9s](/images/2.3_project/k9s.png)

