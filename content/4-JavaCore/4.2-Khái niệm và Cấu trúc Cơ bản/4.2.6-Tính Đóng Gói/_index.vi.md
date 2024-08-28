---
title : "Tính đóng gói (Encapsulation)"
date :  "`r Sys.Date()`"
weight : 6 
chapter : false
pre : " <b> 1.2.6 </b> "
---

#### Tính Đóng gói

- Giúp bảo vệ dữ liệu và kiểm soát cách mà dữ liệu đó được truy cập và thay đổi
- Tính đóng gói liên quan đến việc gói gọn dữ liệu và phương thức xử lý dữ liệu đó vào trong một đơn vị gọi là lớp (class), và chỉ cho phép truy cập vào dữ liệu thông qua các phương thức công khai (public methods) được cung cấp.

#### Lợi ích của tính đóng gói:
- **Bảo Mật Dữ Liệu:**
Đóng gói giúp bảo vệ dữ liệu bên trong lớp, ngăn không cho dữ liệu bị thay đổi trực tiếp bởi mã bên ngoài. Điều này làm giảm nguy cơ lỗi và bảo vệ dữ liệu khỏi các thao tác không mong muốn.

- **Kiểm Soát Truy Cập:**
Thông qua việc cung cấp các phương thức truy cập (getter và setter), lớp có thể kiểm soát cách mà dữ liệu được truy cập và thay đổi. Ví dụ, trong phương thức setter, bạn có thể kiểm tra tính hợp lệ của giá trị trước khi gán nó cho biến thành viên.

- **Dễ Dàng Bảo Trì:**
Đóng gói giúp mã dễ bảo trì và sửa chữa hơn vì các thay đổi có thể được thực hiện bên trong lớp mà không ảnh hưởng đến các phần khác của chương trình.

- **Tăng Tính Tái Sử Dụng:**
Bằng cách tổ chức dữ liệu và hành vi của nó trong một lớp, bạn có thể tái sử dụng các lớp trong các phần khác của chương trình mà không cần phải biết chi tiết cài đặt bên trong.

#### Các thành phần chính của tính đóng gói:

**1. Biến Thành Viên Riêng Tư (Private Variables):**

- Biến thành viên của lớp thường được khai báo với mức truy cập private, điều này có nghĩa là chúng không thể được truy cập trực tiếp từ bên ngoài lớp. Việc này giúp bảo vệ dữ liệu và ngăn chặn việc sửa đổi không mong muốn từ bên ngoài.
- **VD:**
```
public class Person {
    private String name;
    private int age;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getter for name
    public String getName() {
        return name;
    }

    // Setter for name
    public void setName(String name) {
        this.name = name;
    }

    // Getter for age
    public int getAge() {
        return age;
    }

    // Setter for age
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }
}
```

**=> Các biến name và age được khai báo là private, và việc truy cập hoặc thay đổi giá trị của chúng được thực hiện thông qua các phương thức công khai getName, setName, getAge, và setAge.**

**2. Phương Thức Công Khai (Public Methods):**

- Phương thức công khai (public methods) là những phương thức mà các đối tượng khác có thể gọi để thực hiện các hành động hoặc truy cập dữ liệu của lớp. Những phương thức này cung cấp các điểm kiểm soát để đảm bảo rằng dữ liệu được xử lý đúng cách.
- Trong ví dụ trên, các phương thức getName, setName, getAge, và setAge là công khai và cho phép các đối tượng tương tác với dữ liệu của lớp Person.


