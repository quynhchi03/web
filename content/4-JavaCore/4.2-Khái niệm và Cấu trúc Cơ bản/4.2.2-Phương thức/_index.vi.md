---
title : "Phương Thức(Methods)"
date :  "`r Sys.Date()`"
weight : 2 
chapter : false
pre : " <b> 1.2.2 </b> "
---

#### Phương thức
- là các khối mã có thể thực hiện các hành động cụ thể và có thể được gọi để thực hiện một công việc. Phương thức được khai báo trong lớp và có thể được sử dụng để thao tác với dữ liệu và thực hiện các thao tác khác.

#### Khai Báo Phương Thức Trong Java
- Phương thức trong Java được khai báo với cú pháp như sau:
```
[public|protected|private] [static] [return_type] methodName([parameters]) {
    // Phần thân phương thức
}
```
- **Access Modifier**: Quy định phạm vi truy cập của phương thức **(ví dụ: public, protected, private)**. Nếu không chỉ định, phương thức có phạm vi truy cập mặc định.
- **Static**: Từ khóa static cho phép phương thức thuộc về lớp thay vì một đối tượng cụ thể.
- **Return Type**: Kiểu dữ liệu của giá trị mà phương thức trả về. Nếu phương thức không trả về giá trị, sử dụng void.
- **Method Name**: Tên của phương thức, phải tuân theo quy tắc đặt tên trong Java.
- **Parameters**: Danh sách các tham số mà phương thức nhận vào. Có thể không có tham số.

#### Ví Dụ Về Cách Khai Báo và Sử Dụng Phương Thức
```
public class Calculator {
    // Phương thức không trả về giá trị (void)
    public void printWelcomeMessage() {
        System.out.println("Welcome to the Calculator!");
    }

    // Phương thức có tham số và trả về giá trị (int)
    public int add(int a, int b) {
        return a + b;
    }

    // Phương thức có nhiều tham số và trả về giá trị (double)
    public double multiply(double a, double b, double c) {
        return a * b * c;
    }

    // Phương thức static
    public static void printStaticMessage() {
        System.out.println("This is a static method.");
    }
}

public class Main {
    public static void main(String[] args) {
        // Tạo đối tượng của lớp Calculator
        Calculator calc = new Calculator();

        // Gọi phương thức không trả về giá trị
        calc.printWelcomeMessage();

        // Gọi phương thức có tham số và nhận giá trị trả về
        int sum = calc.add(10, 5);
        System.out.println("Sum: " + sum);

        // Gọi phương thức có nhiều tham số và nhận giá trị trả về
        double product = calc.multiply(2.5, 3.0, 4.0);
        System.out.println("Product: " + product);

        // Gọi phương thức static mà không cần tạo đối tượng
        Calculator.printStaticMessage();
    }
}
```
#### Các Loại Phương Thức
- **Phương Thức Không Trả Về Giá Trị (void):**
+ Phương thức không trả về giá trị nào và thường được sử dụng để thực hiện các hành động.
+ Ví dụ: printWelcomeMessage() trong ví dụ trên.
- **Phương Thức Trả Về Một Giá Trị:**
+ Phương thức trả về một giá trị cụ thể và có kiểu dữ liệu.
+ Ví dụ: add(int a, int b) trả về giá trị kiểu int.
- **Phương Thức static:**
+ Phương thức thuộc về lớp chứ không phải đối tượng cụ thể. Có thể được gọi mà không cần tạo đối tượng.
+ Một phương thức static gọi mà không cần tạo một instance của một lớp.
+ Phương thức static có thể truy cập biến static và có thể thay đổi giá trị của nó.
+ Ví dụ: printStaticMessage() trong ví dụ trên.
- **Phương Thức Overloading:**
+ Phương thức có cùng tên nhưng khác tham số (khác kiểu dữ liệu hoặc số lượng tham số).
+ Ví dụ: add(int a, int b) và multiply(double a, double b, double c).
- **Phương Thức Overriding:**
+ Lớp con có thể ghi đè phương thức của lớp cha để thay đổi hoặc mở rộng hành vi của phương thức.
```
public class Animal {
    public void makeSound() {
        System.out.println("Động vật phát ra âm thanh");
    }
}

public class Dog extends  {
    @Override
    public void makeSound() {
        System.out.println("Tiếng chó sửa");
    }
}
```
#### Quy Tắc Đặt Tên Phương Thức
- **Tên Phương Thức:**
+ Phải bắt đầu bằng chữ cái và có thể bao gồm chữ cái, số, và dấu gạch dưới (_).
+ Nên sử dụng các quy tắc đặt tên dongVat, bắt đầu bằng chữ cái thường và chữ cái đầu của mỗi từ tiếp theo được viết hoa (ví dụ: tiengChoSua).
- **Tham Số:**
+ Phương thức có thể có nhiều tham số và mỗi tham số phải có kiểu dữ liệu xác định.
+ Tham số được phân cách bằng dấu phẩy.

#### Biến static
- **static** là một biến thuộc về lớp chứ không phải thuộc về đối tượng của lớp đó. 
- Biến static có thể được sử dụng để tham chiếu thuộc tính chung của tất cả đối tượng (mà không là duy nhất cho mỗi đối tượng), ví dụ như tên công ty của nhân viên, tên trường học của các sinh viên, …

**1. Thuộc Về Lớp, Không Phải Đối Tượng:**
- Biến static được khai báo với từ khóa static và có thể được truy cập mà không cần tạo đối tượng của lớp.
- Biến này tồn tại và được chia sẻ bởi tất cả các đối tượng của lớp đó.

**2. Có Một Bản Sao Duy Nhất:**
- Chỉ có một bản sao của biến static trong bộ nhớ cho toàn bộ lớp, bất kể số lượng đối tượng được tạo ra.

**3. Có Thể Được Truy Cập Qua Tên Lớp:**
- Biến static có thể được truy cập trực tiếp thông qua tên lớp mà không cần tạo một đối tượng của lớp đó.
- Ví dụ: ClassName.staticVariable.

**Cú Pháp Khai Báo Biến static**
```
public class MyClass {
    // Khai báo biến static
    public static int staticVariable = 10;

    // Khai báo biến instance
    public int instanceVariable = 20;
}
```

**VD và Cách sử dụng biến static**

```
public class Counter {
    // Biến static
    public static int count = 0;

    // Constructor
    public Counter() {
        count++;
    }

    // Phương thức static để truy cập biến static
    public static void displayCount() {
        System.out.println("Count: " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        // Không cần tạo đối tượng để truy cập biến static
        Counter.displayCount(); // In ra "Count: 0"

        // Tạo các đối tượng của lớp Counter
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();

        // Truy cập biến static
        Counter.displayCount(); // In ra "Count: 3"
    }
}
```
**Lưu Ý**
- **Không Thể Truy Cập Biến Instance Trong Phương Thức Static:**

- Phương thức static không thể truy cập trực tiếp các biến instance (không phải static) của lớp vì nó không thuộc về bất kỳ đối tượng cụ thể nào. Bạn cần tạo một đối tượng của lớp để truy cập các biến instance từ phương thức static.
- **Biến static Có Thể Gây Đụng Độ:**

- Do biến static được chia sẻ giữa tất cả các đối tượng, nên bạn cần cẩn thận với các vấn đề đồng bộ hóa trong môi trường đa luồng.

 #### Khối static

- Được sử dụng để khởi tạo thành viên dữ liệu static.
- Nó được thực thi trước phương thức main tại lúc tải lớp.
- **Cú Pháp Khai Báo Khối static:**
```
public class MyClass {
    static {
        // Khối static
        System.out.println("Static block executed");
    }
}
```
**Đặc Điểm Của Khối static**
- **Chạy Khi Lớp Được Tải:**
 Khối static được thực thi một lần duy nhất khi lớp đầu tiên được tải vào bộ nhớ, trước khi bất kỳ đối tượng nào của lớp đó được tạo ra.

- **Dùng Để Khởi Tạo Biến static:**
Khối static thường được sử dụng để khởi tạo các biến static hoặc thực hiện các công việc cấu hình cần thiết cho lớp.

- **Có Thể Có Nhiều Khối static:**
 Bạn có thể khai báo nhiều khối static trong cùng một lớp. Các khối này sẽ được thực thi theo thứ tự khai báo.

- **Không Có Tham Số:**
 Khối static không thể nhận tham số và không thể có giá trị trả về. Nó chỉ đơn thuần là một khối mã được thực thi khi lớp được nạp.

- **Không Phụ Thuộc Vào Đối Tượng:**
 Khối static không phụ thuộc vào các đối tượng của lớp. Thay vào đó, nó liên kết với lớp và được thực thi khi lớp được nạp.