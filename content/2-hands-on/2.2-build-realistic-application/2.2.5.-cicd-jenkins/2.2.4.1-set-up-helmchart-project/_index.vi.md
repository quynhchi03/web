---
title : "Set up HelmValue Project"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.2.5.1 </b> "
---
## 4. Setup project helmvalues
Trong dự án, chúng ta sẽ thiết lập dự án giá trị helmchart, nó chứa hoạt động triển khai, dịch vụ của đối tượng kubernetes.

Donwload repostiory  helmvalues tại github: https://github.com/daotq2000/aws-zero-downtime-jenkins

### Giải thích cho dự án này
Mục đích của dự án là định dạng đóng gói được gọi là biểu đồ. Biểu đồ là tập hợp các tệp mô tả một tập hợp tài nguyên Kubernetes có liên quan![copy-private-key.png](/images/2.5-helm-values/explain.png)
![copy-private-key.png](/images/2.5-helm-values/Monitoring.png)

### 4.1 Thông tin xác thực cấu hình cho Git
#### 4.1.1. Tạo khóa ssh cho người dùng jenkins-git để lấy kho lưu trữ từ github
Bây giờ, chúng ta cần ssh đến máy chủ Bastion, nơi máy chủ jenkins đã cài đặt và tạo khóa ssh cho phép mỗi lần chạy bản dựng, máy chủ jenkins có thể lấy cam kết thay đổi mới nhất từ  github.

Thực hiện theo các bước sau để thêm khóa ssh vào github:

![gen-ssh-key.png](/images/2.2-jenkins/gen-ssh-key.png)
Copy private key
![copy-private-key.png](/images/2.2-jenkins/copy-private-key.png)
#### 4.1.2. Go to Jenkins server, click to **Jenkins -> Management Jenkins -> Credentials -> System -> Global Credentials(unrestricted)**
Fill ID với  **jenkins-git**
![selected-plugsin.png](/images/2.2-jenkins/create-ssh-key-jenkins.png)
Next, dán  private key mà bạn đã copy vào đây 
![patseToSSh.png](/images/2.2-jenkins/patseToSSh.png)
#### 4.1.3. Copy public key and Tới **GitHub Preference** thêm  public key
Đi tới github,nhấp vào thanh bên phải và nhấp vào **setting**
![github-preferences.png](/images/2.2-jenkins/github-preferences.png)
Get public key using command:

       $cat ~/.ssh/id_rsa.pub

Đi tới `SSH and GPG keys`, and dán khóa chung của bạn vào đây.
![public-key.png](/images/2.2-jenkins/public-key.png)
Sau khi thành công chúng ta nhận được kết quả như bên dưới
![create-public-key.png](/images/2.2-jenkins/create-public-key.png)
#### 4.1.4. Config pipeline to fetch project
Tạo project pipeline and cấu hình pipeline.
![config-pipeline.png](/images/2.2-jenkins/config-pipeline.png)
Sử dụng pipeline bên dưới:

         def gitUrl = 'git@github.com:daotq2000/aws-spring-sqs-queue.git'
         def gitBranch = 'main'
         def gitCredential = 'jenkins-git'
         pipeline {
            stages {
                  stage('Checkout project') {
                  steps {
                  git branch: gitBranch,
                  credentialsId: gitCredential,
                  url: gitUrl
                  }
                  }
            }
         }
#### 4.1.5. Execute build
Nếu bạn nhận được kết quả dưới đây, bạn đã xây dựng thành công.
![success-build-helm.png](/images/2.2-jenkins/success-build-helm.png)
#### 4.1.6. Troubleshoot issue
Quá trình xây dựng liên quan đến vấn đề không thành công, có thể có một số lý do bên dưới
1. Thiếu variable trên pipeline
   ![issue-build1.png](/images/2.2-jenkins/issue-build1.png)
   Solution: kiểm tra log mesage 
2. Verify host failed
   Nếu bạn nhận được thông báo lỗi như `Verify host failed`, vui lòng làm theo giải pháp bên dưới:

Solution: **Go to Jenkins -> DashBoard -> Manage Jenkins -> Security -> Git Hot Key Verification and Configuration**  and choose **No Verification**
![issue-build1.png](/images/2.2-jenkins/verify-host-solution..png)
3. Git chưa cài đặt trên máy chủ.
   Solution: Kiểm tra phiên bản git trên máy chủ bằng cách sử dụng

         git -v
nếu bạn chưa cài đặt, hãy cài đặt git

      sudo yum install git -y

Sau đó chúng ta sẽ kéo kho lưu trữ bằng lệnh `git clone`

      git clone {your_git_repository}
Nếu bạn nhận được kết quả như hình ảnh bên dưới thì bạn đã kéo kho lưu trữ về máy chủ thành công.
![issue-build1.png](/images/2.2-jenkins/VerifiedGit.png)


