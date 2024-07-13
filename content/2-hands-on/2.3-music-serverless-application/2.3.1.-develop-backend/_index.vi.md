---
title : "Phát triển hệ thống Backend"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.3.1 </b> "
---
## Giới thiệu:
Trong thử thách này, hệ thống phụ trợ là thành phần cốt lõi của Ứng dụng Music Serverless. Nó chịu trách nhiệm xử lý tất cả logic nghiệp vụ, xử lý yêu cầu, quản lý dữ liệu và đảm bảo ứng dụng hoạt động trơn tru. Phần phụ trợ sẽ được xây dựng bằng Java và khung Spring Boot, tận dụng nhiều dịch vụ AWS khác nhau để đảm bảo khả năng mở rộng, độ tin cậy và hiệu suất.
## Mã nguồn: https://github.com/daotq2000/spotify-be-public
Bạn có thể kiểm tra mã nguồn của mình tại github, về cấu trúc chi tiết, quy trình và cách build Rest API với Spring Boot Framework
## Tài nguyên cần thiết:
**- Công cụ phát triển:**
+ IDE: IntelliJ IDEA hoặc Eclipse để phát triển Java.
+ Build Tool: Maven hoặc Gradle để quản lý các phụ thuộc của dự án và xây dựng ứng dụng.
+ Kiểm soát phiên bản: Git để quản lý và cộng tác mã nguồn.
+ Containerization: Docker tạo container image của ứng dụng backend.

**Dịch vụ AWS:**

+ Amazon Fargate: Để triển khai và quản lý ứng dụng phụ trợ được đóng gói trong container.
+ Amazon Aurora MySQL: Để quản lý cơ sở dữ liệu, mang lại hiệu suất và tính sẵn sàng cao.
+ Amazon ElastiCache (Redis): Dùng để đệm các dữ liệu thường xuyên truy cập nhằm cải thiện hiệu suất ứng dụng.
+ Application Load Balancer (ALB): Để phân phối lưu lượng truy cập đến trên nhiều phiên bản.
+ Internet Gateway: Để cho phép ứng dụng truy cập internet.
+ Auto Scaling Group: Để tự động điều chỉnh số lượng instance đang chạy theo nhu cầu.

**-Cơ sở hạ tầng dưới dạng Mã:**
+ Terraform: Để xác định và cung cấp cơ sở hạ tầng AWS, đảm bảo môi trường nhất quán và có thể tái tạo.
### Phát triển ngôn ngữ:
+ Ngôn ngữ chính: Java
+ Khung: Khởi động mùa xuân

**Phụ thuộc chính:**

+ Spring Web: Dùng để xây dựng các dịch vụ web RESTful.
+ Spring Data JPA: Dùng để truy cập cơ sở dữ liệu và ORM.
+ Spring Security: Để xác thực và ủy quyền.
+ Spring Cache: Dùng để tích hợp với Redis và cache data.
+ MySQL Driver: Dùng để kết nối với cơ sở dữ liệu Amazon Aurora MySQL.
+ Redis Client: Dùng để tương tác với Amazon ElastiCache (Redis).
+ Cloudinary: Để lưu file, tài nguyên media.

#### Quá trình phát triển:
1.Thiết lập dự án:

- Khởi tạo một dự án Spring Boot mới với các phụ thuộc cần thiết.
- Thiết lập kiểm soát phiên bản bằng Git và tạo kho lưu trữ.

2. Phát triển API:

- Xác định điểm cuối RESTful cho các chức năng khác nhau như quản lý người dùng, phát nhạc trực tuyến, tạo danh sách phát, v.v.

- Triển khai logic lớp dịch vụ để xử lý các quy trình nghiệp vụ.

- Tạo các lớp kho lưu trữ cho các tương tác cơ sở dữ liệu bằng Spring Data JPA.

3.Tích hợp cơ sở dữ liệu:
- Cấu hình ứng dụng để kết nối với Amazon Aurora MySQL.
- Xác định các thực thể và kho lưu trữ JPA để lập mô hình và truy cập dữ liệu.
- Thực hiện các kịch bản xác thực và di chuyển dữ liệu nếu cần thiết.

4. Bộ nhớ đệm:

- Tích hợp Redis để lưu trữ dữ liệu thường xuyên truy cập.
- Cấu hình Spring Cache để sử dụng Redis làm nhà cung cấp cache.
- Thực hiện các chiến lược bộ nhớ đệm để tối ưu hóa hiệu suất.

5. Bảo mật:

- Triển khai xác thực và ủy quyền bằng Spring Security.
- Định cấu hình JWT (Mã thông báo Web JSON) để xác thực an toàn và không trạng thái.

6.Kiểm tra:
- Viết bài kiểm tra đơn vị cho từng thành phần riêng lẻ bằng JUnit và Mockito.
- Thực hiện các thử nghiệm tích hợp để đảm bảo chức năng end-to-end.

7.Container hóa:

- Tạo Dockerfile để chứa ứng dụng Spring Boot.
- Xây dựng và thử nghiệm Docker image cục bộ.

8. Triển khai:

- Sử dụng tập lệnh Terraform để cung cấp tài nguyên AWS (Fargate, Aurora MySQL, ElastiCache, ALB, v.v.).
- Triển khai ứng dụng được đóng gói lên Amazon Fargate.
- Định cấu hình Cân bằng tải ứng dụng và Nhóm tự động thay đổi quy mô để có tính khả dụng và khả năng mở rộng cao.

9.Kết quả đạt được:

**Hệ thống phụ trợ mạnh mẽ:**

Một hệ thống phụ trợ đầy đủ chức năng được phát triển bằng Java và Spring Boot, có khả năng xử lý nhiều chức năng ứng dụng âm nhạc khác nhau.
Cơ sở hạ tầng có thể mở rộng và đáng tin cậy:

Kiến trúc triển khai dựa trên AWS đảm bảo tính sẵn sàng, khả năng mở rộng và độ tin cậy cao bằng cách sử dụng các dịch vụ như Fargate, Aurora MySQL, ElastiCache và ALB.
Hiệu suất được cải thiện:

Tối ưu hóa khả năng truy cập dữ liệu và hiệu suất ứng dụng thông qua các chiến lược bộ nhớ đệm hiệu quả với Redis.
Bảo mật và xác thực:

Cơ chế xác thực và ủy quyền người dùng an toàn được triển khai bằng Spring Security và JWT.
Quản lý cơ sở hạ tầng tự động:

Cơ sở hạ tầng dưới dạng mã (IaC) sử dụng Terraform, cho phép cung cấp tài nguyên AWS một cách tự động và nhất quán.
Tài liệu và kiểm tra toàn diện:

Tài liệu chi tiết về hệ thống phụ trợ, quy trình thiết lập và các bước triển khai.
Kiểm tra kỹ lưỡng để đảm bảo độ tin cậy và tính chính xác của ứng dụng.
Bằng cách hoàn thành quá trình phát triển phụ trợ này, bạn sẽ có nền tảng vững chắc cho Ứng dụng Music Serverless, có khả năng xử lý lưu lượng truy cập trong thế giới thực và mở rộng quy mô hiệu quả trên AWS.