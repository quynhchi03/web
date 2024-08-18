---
title : "Các Câu Hỏi Phỏng Vấn"
date :  "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

#### Câu Hỏi

**1. Constructor là gì?**
-	Là phương thức khởi tạo đối tượng của một lớp
-	Cùng tên với class mà nó thuộc về
-	2 loại constructor: mặc định và chứa tham số
-	Quy tắc: Nếu trong class không có constructor, trình biên dịch sẽ tự động tạo một constructor mặc định trong class đó.
-	VD constructor mặc định:
```
public Animal(){

}
```
-	VD constructor chứa tham số:
```
public Person(String name, int age) {
        this.name = name;
        this.age = age;
}
```

**2. Mục đích của constructor là gì?**
-	Khởi tạo các giá trị để cung cấp dữ liệu cho thuộc tính đối tượng

**3. Constructor trả về kiểu giá trị gì?**
-	Không có kiểu giá trị trả về

**4. Constructor được kế thừa không?**
-	Constructor lớp con không thể kế thừa từ lớp cha nhưng có thể gọi constructor lớp cha bằng từ khóa “super”

**5. Có thể tạo constructor final không?**
-	Không thể. Vì khi đó constructor không được kế thừa.

**6. Biến static là gì?**
-	Là biến thuộc về class, chứ không thuộc về đối tượng trong lớp đó
-	Dùng làm thuộc tính chung cho mọi đối tượng trong class 
-	Tiết kiệm bộ nhớ
-	Có thể truy cập biến static mà không cần tạo đối tượng của class chứa nó
```
private static int count = 0;

public student(){
    count ++;
}
```
**7. Phương thức static là gì?**
-	Thuộc về class
-	Có thể truy cập biến static và thay đổi giá trị của nó
-	Không thể truy cập biến hoặc phương thức non-static
```
public static int getConunt(){
    return count;
}

public static void setCount(int count){
    Student.count = count;
}
```
**8. Tại sao phương thức main là static?**
-	Không cần thiết tạo đối tượng để gọi phương thức main (non – static) => gây ra vấn đề về cấp phát bộ nhớ phụ

**9. Khối static là gì?**
-	Dùng để khởi tạo hoặc thay đổi giá trị biến static 
-	Không cần tạo đối tượng để thực hiện khối static
-	Thực thi 1 lần trước phương thức main
```
static int count;
static{
    System.out.println("Hello");
    count = 5;
}
```

**10. Sự khác nhau giữa phương thức static và phương thức instance?**
-	Phương thức static thuộc về class, phương thức instance thuộc về đối tượng
=>	Để gọi phương thức instance, cần gọi từ một đối tượng cụ thể 
```
public void setName(String name){
    this.name = name;
}
public int getAge(){
    return Age;
}
```
=> Ví dụ phương thức instance

```
Student student = new Student();
student.setName("Chi");
```
=> Gọi phương thức instance

**11. this trong java là gì?**
-	Dùng để tham chiếu đến biến instance của class => Phân biệt được biến instance và tham số khi nó cùng tên
```
public void setName(String name){
    this.name = name;
}
```

**12. Kế thừa là gì?**
-	Lớp con kế thừa từ lớp cha => thừa hưởng các thuộc tính và phương thức từ lớp cha mà không cần viết lại code => tính tái sử dụng
-	Lớp con có thể ghi đè phương thức lớp cha và thay đổi hành vi theo yêu cầu lớp con
=>	Lớp cha có gì thì lớp con có đó (không có chiều ngược lại)

**13. Lớp nào là lớp cha cho tất cả các lớp?**
-	Lớp object

**14. Tại sao đa kế thừa không được hỗ trợ trong java?**
-	Để giảm thiểu sự phức tạp và đơn giản hóa ngôn ngữ, đa kế thừa không được support trong java.

**15. Composition là gì?**
-	Khai báo biến tham chiếu của một class trong một class khác được gọi là composition(sự hợp thành).

**16. Sự khác nhau giữa aggregation và composition?**
-	Aggregation biểu diễn mối quan hệ yếu, còn composition biểu diễn quan hệ chặt chẽ. Ví dụ: xe máy có một công tơ mét (aggregation), nhưng xe máy có một động cơ (composition).

**17. Tại sao java không support con trỏ?**
-	Con trỏ là một biến tham chiếu tới địa chỉ ô nhớ. Nó không được sử dụng trong java vì nó không an toàn và phức tạp.

**18. super trong java là gì?**
-	Nó là một từ khóa mà tham chiếu trực tiếp đến đối tượng của lớp cha.

**19. Có thể sử dụng cả this() và super() trong một constructor?**
-	Không, vì this() gọi đến một constructor khác trong lớp hiện tại, còn super() gọi constructor của lớp cha.

**20. Object cloning là gì?**
-	object cloning được sử dụng để tạo ra một bản sao giống hệt đối tượng ban đầu.

**21. Overloading (nạp chồng) phương thức là gì?**
-	Nếu một lớp có nhiều phương thức có tên giống nhau nhưng các tham số khác nhau, được gọi là overloading phương thức (nạp chồng phương thức). Nó giúp code rõ ràng, dễ hiểu hơn.

**22. Tại sao overloading phương thức không xảy ra khi thay đổi kiểu giá trị trả về?**
-	Bởi vì đó là sự không rõ ràng, không biết gọi phương thức nào khi runtime.

**23. Có thể overload phương thúc main() không?**
-	Có, có thể overload phương thức main().

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn overriding phương thức

**1. Ghi đè (overriding) phương thức là gì?**

-	Là quá trình lớp con thay đổi hành vi  cho một phương thức đã được định nghĩa trong lớp cha (phương thức có cùng tên, cùng tham số)
-	Không ảnh hưởng tới phương thức lớp cha hay lớp con khác

![alt text](/web/images/4.3/image-001.png)

**2. Có thể ghi đè phương thức static không?**
-	Không. Vì phương thức static thuộc về class

**3. Tại sao không thể ghi đè phương thức static?**
-	Phương thức static được liên kết với lớp, không phải với đối tượng,nên nó không thể ghi đè được

**4. Có thể ghi đè phương thức đã nạp chồng?**
-	Có

**5. Có thể ghi đè biến instance không?**
-	Không

**6. Kiểu trả về hiệp biến là gì?**
-	Từ java 5 trở đi, có thể ghi đè bất kỳ phương thức nào bởi việc thay đổi kiểu giá trị trả về. Nếu kiểu trả về của phương thức ghi đè của lớp con là lớp con. Nó được gọi là kiểu trả về hiệp biến.

#### Các khái niệm về OPPs: Các câu hỏi phỏng vấn từ khóa final

**1. Biến final là gì?**
-	Nếu bạn tạo một biến với từ khóa final, bạn sẽ không thể thay đổi được giá trị của biến đó (hằng số).

**2. Phương thức final là gì?**
-	Phương thức final không thể được ghi đè.

**3. Lớp final là gì?**
-	Lớp final không thể được kế thừa.

**4. Biến final blank là gì?**
-	Một biến final không được khởi tạo giá trị lúc khai báo được gọi là biến final blank.

**5. Có thể khởi tạo giá trị cho biến final blank không?**
-	Có, nếu biến đó là non-static thì chỉ khởi tạo được trong constructor. Nếu biến đó là static thì chỉ khởi tạo được trong khối static.











