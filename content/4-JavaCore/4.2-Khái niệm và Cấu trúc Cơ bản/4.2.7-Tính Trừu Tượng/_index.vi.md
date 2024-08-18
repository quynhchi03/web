---
title : "Tính Trừu Tượng (Abstraction)"
date :  "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 4.2.7 </b> "
---

#### Tính Trừu Tượng

- Giúp đơn giản hóa và tổ chức mã nguồn bằng cách tập trung vào các đặc điểm quan trọng và ẩn đi các chi tiết không cần thiết. 
- Trừu tượng cho phép bạn làm việc với các đối tượng và lớp mà không cần phải biết chi tiết cài đặt bên trong của chúng.

#### Lợi ích của tính trừu tượng:
- **Giảm Độ Phức Tạp:**
Trừu tượng giúp giảm độ phức tạp bằng cách ẩn đi các chi tiết thực hiện không cần thiết và chỉ cung cấp những phương thức và thuộc tính cần thiết để người dùng tương tác với đối tượng.

- **Tăng Tính Tái Sử Dụng:**
Các lớp trừu tượng và giao diện cho phép tái sử dụng mã một cách hiệu quả. Các lớp con có thể kế thừa hoặc triển khai các lớp trừu tượng và giao diện mà không cần phải biết chi tiết cài đặt của các lớp khác.

- **Dễ Dàng Mở Rộng:**
Tính trừu tượng làm cho việc mở rộng hệ thống trở nên dễ dàng hơn. Bạn có thể thêm các lớp mới hoặc thay đổi các lớp hiện tại mà không làm ảnh hưởng đến các phần khác của chương trình.

- **Cải Thiện Tính Tinh Vi:**
Bằng cách sử dụng trừu tượng, bạn có thể thiết kế các hệ thống với các giao diện đơn giản và dễ hiểu, giúp cải thiện tính tinh vi và khả năng bảo trì của mã nguồn.

#### Các khía cạnh chính của tính trừu tượng:
**1. Lớp Trừu Tượng (Abstract Class):**

- Một lớp trừu tượng là một lớp không thể được khởi tạo trực tiếp và có thể chứa các phương thức không có cài đặt (abstract methods). Các lớp con kế thừa lớp trừu tượng phải triển khai các phương thức trừu tượng đó.
- Lớp trừu tượng thường được sử dụng để định nghĩa một giao diện chung cho các lớp con và cung cấp một khuôn mẫu cho các lớp con thực hiện các hành vi cụ thể.
- **VD:**
```
abstract class Animal {
    abstract void makeSound(); // Phương thức trừu tượng không có cài đặt
    
    void sleep() { // Phương thức cụ thể có cài đặt
        System.out.println("This animal sleeps");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound(); // Xuất ra "Dog barks"
        myDog.sleep(); // Xuất ra "This animal sleeps"
    }
}
```

**2. Giao Diện (Interface):**

- Một giao diện là một tập hợp các phương thức trừu tượng (trong Java 8 và các phiên bản sau, giao diện cũng có thể chứa các phương thức cụ thể với default và static). Các lớp khác có thể triển khai giao diện này và cung cấp cài đặt cho các phương thức được định nghĩa trong giao diện.
- Giao diện giúp định nghĩa một hợp đồng mà các lớp phải tuân theo mà không cần biết chi tiết cài đặt.
- **VD:**
```
interface Animal {
    void makeSound();
}

class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myCat = new Cat();
        myCat.makeSound(); // Xuất ra "Cat meows"
    }
}
```

