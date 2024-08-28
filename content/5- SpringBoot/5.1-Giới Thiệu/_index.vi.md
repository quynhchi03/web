---
title : "Tổng Quan về SpringBoot"
date :  "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### 1. Khái niệm cơ bản
- Spring Boot là một framework mã nguồn mở cho phép tạo ra các ứng dụng Java độc lập, dễ triển khai, và cấu hình ít. Nó cung cấp một loạt các tính năng tích hợp sẵn, giúp đơn giản hóa quy trình phát triển ứng dụng.

#### 2. Các tính năng chính
- **Cấu hình tự động (Auto Configuration)**: Spring Boot tự động cấu hình các bean và thành phần của ứng dụng dựa trên các phụ thuộc trong classpath và các cấu hình mặc định.

- **Ứng dụng độc lập**: Spring Boot cho phép bạn tạo ra các ứng dụng Java độc lập, có thể chạy từ dòng lệnh mà không cần phải triển khai lên máy chủ ứng dụng.

- **Khởi tạo nhanh (Rapid Development)**: Spring Boot cung cấp các mẫu và khởi tạo dự án nhanh chóng thông qua các công cụ như Spring Initializr.

- **Quản lý phụ thuộc (Dependency Management)**: Spring Boot đi kèm với một bộ phụ thuộc được quản lý, giúp đảm bảo tính tương thích giữa các thư viện và phiên bản.

- **Hỗ trợ tích hợp (Integration)**: Có tích hợp sẵn với nhiều công nghệ khác như JPA, Hibernate, RabbitMQ, Kafka, và nhiều công cụ khác.

#### 3. Cấu trúc dự án

- Một dự án Spring Boot thường có cấu trúc cơ bản sau:

+ **src/main/java:** Chứa mã nguồn Java.
+ **src/main/resources:** Chứa tài nguyên (cấu hình, tệp mẫu, v.v.).
+ **src/test/java:** Chứa mã nguồn cho các bài kiểm tra.
+ **pom.xml hoặc build.gradle:** Quản lý các phụ thuộc của dự án (pom.xml cho Maven, build.gradle cho Gradle).

#### 4. Cách hoạt động

- Spring Boot khởi động ứng dụng bằng cách chạy phương thức main trong lớp chính được đánh dấu bằng @SpringBootApplication. Annotation này là sự kết hợp của @Configuration, @EnableAutoConfiguration, và @ComponentScan, giúp cấu hình và quét các thành phần của ứng dụng.

#### 5. Các thành phần cơ bản

+ **Controller:** Xử lý các yêu cầu web và trả về các phản hồi. Được đánh dấu bằng @RestController hoặc @Controller.
+ **Service:** Chứa logic nghiệp vụ, được đánh dấu bằng @Service.
+ **Repository:** Tương tác với cơ sở dữ liệu, được đánh dấu bằng @Repository.
+ **Configuration:** Các cấu hình đặc biệt của ứng dụng, được đánh dấu bằng @Configuration.

#### 6. Lợi ích

- **Tiết kiệm thời gian:** Giảm bớt công việc cấu hình và thiết lập môi trường.
- **Dễ triển khai:** Ứng dụng Spring Boot có thể đóng gói thành một JAR hoặc WAR file và dễ dàng triển khai.
- **Dễ mở rộng:** Tích hợp dễ dàng với các công nghệ và công cụ khác.
