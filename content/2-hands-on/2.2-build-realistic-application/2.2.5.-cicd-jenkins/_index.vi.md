---
title : "Integration CI/CD Automate Tools"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.2.5 </b> "
---
## 1. CI/CD Tools

#### Công cụ CI/CD là gì?
CI/CD là viết tắt của Tích hợp liên tục và Phân phối/Triển khai liên tục, là các phương pháp cho phép các nhóm tích hợp mã mới một cách nhất quán và cung cấp các bản cập nhật phần mềm của họ một cách đáng tin cậy.

**Tích hợp liên tục (CI):**

Đây là một phương pháp phát triển trong đó các nhà phát triển thường xuyên tích hợp mã vào kho lưu trữ dùng chung, thường là nhiều lần trong ngày. Sau đó, mỗi tích hợp có thể được xác minh bằng quá trình xây dựng tự động và kiểm tra tự động. Mục tiêu chính của CI là tìm và giải quyết lỗi nhanh hơn, cải thiện chất lượng phần mềm và giảm thời gian xác thực và phát hành bản cập nhật phần mềm mới.

**Giao hàng liên tục (CD):**

Theo CI, Phân phối liên tục tự động hóa việc phân phối ứng dụng đến các môi trường cơ sở hạ tầng đã chọn. Hầu hết các nhóm làm việc với nhiều môi trường khác ngoài môi trường sản xuất, chẳng hạn như môi trường phát triển và thử nghiệm, đồng thời CD đảm bảo có một cách tự động để đẩy các thay đổi mã tới chúng.

**Triển khai liên tục (CD):**

Một bước xa hơn Phân phối liên tục, Triển khai liên tục còn tiến xa hơn bằng cách phát hành mọi thay đổi đi qua quy trình sản xuất tới khách hàng mà không có sự can thiệp của con người. Nó đòi hỏi một nền văn hóa giám sát, kiểm tra tự động và đảm bảo chất lượng phát triển cao để hoạt động hiệu quả.

#### Công cụ CI/CD phổ biến nhất
![Công cụ CICD](/aws-stutdy-group-workshop/images/2.2/cicd_tools.png?featherlight=false&width=50pc)
Như hình trên, có những công cụ CI/CD phổ biến nhất, giá cả và độ phức tạp, bạn có thể tham khảo:

- **Jenkins:** Một máy chủ tự động hóa nguồn mở cung cấp hệ sinh thái plugin ấn tượng để hỗ trợ xây dựng, triển khai và tự động hóa bất kỳ dự án nào.

- **GitLab CI/CD:** Được tích hợp vào nền tảng GitLab để quản lý mã nguồn, nó cung cấp một bộ tính năng phong phú để tự động hóa các giai đoạn khác nhau của vòng đời ứng dụng.
- **CircleCI:** Dịch vụ CI/CD gốc trên nền tảng đám mây cung cấp cơ sở hạ tầng để tự động hóa quy trình phát triển phần mềm.
- **Travis CI:** Dịch vụ tích hợp liên tục được phân phối, được lưu trữ để xây dựng và thử nghiệm các dự án phần mềm được lưu trữ tại GitHub và Bitbucket.
- **Thao tác GitHub:** Kích hoạt quy trình công việc để tích hợp liên tục và triển khai liên tục trực tiếp trong nền tảng GitHub.
- **Bamboo:** Máy chủ CI/CD của Atlassian, cung cấp khả năng xây dựng, thử nghiệm và triển khai ứng dụng tự động.
- **Spinnaker:** Nền tảng phân phối liên tục trên nhiều đám mây, mã nguồn mở để phát hành các thay đổi phần mềm với tốc độ cao và độ tin cậy.
- **Azure Pipelines:** Là một phần của Dịch vụ Azure DevOps của Microsoft, dịch vụ đám mây này được sử dụng để tự động xây dựng và kiểm tra các dự án mã cũng như cung cấp cho những người dùng khác.
## 2. Cài đặt Jenkins trên Bastion Host
Chúng tôi sẽ cài đặt Jenkins trên Bastion Host.

#### 2.1 SSH tới máy chủ Bastion
ssh -i public-bastion-host.pem ec2-user@YourEC2PublicIPV4
![SSH vào máy chủ Bastion thành công](/aws-stutdy-group-workshop/images/2.2/ssh-bastion-host.png?featherlight=false&width=50pc)

#### 2.2 Cấu hình bảo mật cho Jenkins
Tại [mã nguồn terraform](https://github.com/daotq2000/aws-iaac-terraform), chúng tôi đã định cấu hình nhóm bảo mật gửi đến cho Jenkins cho phép truy cập từ Internet đến máy chủ Jenkins qua cổng **8080**
    

      ingress {
          from_port   = 8080
          to_port     = 8080
          protocol    = "tcp"
          cidr_blocks = ["0.0.0.0/0"] # Warning: This allows traffic from any IP which might not be secure.
          }

chi tiết : https://github.com/daotq2000/aws-iaac-terraform/blob/main/aws-resources/05_sg.tf

#### 2.3 Downloading and installing Jenkins

Việc hoàn thành các bước trước đó sẽ cho phép bạn tải xuống và cài đặt Jenkins trên AWS. Để tải xuống và cài đặt Jenkins:

Đảm bảo rằng các gói phần mềm được cập nhật trên phiên bản của bạn bằng cách sử dụng lệnh sau để thực hiện cập nhật phần mềm nhanh:

    [ec2-user ~]$ sudo yum update –y

Thêm repo Jenkins bằng lệnh sau:

    [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

Nhập tệp khóa từ Jenkins-CI để cho phép cài đặt từ gói:

    [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
    [ec2-user ~]$ sudo yum upgrade
    Install Java (Amazon Linux 2023):

    [ec2-user ~]$ sudo dnf install java-17-amazon-corretto -y

**Cài đặt Jenkins:**

    [ec2-user ~]$ sudo yum install jenkins -y
Kích hoạt dịch vụ Jenkins để bắt đầu khi khởi động:

    [ec2-user ~]$ sudo systemctl enable jenkins
Bắt đầu Jenkins như một dịch vụ:

    [ec2-user ~]$ sudo systemctl start jenkins
Bạn có thể kiểm tra trạng thái của dịch vụ Jenkins bằng lệnh:

    [ec2-user ~]$ sudo systemctl status jenkins
## 3. Cài đặt Docker trên Bastion Host
Bạn có thể tham khảo bài đăng cài đặt docker trên Amazon Linux tại [tại đây](https://www.cyberciti.biz/faq/how-to-install-docker-on-amazon-linux-2/) hoặc các bước xây dựng sau đây:
1. Áp dụng các bản cập nhật đang chờ xử lý bằng lệnh yum

         sudo yum update
2. Tìm kiếm gói Docker:

         sudo yum search docker
3. Lấy thông tin phiên bản:

        sudo yum info docker
4. Cài đặt docker, chạy:

        sudo yum install docker
5. Thêm tư cách thành viên nhóm cho người dùng jenkins mặc định để bạn có thể chạy tất cả các lệnh docker mà không cần sử dụng lệnh sudo:

        sudo usermod -a -G docker jenkins
6. Kích hoạt dịch vụ docker khi khởi động AMI:

        sudo systemctl enable docker.service
7. Khởi động dịch vụ Docker:

        sudo systemctl start docker.service
8. Nhận trạng thái dịch vụ docker trên phiên bản AMI của bạn, chạy:

        sudo systemctl status docker.service
Outputs:

      docker.service - Docker Application Container Engine
      Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
      Active: active (running) since Wed 2021-09-08 05:03:52 EDT; 18s ago
      Docs: https://docs.docker.com
      Process: 3295 ExecStartPre=/usr/libexec/docker/docker-setup-runtimes.sh (code=exited, status=0/SUCCESS)
      Process: 3289 ExecStartPre=/bin/mkdir -p /run/docker (code=exited, status=0/SUCCESS)
      Main PID: 3312 (dockerd)
      Tasks: 9
      Memory: 39.9M
      CGroup: /system.slice/docker.service
      └─3312 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/c...
      
      Sep 08 05:03:51 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:51 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:51 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:51 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:52 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:52 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:52 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:52 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Sep 08 05:03:52 amazon.example.local systemd[1]: Started Docker Applicatio...
      Sep 08 05:03:52 amazon.example.local dockerd[3312]: time="2021-09-08T05:03...
      Hint: Some lines were ellipsized, use -l to show in full.

## 4. Configuring Jenkins
Jenkins hiện đã được cài đặt và chạy trên phiên bản EC2 của bạn. Để định cấu hình Jenkins:
1. Kết nối với http://<your_server_public_DNS>:8080 từ trình duyệt của bạn. Bạn sẽ có thể truy cập Jenkins thông qua giao diện quản lý của nó:
   ![unlock_jenkins.png](/aws-stutdy-group-workshop/images/2.2/unlock_jenkins.png)[Mật khẩu Jenkins](https://www.jenkins.io/doc/book/resources/tutorials/AWS/unlock_jenkins.png)
2. Mở file password default của Jenkins tại  /var/lib/jenkins/secrets/initialAdminPassword.

Sử dụng lệnh sau để hiển thị mật khẩu này:

    [ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
3. Tập lệnh cài đặt Jenkins hướng bạn đến trang Tùy chỉnh Jenkins. Nhấp vào Cài đặt các plugin được đề xuất.
4. Sau khi quá trình cài đặt hoàn tất, Tạo người dùng quản trị viên đầu tiên sẽ mở ra. Nhập thông tin của bạn rồi chọn Lưu và tiếp tục.
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.2/create_admin_user.png)
5. Ở phía bên trái, chọn Quản lý Jenkins rồi chọn Quản lý plugin.
6. Chọn tab Có sẵn, sau đó nhập plugin Amazon EC2 ở trên cùng bên phải.

7. Chọn hộp kiểm bên cạnh plugin Amazon EC2, sau đó chọn Cài đặt mà không cần khởi động lại.
   ![unlock_jenkins.png](/aws-stutdy-group-workshop/images/2.2/unlock_jenkins.png)
8. Sau khi cài đặt xong, hãy chọn Quay lại Bảng điều khiển.
9. Chọn Định cấu hình đám mây nếu không có nút hoặc đám mây nào hiện có.
   ![configure_cloud.png](/aws-stutdy-group-workshop/images/2.2/configure_cloud.png)
   Chúng ta gần như đã hoàn tất việc định cấu hình Jenkins trên Bastion Host
## 3. Install require plugins for Jenkins
Nhấp để **cài đặt các plugin được đề xuất**
![selected-plugsin.png](/aws-stutdy-group-workshop/images/2.2-jenkins/suggest-plugins.png)
![selected-plugsin.png](/aws-stutdy-group-workshop/images/2.2-jenkins/require-plugins.png)

## 4. Cấu hình thông tin xác thực aws trên Máy chủ Bastion
1. Sử dụng lệnh này để định cấu hình thông tin xác thực. Theo mặc định, aws-cli luôn có sẵn trên EC2, chúng ta không cần cài đặt lại aws-cli.

         aws configure

Output:

      aws configure
      AWS Access Key ID [****************]: ****************
      AWS Secret Access Key [****************r]: ****************
      Default region name [us-east-1]: us-east-1
      Default output format [None]: 
## 5. Install helm on Bastion Host
In this project, we will using Helm Chart to manage kubernetes object on EKS Cluster and Jenkins using helm command to apply this.

1. cài đặt các tệp nhị phân bằng các lệnh sau.

         curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh
         chmod 700 get_helm.sh
         ./get_helm.sh

2. Xem phiên bản Helm mà bạn đã cài đặt.

         helm version | cut -d + -f 1
