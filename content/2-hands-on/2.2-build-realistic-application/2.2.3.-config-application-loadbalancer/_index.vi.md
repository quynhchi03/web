---
title : "Cấu hình tài nguyên AWS"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.2.3 </b> "
---
Mặc dù chúng tôi đã thiết lập tài nguyên AWS theo địa hình nhưng chúng chứa nhiều thành phần, có độ phức tạp lớn nhưng
chúng tôi thậm chí cần phải định cấu hình một số tài nguyên để ứng dụng hoạt động mà không gặp lỗi.
## 1. Cấu hình nhóm bảo mật để liên lạc giữa các tài nguyên
Ý của bước này là cho phép liên lạc giữa các tài nguyên trong mạng con riêng tư, theo mặc định, các tài nguyên trong mạng con riêng tư sẽ
từ chối mọi kết nối nếu chúng tôi không có cấu hình bảo mật.

Bước cấu hình được chuyển tới **AWS console => EC2 => Security Group**
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/sg-eks-remote.png)
###  Edit inbound rules
Click Edit inbound rules
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/inbound.png)
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/inbound1.png)

Inbound configure successfully
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/config-inboumd-success.png)

###  Edit outbound rules
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/outbound.png)
![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/outboundSuccessfully.png)

## 2. Cấu hình nhóm mục tiêu cho Application Load Balancer
Mục tiêu cấu hình cho bộ cân bằng tải, bộ cân bằng tải sẽ chuyển tiếp yêu cầu từ cloudfront đến Nginx-Controller bên trong
Cụm EKS.
Thực hiện theo các bước:
1. Click vào `alb-target-group`
   ![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/configALB.png)
2. Register target group
   ![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/config-targetGroup.png)
- Port `30080` là NodePort của Nginx Controller.
3. At tab Health checks, click to `Edit`
   ![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/success-config-alb.png)
   ![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/config-heathy.png)
4. Config heath check successfully
   ![create_admin_user.png](/aws-stutdy-group-workshop/images/2.4-config/success-config-alb.png)

Sau khi cấu hình kiểm tra tình trạng thành công, bộ cân bằng tải ứng dụng sẽ chuyển tiếp yêu cầu tới bộ điều khiển nginx.