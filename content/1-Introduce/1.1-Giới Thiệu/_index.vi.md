---
title : "Lý Thuyết về Docker"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---

### Nội Dung
- Docker là gì?
- Tại sao nên sử dụng Docker
- Lợi ích của Docker
- Một số khái niệm
- Dockerfile là gì?
- Docker compose
- So sánh image và container

#### **1. Docker là gì?**

- Docker là một nền tảng cho developers và system admin để develop, deploy và run application với container. Nó cho phép tạo các môi trường độc lập và tách biệt để khởi chạy và phát triển ứng dụng và môi trường này được gọi là container. Khi cần deploy lên bất kỳ server nào chỉ cần run container của Docker thì application của bạn sẽ được khởi chạy ngay lập tức.
- Xây dựng một lần, chạy mọi nơi Hoặc nói một cách đơn giản: Khi chúng ta muốn chạy ứng dụng, chúng ta phải thiết lập một môi trường chạy cho nó. Thay vì cài đặt một môi trường chạy cho nó, chúng ta sẽ chạy docker.

![alt text](/images/1.1/image-001.png)

#### **2.Tại sao nên sử dụng Docker**

- Như bạn đã từng triển khai một phần mềm, việc cài đặt môi trường khá là vất vả, và rất vất vả nếu như có xung đột trong hệ thống. Ví dụ như làm khi làm Machine Learning, ta cần phiên bản python phù hợp với các thư viện của tensorflow, numpy... môi trường ở trên máy công ty, khác với môi trường trên máy cá nhân của bạn, và như vậy để làm việc tại nhà trên dự án công ty, bạn phải build lại môi trường. Và cứ như thế, rất mất nhiều thời gian và công sức.
- Với Docker, các cấu hình được phân biệt với quản lý tài nguyên và việc triển khai là không đáng kể. Chỉ cần đơn giản chạy lệnh **docker run** là tất cả mọi thứ đã sẵn sàng cho chúng ta trải nghiệm.


#### **3.Lợi ích của Docker**

- Không như máy ảo Docker start và stop chỉ trong vài giây.
- Bạn có thể khởi chạy container trên mỗi hệ thống mà bạn muốn.
- Container có thể build và loại bỏ nhanh hơn máy ảo.
- Dễ dàng thiết lập môi trường làm việc. Chỉ cần config 1 lần duy nhất và không bao giờ phải cài đặt lại các dependencies. Nếu bạn thay đổi máy hoặc có người mới tham gia vào project thì bạn chỉ cần lấy config đó và đưa cho họ.
- Nó giữ cho word-space của bạn sạch sẽ hơn khi bạn xóa môi trường mà ảnh hưởng đến các phần khác.
 
#### **4.Một số khái niệm**

![alt text](/images/1.1/image-002.png)

- **Docker Client**: là cách mà bạn tương tác với docker thông qua command trong terminal. Docker Client sẽ sử dụng API gửi lệnh tới Docker Daemon.

- **Docker Daemon**: là server Docker cho yêu cầu từ Docker API. Nó quản lý images, containers, networks và volume.
- **Docker Volumes**: là cách tốt nhất để lưu trữ dữ liệu liên tục cho việc sử dụng và tạo apps.
- **Docker Registry**: là nơi lưu trữ riêng của Docker Images. Images được push vào registry và client sẽ pull images từ registry. Có thể sử dụng registry của riêng bạn hoặc registry của nhà cung cấp như : AWS, Google Cloud, Microsoft Azure.
- **Docker Hub**: là Registry lớn nhất của Docker Images ( mặc định). Có thể tìm thấy images và lưu trữ images của riêng bạn trên Docker Hub ( miễn phí).
- **Docker Repository**: là tập hợp các Docker Images cùng tên nhưng khác tags. VD: golang:1.11-alpine.
- **Docker Networking**: cho phép kết nối các container lại với nhau. Kết nối này có thể trên 1 host hoặc nhiều host.
- **Docker Compose**: là công cụ cho phép run app với nhiều Docker containers 1 cách dễ dàng hơn. Docker Compose cho phép bạn config các command trong file docker-compose.yml để sử dụng lại. Có sẵn khi cài Docker.
- **Docker Swarm**: để phối hợp triển khai container.
- **Docker Services**: là các containers trong production. 1 service chỉ run 1 image nhưng nó mã hoá cách thức để run image — sử dụng port nào, bao nhiêu bản sao container run để service có hiệu năng cần thiết và ngay lập tức.

#### **5.Dockerfile là gì?**

- **Dockerfile** là tệp cấu hình để Docker xây dựng hình ảnh. Nó sử dụng một hình ảnh cơ sở để xây dựng lớp hình ảnh ban đầu. Một số hình ảnh cơ bản: python, unbutu và alpine. Sau đó, nếu có các lớp bổ sung, nó sẽ được xếp chồng lên trên lớp cơ sở. Cuối cùng, một lớp mỏng có thể được xếp chồng lên trên các lớp trước đó khác.

- **Các config:**

- **FROM** — chỉ định image gốc: python, unbutu, alpine…
- **LABEL** — cung cấp metadata cho image. Có thể sử dụng để add thông tin maintainer. Để xem các label của images, dùng lệnh docker inspect.
- **ENV** — thiết lập một biến môi trường.
- **RUN** — Có thể tạo một lệnh khi build image. Được sử dụng để cài đặt các package vào container.
- **COPY** — Sao chép các file và thư mục vào container.
- **ADD** — Sao chép các file và thư mục vào container.
- **CMD** — Cung cấp một lệnh và đối số cho container thực thi. Các tham số có thể được ghi đè và chỉ có một CMD.
- **WORKDIR** — Thiết lập thư mục đang làm việc cho các chỉ thị khác như: RUN, CMD, ENTRYPOINT, COPY, ADD,…
- **ARG** — Định nghĩa giá trị biến được dùng trong lúc build image.
- **ENTRYPOINT** — cung cấp lệnh và đối số cho một container thực thi.
- **EXPOSE** — khai báo port lắng nghe của image.
- **VOLUME** — tạo một điểm gắn thư mục để truy cập và lưu trữ data.

#### **6.So sánh image và container**

![alt text](/images/1.1/image-004.png)




