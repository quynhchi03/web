---
title : "Docker compose"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

#### **Docker compose**

- **Docker compose** là công cụ dùng để định nghĩa và run multi-container cho Docker application. Với compose bạn sử dụng file YAML để config các services cho application của bạn. Sau đó dùng command để create và run từ những config đó. Sử dụng cũng khá đơn giản chỉ với ba bước:

+ Khai báo app’s environment trong Dockerfile.
+ Khai báo các services cần thiết để chạy application trong file docker-compose.yml.
+ Run docker-compose up để start và run app.

- **Docker Compose** là một công cụ giúp quản lý các container Docker trong một ứng dụng. Với Docker Compose, bạn có thể dễ dàng quản lý các container của ứng dụng mà không cần phải khởi động một container một cách thủ công.

**=> Hiểu đơn giản: Docker compose là công cụ giúp chạy 1 lúc nhiều container**

![alt text](/web/images/1.1/image-003.png)

- Không giống như Dockerfile (build các image). Docker compose dùng để build và run các container. Các thao tác của docker-compose tương tự như lệnh: docker run.

- Docker compose cho phép tạo nhiều service(container) giống nhau bằng lệnh: **$ docker-compose scale <tên service> = <số lượng>**

#### **Các tính năng của Docker Compose**
- Docker Compose cung cấp nhiều tính năng hữu ích để giúp bạn quản lý các ứng dụng của mình. Dưới đây là một số tính năng quan trọng của Docker Compose:

+ **Định nghĩa dịch vụ**: Bạn có thể định nghĩa các dịch vụ khác nhau và cấu hình chúng bằng cách sử dụng Docker Compose. Ví dụ: bạn có thể định nghĩa một dịch vụ database và một dịch vụ web để triển khai ứng dụng của mình.
+ **Tự động tạo container**: Docker Compose sẽ tự động tạo các container cần thiết để triển khai ứng dụng của bạn. Nó sẽ tạo các container dựa trên cấu hình mà bạn đã định nghĩa.
+ **Quản lý mạng**: Docker Compose cung cấp các công cụ để quản lý mạng cho các container. Bạn có thể định nghĩa các mạng riêng để giữ cho các container của bạn an toàn và đảm bảo chúng không bị tấn công từ bên ngoài.
+ **Quản lý lưu trữ**: Bạn có thể định nghĩa các khối lượng lưu trữ để sử dụng cho các container. Docker Compose sẽ giúp bạn quản lý các khối lượng lưu trữ này và đảm bảo chúng được lưu trữ và quản lý một cách an toàn và hiệu quả.
+ **Tích hợp với Docker Swarm**: Docker Compose có thể tích hợp với Docker Swarm để triển khai ứng dụng của bạn trên một cụm máy chủ Docker. Điều này giúp bạn quản lý và mở rộng các ứng dụng của mình một cách dễ dàng.
+ **Khả năng mở rộng**: Docker Compose cho phép bạn mở rộng ứng dụng của mình bằng cách thêm các dịch vụ mới hoặc tăng số lượng container cho các dịch vụ hiện có. Điều này giúp bạn quản lý tốt hơn sự tăng trưởng của ứng dụng của mình.

#### **Những lưu ý quan trọng khi sử dụng Docker Compose**
- **Đặt tên cho các container**: Để dễ dàng quản lý các container, bạn nên đặt tên cho chúng. Điều này sẽ giúp bạn xác định được container nào đang chạy trong ứng dụng của bạn.
- **Sử dụng mạng riêng**: Khi sử dụng Docker Compose, bạn nên sử dụng một mạng riêng để giữ cho các container của bạn an toàn và được cô lập khỏi mạng bên ngoài.
- **Sử dụng các biến môi trường**: Sử dụng các biến môi trường trong tệp YAML của bạn để tránh lưu trữ các thông tin nhạy cảm trong tệp YAML. Các biến môi trường có thể được đặt trong một tệp .env riêng biệt.
- Để tránh xung đột khi khởi động container, bạn nên đặt các cổng cho container của mình trong **tệp YAML**. Bạn nên sử dụng cổng được khuyến nghị của Docker.
- Các lệnh Docker Compose có thể được thực thi thông qua một Makefile. Điều này giúp cho việc sử dụng Docker Compose trở nên đơn giản và hiệu quả hơn.

#### **Các bước sử dụng Docker Compose**

- **Bước 1: Tạo tệp YAML**: Tạo một tệp YAML để định nghĩa các container
- **Bước 2: Khởi động các container**: Sau khi chúng ta đã định nghĩa các container trong tệp YAML, chúng ta có thể sử dụng lệnh **docker-compose up** để khởi động các container của chúng ta. Docker Compose sẽ tự động tải xuống các hình ảnh và khởi động các container cho chúng ta.
- **Bước 3: Kiểm tra trạng thái của các container**:Sau khi chúng ta đã khởi động các container, chúng ta có thể sử dụng lệnh **docker-compose ps** để kiểm tra trạng thái của các container.
- **Bước 4: Dừng các container**:Khi chúng ta đã hoàn thành việc sử dụng các container, chúng ta có thể sử dụng lệnh **docker-compose down** để dừng các container.

#### **Câu hỏi thường gặp**
1. **Docker Compose hoạt động như thế nào?**
- Docker Compose hoạt động bằng cách định nghĩa các dịch vụ trong file docker-compose.yml. Sau đó, Docker Compose sẽ sử dụng các thông tin này để khởi tạo và quản lý các container tương ứng.

2. **Docker Compose có thể được sử dụng để triển khai các ứng dụng lớn không?**
- Docker Compose có thể được sử dụng để triển khai các ứng dụng lớn, nhưng nó không phải là giải pháp tối ưu cho các ứng dụng lớn và phức tạp. Đối với các ứng dụng lớn và phức tạp hơn, bạn có thể muốn sử dụng các công cụ khác như Kubernetes hoặc Docker Swarm để quản lý các container của bạn.

3. **Docker Compose có hỗ trợ đa môi trường không?**
- Docker Compose có thể hỗ trợ đa môi trường bằng cách sử dụng các tệp docker-compose.yml khác nhau cho mỗi môi trường. Bằng cách định nghĩa các biến môi trường trong tệp docker-compose.yml và sử dụng các biến này để định nghĩa các cài đặt khác nhau cho mỗi môi trường, bạn có thể triển khai các ứng dụng Docker của mình trên nhiều môi trường khác nhau một cách dễ dàng.