---
title : "Annotation là gì"
date :  "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

#### Annotation

- **Annotation (chú thích)** là một loại cơ chế đặc biệt cho phép bạn thêm thông tin meta (dữ liệu) vào mã nguồn. Annotation không ảnh hưởng trực tiếp đến hoạt động của chương trình nhưng có thể được sử dụng để cung cấp thông tin bổ sung cho các công cụ, framework, hoặc trình biên dịch.

#### 1. Khái niệm cơ bản

- Annotation trong Java là một loại đối tượng, cho phép bạn gán thông tin bổ sung cho các lớp, phương thức, biến, và các thành phần khác của mã nguồn. Annotation được khai báo với ký hiệu **@** và có thể chứa các tham số.

#### 2. Cú pháp cơ bản

- Một annotation thường được khai báo như sau:
```
@AnnotationName(parameter = "value")
public class MyClass {
    // class body
}
```
- **AnnotationName: Tên của annotation.**
- **parameter: Các tham số tùy chọn có thể được chỉ định cho annotation.**