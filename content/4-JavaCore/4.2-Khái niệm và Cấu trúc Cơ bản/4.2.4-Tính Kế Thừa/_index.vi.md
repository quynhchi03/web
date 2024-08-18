---
title : "Tính kế thừa (inheritance)"
date :  "`r Sys.Date()`"
weight : 4 
chapter : false
pre : " <b> 4.2.4 </b> "
---

#### Tính Kế Thừa

- Là một cơ chế cho phép một lớp mới (lớp con) kế thừa các thuộc tính và phương thức từ một lớp hiện có (lớp cha). 
- Tính kế thừa giúp tái sử dụng mã nguồn, mở rộng chức năng của lớp hiện có, và tổ chức mã theo cấu trúc phân cấp.

#### Các Khái Niệm Cơ Bản về Kế Thừa
**1. Lớp Cha (Superclass):**
- Là lớp mà lớp con kế thừa từ nó. Lớp cha có thể là một lớp hiện có hoặc một lớp bạn tạo ra.

**2. Lớp Con (Subclass):**
- Là lớp kế thừa từ lớp cha. Lớp con có thể mở rộng hoặc thay đổi hành vi của lớp cha, cũng như có thể có thêm các thuộc tính và phương thức riêng.

**3. Từ Khóa extends:**
- Được sử dụng để chỉ định rằng một lớp kế thừa từ một lớp khác.
- **Cú Pháp: class Dog extends Animal**

**4. Tính Kế Thừa Đơn (Single Inheritance):**
- Một lớp con chỉ có thể kế thừa từ một lớp cha duy nhất

**5. Tính Kế Thừa Đa Cấp (Multilevel Inheritance):**
- Một lớp có thể kế thừa từ lớp con, tạo ra một chuỗi kế thừa.
- **Ví Dụ: Grandparent → Parent → Child**
**6. Tính Kế Thừa Hỗn Hợp (Hierarchical Inheritance):**
- Nhiều lớp con có thể kế thừa từ một lớp cha chung.
- **Ví Dụ: Parent → Child1, Parent → Child2**

**7. Tính Kế Thừa Đa (Multiple Inheritance):**
- Java không hỗ trợ kế thừa đa (một lớp kế thừa từ nhiều lớp cha) trực tiếp để tránh các vấn đề phức tạp như Diamond Problem. Tuy nhiên, Java hỗ trợ kế thừa từ nhiều giao diện (interfaces).

#### Ví Dụ về Kế Thừa và Cách sử dụng
```
// Lớp cha
public class Animal {
    // Thuộc tính của lớp cha
    private String name;

    // Constructor của lớp cha
    public Animal(String name) {
        this.name = name;
    }

    // Phương thức của lớp cha
    public void eat() {
        System.out.println(name + " is eating.");
    }

    // Phương thức getter cho thuộc tính name
    public String getName() {
        return name;
    }
}

// Lớp con kế thừa từ lớp Animal
public class Dog extends Animal {
    // Constructor của lớp con
    public Dog(String name) {
        super(name); // Gọi constructor của lớp cha
    }

    // Phương thức đặc trưng của lớp con
    public void bark() {
        System.out.println(getName() + " is barking.");
    }
}

public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng của lớp Dog
        Dog dog = new Dog("Buddy");

        // Sử dụng phương thức kế thừa từ lớp Animal
        dog.eat(); // In ra "Buddy is eating."

        // Sử dụng phương thức của lớp Dog
        dog.bark(); // In ra "Buddy is barking."
    }
}
```

#### Các Quy Tắc về Kế Thừa
- **Lớp Con Có Thể Ghi Đè Phương Thức:**
+ Lớp con có thể ghi đè (override) các phương thức của lớp cha để thay đổi hoặc mở rộng hành vi. Để ghi đè phương thức, lớp con sử dụng từ khóa **@Overrid
```
@Override
public void eat() {
    System.out.println(getName() + " is eating with a different style.");
}
```
- **Lớp Con Không Thể Ghi Đè Phương Thức final:**
 Phương thức được khai báo là final trong lớp cha không thể được ghi đè trong lớp con.

- **Lớp Con Không Thể Ghi Đè Phương Thức static:**
 Phương thức static không thể được ghi đè, mà chỉ có thể được ẩn (hiding) trong lớp con.

- **Lớp Con Có Thể Truy Cập Thành Phần protected và default:**
 Lớp con có thể truy cập các thành phần protected và default của lớp cha, nhưng không thể truy cập các thành phần private.


