---
title : "Tạo project INTELLIJ"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

#### Các bước:

1. Tạo project Java trên Intellj IDEA

   - Mở Intellij IDEA và chọn **Create New Project
   - **Chọn các mục theo ảnh**

![alt text](/images/2.2/image-1.png)
   - Ở phần bên trái, chọn loại project (Java, Spring…  Với các ngôn ngữ khác như Node.js, Python thì bạn cài cài plugin nó mới hiện ra)
   - Ở phần bên phải trọn thư viện hoặc framework sử dụng (Trong ví dụ này mình viết chương trình Hello World nên không cần thư viện hay framework gì cả)
   - Trong mục Project SDK thì các bạn trỏ tới folder cài đặt Java hoặc sử dụng SDK có sẵn của Intellij đều được.

![alt text](/images/2.2/image-3.png)
![alt text](/images/2.2/image-4.png)
- **Nhập tên Project**

![alt text](/images/2.2/image-5.png)

- **Kết quả: Project HelloWorld được tạo ra với cấu trúc như sau:**

![alt text](/images/2.2/image-6.png)

- Tiếp theo, tạo file java cho project. Click chuột phải vào folder **src** và chọn **New/Java Class**

![alt text](/images/2.2/image-7.png)

- Nhập tên class. (nếu sử dụng dấu chấm thì nó sẽ hiểu phần trước đó là package)

- Ví dụ **stackjava.com.helloworld.Hello** thì nó sẽ tạo package **stackjava.com.helloworld** trong folder src và tạo file **Hello.java** trong package đó.

![alt text](/images/2.2/image-8.png)

- Kết quả :

![alt text](/images/2.2/image-9.png)

- Tiếp theo viết chương trình in ra dòng chữ **Hello World!** vào filde **Hello.java**

![alt text](/images/2.2/image-10.png)

- Chạy file **Hello.java** (click chuột phải vào file Hello và chọn **Run 'Hello.main()'**)

![alt text](/images/2.2/image-11.png)

- Kết quả: 

![alt text](/images/2.2/image-12.png)

- **Okay, Done!**
