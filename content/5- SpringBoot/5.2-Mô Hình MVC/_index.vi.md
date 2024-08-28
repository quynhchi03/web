---
title : "Mô Hình MVC là gì"
date :  "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Nội Dung

- **Mô hình MVC (Model-View-Controller)** là một mẫu thiết kế phần mềm được sử dụng phổ biến trong phát triển ứng dụng web và desktop để phân chia các thành phần của ứng dụng thành ba phần chính: Model, View và Controller. Mô hình này giúp tổ chức mã nguồn tốt hơn, dễ bảo trì và mở rộng.
![alt text](/web/images/5.1.1/image-001.png)

#### 1. Model
- **Chức năng:** Model đại diện cho dữ liệu và logic nghiệp vụ của ứng dụng. Nó xử lý các thao tác liên quan đến dữ liệu và các quy tắc nghiệp vụ.

- **Thành phần:** Model thường bao gồm các lớp Java POJO (Plain Old Java Object) hoặc các lớp JPA Entity. Những lớp này tương tác với cơ sở dữ liệu và chứa logic nghiệp vụ.

- **Ví dụ:** Nếu bạn xây dựng một ứng dụng quản lý người dùng, lớp User có thể là một Model, chịu trách nhiệm lưu trữ và xử lý thông tin người dùng.

#### 2. View
- **Chức năng:** View chịu trách nhiệm hiển thị dữ liệu cho người dùng. Nó nhận thông tin từ Model và trình bày thông tin đó trên giao diện người dùng.

- **Thành phần:** View thường bao gồm các trang HTML, JSP (JavaServer Pages), Thymeleaf templates, hoặc các phần tử giao diện người dùng khác. Trong các ứng dụng web, các template engine như Thymeleaf hoặc JSP được sử dụng để tạo giao diện người dùng động.

- **Ví dụ:** Trang HTML hoặc JSP hiển thị danh sách người dùng là một View. Nó lấy dữ liệu từ Model và hiển thị chúng trong giao diện người dùng.

#### 3. Controller

- **Chức năng:** Controller xử lý các yêu cầu từ người dùng, tương tác với Model để xử lý dữ liệu, và trả về kết quả cho View. Nó là cầu nối giữa Model và View.

- **Thành phần:** Controller thường được triển khai dưới dạng các lớp Java với các phương thức được chú thích bằng các annotation như @RequestMapping, @GetMapping, hoặc @PostMapping trong Spring MVC.

- **Ví dụ:** Lớp UserController xử lý các yêu cầu HTTP như GET và POST liên quan đến người dùng. Nó có thể gọi các phương thức trong lớp Model để lấy dữ liệu và chuyển giao dữ liệu đó cho View.

#### Cách hoạt động của mô hình MVC trong ứng dụng Java:

- **Người dùng gửi yêu cầu:** Người dùng gửi yêu cầu từ trình duyệt (hoặc giao diện người dùng) đến ứng dụng web.

- **Controller xử lý yêu cầu:** Controller nhận yêu cầu và xác định các hành động cần thực hiện. Nó có thể gọi các phương thức trong Model để xử lý dữ liệu.

- **Model xử lý dữ liệu:** Model thực hiện các thao tác với cơ sở dữ liệu hoặc xử lý logic nghiệp vụ theo yêu cầu từ Controller.

- **View cập nhật giao diện:** Controller sau đó chuyển dữ liệu từ Model tới View. View sử dụng dữ liệu này để cập nhật giao diện người dùng.

- **Người dùng nhận kết quả:** Người dùng thấy kết quả trong giao diện đã được cập nhật.

#### Ưu Điểm của Mô hình MVC:

- **Kiểm tra Dễ Dàng:** Với MVC, bạn có thể kiểm tra và rà soát lỗi phần mềm trước khi đưa ra người dùng, đảm bảo chất lượng và độ tin cậy cao hơn.

- **Chức Năng Kiểm Soát:** Mô hình MVC cho phép bạn có quyền kiểm soát tốt hơn đối với các yếu tố quan trọng như giao diện, dữ liệu và logic ứng dụng.

- **Tích hợp dễ dàng:** Mô hình này cho phép tích hợp ứng dụng dễ dàng trên nền tảng web và giảm tải máy chủ.

- **Phân Tách Các Trách Nhiệm:** MVC phân tách rõ ràng các phần khác nhau của ứng dụng như Model, View và Controller, giúp dễ dàng quản lý và bảo trì mã nguồn.

#### Nhược Điểm của Mô hình MVC:

- Mô hình này thường được ưa chuộng trong các dự án lớn, có thể gây cồng kềnh và tốn thời gian đối với các dự án nhỏ hơn.

#### Ví dụ về MVC trong Spring Boot:
- **Model: Một lớp User được chú thích bằng @Entity, đại diện cho bảng người dùng trong cơ sở dữ liệu.**
```
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    
    // Getters and setters
}
```
- **View: Một trang Thymeleaf để hiển thị danh sách người dùng.**
```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>User List</title>
</head>
<body>
    <h1>User List</h1>
    <ul>
        <li th:each="user : ${users}" th:text="${user.name}"></li>
    </ul>
</body>
</html>
```
- **Controller: Một lớp UserController xử lý yêu cầu và trả về dữ liệu cho View.**
```
@Controller
public class UserController {
    
    @Autowired
    private UserService userService;
    
    @GetMapping("/users")
    public String listUsers(Model model) {
        List<User> users = userService.findAllUsers();
        model.addAttribute("users", users);
        return "userList";
    }
}
```