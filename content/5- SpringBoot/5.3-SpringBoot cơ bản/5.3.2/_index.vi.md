---
title : "@Component annotation và @Autowired annotation"
date :  "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

#### @Component

- **@Component là một annotation trong Spring Framework dùng để đánh dấu một lớp là một bean (đối tượng quản lý bởi Spring). Khi bạn đánh dấu một lớp với @Component, Spring sẽ tự động phát hiện và đăng ký lớp đó là một bean trong ngữ cảnh ứng dụng (Application Context).**

- **Ví dụ:**
```
import org.springframework.stereotype.Component;

@Component
public class MyService {
    public void doSomething() {
        // implementation
    }
}
```

- Trong ví dụ trên, MyService sẽ được tự động quản lý bởi Spring Container. Điều này có nghĩa là Spring sẽ tạo ra một instance của MyService và quản lý vòng đời của nó.

#### @Autowired

- **@Autowired là một annotation được dùng để tự động tiêm phụ thuộc vào một bean trong Spring. Khi bạn đánh dấu một trường (field), phương thức, hoặc constructor của một bean với @Autowired, Spring sẽ tự động cung cấp giá trị (dependency) cho trường, phương thức, hoặc constructor đó.**

- **Ví dụ:**
```
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyController {

    private final MyService myService;

    @Autowired
    public MyController(MyService myService) {
        this.myService = myService;
    }

    public void handleRequest() {
        myService.doSomething();
    }
}
```

- Trong ví dụ trên, MyController phụ thuộc vào MyService. @Autowired cho phép Spring tự động chèn một instance của MyService vào MyController thông qua constructor.

- Kết Luận: 
+ **@Component: Đánh dấu một lớp là một bean để Spring quản lý.**
+ **@Autowired: Tự động tiêm phụ thuộc vào bean mà Spring quản lý.**