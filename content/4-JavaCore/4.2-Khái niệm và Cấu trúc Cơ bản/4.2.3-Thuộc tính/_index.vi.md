---
title : "Thuộc tính (Attributes/Fields)"
date :  "`r Sys.Date()`"
weight : 3 
chapter : false
pre : " <b> 4.2.3 </b> "
---

#### Thuộc Tính
- là các biến được khai báo trong một lớp và đại diện cho trạng thái hoặc dữ liệu của các đối tượng của lớp đó. Các thuộc tính có thể có các mức độ truy cập khác nhau và có thể là các biến thể hiện (instance variables) hoặc biến tĩnh (static variables).

#### Khai Báo Thuộc Tính Trong Java
- Thuộc tính trong Java được khai báo bên trong lớp nhưng ngoài các phương thức. Cú pháp khai báo thuộc tính như sau:
```
[access_modifier] [static] [data_type] variable_name [= initial_value];
```
- **Access Modifier:** Quy định phạm vi truy cập của thuộc tính (ví dụ: public, protected, private). Nếu không chỉ định, thuộc tính có phạm vi truy cập mặc định.
- **Static:** Từ khóa static chỉ ra rằng thuộc tính thuộc về lớp thay vì thuộc về các đối tượng cụ thể.
- **Data Type:** Kiểu dữ liệu của thuộc tính (ví dụ: int, String, double).
- **Variable Name:** Tên của thuộc tính.
- **Initial Value:** Giá trị khởi tạo (tuỳ chọn).

#### Ví Dụ Về Khai Báo Và Sử Dụng Thuộc Tính

```
public class Person {
    // Thuộc tính instance (biến thể hiện)
    private String name;
    private int age;

    // Thuộc tính static
    public static int population;

    // Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        population++; // Tăng số lượng dân số mỗi khi một đối tượng mới được tạo
    }

    // Getter cho thuộc tính name
    public String getName() {
        return name;
    }

    // Setter cho thuộc tính name
    public void setName(String name) {
        this.name = name;
    }

    // Getter cho thuộc tính age
    public int getAge() {
        return age;
    }

    // Setter cho thuộc tính age
    public void setAge(int age) {
        this.age = age;
    }

    // Phương thức static để lấy số lượng dân số
    public static int getPopulation() {
        return population;
    }
}

public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng của lớp Person
        Person person1 = new Person("Alice", 30);
        Person person2 = new Person("Bob", 25);

        // Sử dụng phương thức getter để lấy giá trị của thuộc tính
        System.out.println("Name: " + person1.getName()); // In ra "Name: Alice"
        System.out.println("Age: " + person1.getAge());   // In ra "Age: 30"

        // Thay đổi giá trị của thuộc tính bằng setter
        person1.setName("Alicia");
        System.out.println("Updated Name: " + person1.getName()); // In ra "Updated Name: Alicia"

        // Sử dụng thuộc tính static
        System.out.println("Population: " + Person.getPopulation()); // In ra "Population: 2"
    }
}
```

#### Các Loại Thuộc Tính
**1. Thuộc Tính Instance (Biến Thể Hiện):**
- Được khai báo mà không có từ khóa static. Mỗi đối tượng của lớp có một bản sao riêng của các thuộc tính này.
- Ví dụ: name và age trong ví dụ trên.
**2. Thuộc Tính Static:**
- Được khai báo với từ khóa static và chỉ có một bản sao cho toàn bộ lớp, chia sẻ giữa tất cả các đối tượng của lớp.
- Ví dụ: population trong ví dụ trên.

#### Các Mức Độ Truy Cập Của Thuộc Tính
**1. Public:**
- Thuộc tính có thể được truy cập từ bất kỳ đâu.
- Ví dụ: public static int population.

**2. Private:**
- Thuộc tính chỉ có thể được truy cập từ bên trong lớp mà nó được khai báo.
- Ví dụ: private String name.

**3. Protected:**
- Thuộc tính có thể được truy cập từ các lớp con và các lớp trong cùng một gói.
- Ví dụ: protected int age.

**4. Default (Package-Private):**
- Nếu không chỉ định từ khóa truy cập, thuộc tính sẽ có phạm vi truy cập mặc định, tức là chỉ có thể được truy cập từ các lớp trong cùng một gói.

#### Khởi Tạo Thuộc Tính
**1. Khởi Tạo Trực Tiếp:**
- Bạn có thể gán giá trị mặc định cho thuộc tính ngay khi khai báo.
- Ví dụ: public int age = 18;

**2. Khởi Tạo Trong Constructor:**
- Bạn có thể khởi tạo giá trị của thuộc tính trong constructor.
- Ví dụ: public Person(String name, int age) { this.name = name; this.age = age; }

**3. Khởi Tạo Trong Khối Static:**
- Đối với thuộc tính static, bạn có thể sử dụng khối static để khởi tạo.
- Ví dụ: 
```
static {
    population = 0;
}
```
**=> Thuộc tính là các biến định nghĩa trong lớp và đại diện cho trạng thái của các đối tượng của lớp đó.**

**=> Biến instance thuộc về các đối tượng cụ thể, trong khi biến static thuộc về lớp.**