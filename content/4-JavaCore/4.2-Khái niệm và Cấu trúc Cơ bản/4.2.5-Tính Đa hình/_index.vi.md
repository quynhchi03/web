---
title : "Tính đa hình (Polymorphism) "
date :  "`r Sys.Date()`"
weight : 5 
chapter : false
pre : " <b> 4.2.5 </b> "
---

#### Tính Đa Hình

- Cho phép một đối tượng có thể được xử lý theo nhiều cách khác nhau. 
- Cho phép các phương thức có cùng tên hoạt động khác nhau tùy thuộc vào loại đối tượng mà chúng thuộc về. 

#### Lợi ích của Đa hình
- **Tính linh hoạt và mở rộng:** Bạn có thể thêm các lớp mới mà không cần thay đổi mã nguồn đã có.
- **Giảm thiểu mã lặp lại:** Có thể viết mã một lần cho một phương thức và sau đó mở rộng cho các lớp khác.
- **Cải thiện khả năng bảo trì:** Dễ dàng thay đổi triển khai mà không làm thay đổi mã khách hàng.

#### Chia thành 2 loại : 

**1. Đa hình thời gian biên dịch (Compile-time polymorphism) hay còn gọi là Overloading:**

- **Phương thức Overloading:** Được thực hiện khi nhiều phương thức trong cùng một lớp có cùng tên nhưng khác nhau về số lượng hoặc kiểu tham số. - **Ví dụ:**
```
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```
**=> Phương thức "add" với nhiều tham số khác nhau**

**2. Đa hình thời gian chạy (Runtime polymorphism) hay còn gọi là Overriding:**

- **Phương thức Overriding:** Xảy ra khi một lớp con cung cấp một triển khai cụ thể cho một phương thức đã được định nghĩa trong lớp cha của nó. Điều này cho phép lớp con thay đổi hành vi của phương thức từ lớp cha. 
- **Ví dụ:**
```
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
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
        Animal myAnimal = new Dog(); // Tính đa hình ở đây
        myAnimal.makeSound(); // Xuất ra "Dog barks"
    }
}
```
**=> Phương thức makeSound được ghi đè (overridden) trong lớp Dog, và khi gọi phương thức từ một đối tượng của lớp Dog, hành vi của phương thức sẽ là của lớp Dog, không phải của lớp Animal.**


