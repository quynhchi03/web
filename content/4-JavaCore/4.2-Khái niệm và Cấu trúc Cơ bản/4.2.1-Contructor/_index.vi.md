---
title : "Contructor"
date :  "`r Sys.Date()`"
weight : 1 
chapter : false
pre : " <b> 1.2.1 </b> "
---


### Contructor
- Constructor giống như một phương thức được sử dụng để khởi tạo trạng thái của một đối tượng. Nó được gọi ra vào thời điểm tạo ra đối tượng.
```
pubic soChan(){
}

public soChan(int giaTri){
    this.giaTri = giaTri;
}
```

- **Tự Động Gọi Khi Tạo Đối Tượng:**
+ Constructor được gọi tự động khi một đối tượng của lớp được tạo ra bằng từ khóa **new**.
+ Mục đích chính của constructor là khởi tạo thuộc tính của đối tượng và thực hiện các công việc cần thiết để chuẩn bị đối tượng cho sử dụng.

- **Tên Constructor Phải Trùng Với Tên Lớp:**
+ Constructor có cùng tên với lớp mà nó thuộc về.
+ Ví dụ: Nếu lớp của bạn là **Car**, thì constructor của lớp đó cũng phải được đặt tên là **Car**.

- **Có Thể Định Nghĩa Nhiều Constructor (Constructor Overloading):**
+ Bạn có thể định nghĩa nhiều constructor trong cùng một lớp với các tham số khác nhau (constructor overloading).
+ Điều này cho phép bạn khởi tạo đối tượng theo nhiều cách khác nhau.
#### 1. Default Constructor (Constructor Mặc Định)

- **Khái niệm**: Default constructor là constructor **không có tham số**. Nếu bạn không định nghĩa bất kỳ constructor nào trong lớp, Java sẽ tự động cung cấp một default constructor mà không có tham số.Nếu bạn định nghĩa một constructor có tham số trong lớp, bạn cần phải định nghĩa rõ ràng một constructor không tham số nếu cần.
- **Cú Pháp:**
```
public class Person {
    private String name;
    private int age;

    // constructor mặc định
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
}
```
- **Sử Dụng**
```
Person person = new Person(); // Gọi constructor mặc định
```

#### 2.Parameterized Constructor (Constructor Có Tham Số)

- **Khái niệm**: Parameterized constructor là constructor **có tham số** để khởi tạo các thuộc tính của đối tượng. Bạn có thể định nghĩa nhiều parameterized constructor với các danh sách tham số khác nhau.

- **Cú pháp:**
```
public class Person {
    private String name;
    private int age;

    // constructor có tham số
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```
- **Sử dụng**
```
Person person = new Person("Alice", 30); //Gọi constructor có tham số
```
#### 3.Quy Tắc Sử Dụng Constructor
- Khi Tạo Đối Tượng: Constructor được gọi khi một đối tượng được tạo ra bằng từ khóa **new**. Java sẽ tìm constructor phù hợp dựa trên tham số bạn cung cấp.

- Có Thể Có Nhiều Constructor: Bạn có thể định nghĩa nhiều constructor trong một lớp với các danh sách tham số khác nhau **(constructor overloading)**. Java sẽ chọn constructor phù hợp khi tạo đối tượng.

#### 4. Các câu hỏi phỏng vấn
**1. Contructor trả về kiểu giá trị gì?**
- **Không Trả Về Giá Trị:**
+ Constructor không có kiểu trả về, không phải là void hoặc bất kỳ kiểu dữ liệu nào khác.
+ Không thể có từ khóa return để trả về một giá trị trong constructor.

**2.Contructor dc kế thừa không?**

 **=> Không** 
 - Tuy nhiên, các lớp con có thể gọi constructor của lớp cha thông qua cơ chế gọi constructor của lớp cha trong constructor của lớp con.
 - **Cách Kế Thừa Constructor Trong Java**
- **Constructor Không Được Kế Thừa Trực Tiếp:**
+ Các constructor không được kế thừa trực tiếp từ lớp cha sang lớp con. Lớp con không tự động có các constructor của lớp cha.
- **Gọi Constructor của Lớp Cha:**
+ Lớp con có thể gọi constructor của lớp cha bằng từ khóa **super()**. Điều này thường được thực hiện trong constructor của lớp con để khởi tạo các thuộc tính của lớp cha trước khi thực hiện các công việc khởi tạo trong lớp con.
- **Sử Dụng super():**
+ Từ khóa super() được sử dụng để gọi constructor của lớp cha. Nếu lớp cha có nhiều constructor (constructor overloading), bạn có thể chỉ định constructor cụ thể bằng cách truyền tham số vào **super()**.
+ Nếu bạn không gọi super() rõ ràng, Java sẽ tự động gọi constructor không tham số của lớp cha (nếu có).
- **VD:**
```
// Lớp cha
public class Animal {
    private String name;

    // Constructor của lớp cha
    public Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor called");
    }

    public String getName() {
        return name;
    }
}

// Lớp con
public class Dog extends Animal {
    private String breed;

    // Constructor của lớp con
    public Dog(String name, String breed) {
        // Gọi constructor của lớp cha
        super(name);
        this.breed = breed;
        System.out.println("Dog constructor called");
    }

    public String getBreed() {
        return breed;
    }
}

// Lớp Main để kiểm tra
public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng Dog, constructor của lớp cha sẽ được gọi trước
        Dog myDog = new Dog("Buddy", "Golden Retriever");
        System.out.println("Dog's name: " + myDog.getName());
        System.out.println("Dog's breed: " + myDog.getBreed());
    }
}
```
**3. Có thể tạo contructor final không?**

**=> Không thể tạo constructor final trong Java vì từ khóa final không được áp dụng cho constructor.**
- Không thể tạo một **constructor final**. Constructor không thể có từ khóa **final**, cũng như không thể có các thuộc tính **static** hoặc **abstract**.
- **Không Có Từ Khóa final Đối Với Constructor:**
+ Từ khóa final không thể được sử dụng với constructor. **Từ khóa final được sử dụng để chỉ định rằng một biến, phương thức, hoặc lớp không thể bị thay đổi hoặc mở rộng:**
+ **Biến final**: Giá trị của biến không thể thay đổi sau khi được khởi tạo.
+ **Phương thức final**: Phương thức không thể bị ghi đè trong các lớp con.
+ **Lớp final**: Lớp không thể được kế thừa.
- Constructor không thể được định nghĩa là final vì chúng không phải là phương thức có thể bị ghi đè hoặc kế thừa.
- **Không Có Khái Niệm Constructor static hoặc abstract:**
+ **static**: Constructor không thể là static. Constructor luôn liên kết với một thể hiện cụ thể của lớp và không thể thuộc về lớp theo cách mà các phương thức static làm.
+ **abstract**: Constructor không thể là abstract vì không thể có một constructor chưa được triển khai. Constructor phải có phần thân đầy đủ để khởi tạo đối tượng.
