---
title : "Lý Thuyết về Github"
date :  "`r Sys.Date()`"
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
---

#### Nội Dung

- Github là gì?
- Tại sao nên sử dụng Github
- Một số khái niệm cơ bản
- Câu lệnh cơ bản của Github

#### **1..Github là gì?**

- **GitHub** là một dịch vụ cung cấp kho lưu trữ mã nguồn Git dựa trên nền web cho các dự án phát triển phần mềm.
- **Git** đơn giản hơn đó là nó sẽ giúp bạn lưu lại các phiên bản của những lần thay đổi vào mã nguồn và có thể dễ dàng khôi phục lại dễ dàng mà không cần copy lại mã nguồn rồi cất vào đâu đó.
<!-- 
![alt text](/web/images/3.1/image-001.png) -->

#### **2.Tại sao nên sử dụng Github**

- Git dễ sử dụng, an toàn và nhanh chóng.
- Có thể giúp quy trình làm việc code theo nhóm đơn giản hơn rất nhiều bằng việc kết hợp các phân nhánh (branch).
- Bạn có thể làm việc ở bất cứ đâu vì chỉ cần clone mã nguồn từ kho chứa hoặc clone một phiên bản thay đổi nào đó từ kho chứa, hoặc một nhánh nào đó từ kho chứa.

#### **3.Một số khái niệm cơ bản**

**1.Repository (Repo)**: Là một kho lưu trữ chứa mã nguồn và các tài liệu liên quan đến dự án. Mỗi repository có thể chứa các file mã nguồn, tài liệu, và có thể quản lý nhiều phiên bản khác nhau của dự án.

**2.Branch**: Một nhánh trong GitHub cho phép bạn làm việc trên các tính năng hoặc sửa lỗi mới mà không ảnh hưởng đến mã nguồn chính (thường là nhánh main hoặc master). Bạn có thể tạo, chỉnh sửa, và xóa nhánh theo nhu cầu.

**3.Commit**: Là hành động lưu trữ các thay đổi vào kho lưu trữ. Mỗi commit thường đi kèm với một thông điệp mô tả thay đổi đó. Commit cho phép bạn theo dõi lịch sử thay đổi của mã nguồn.

**4.Pull Request (PR)**: Là một yêu cầu hợp nhất thay đổi từ một nhánh này sang nhánh khác. Pull request thường được dùng để thảo luận về những thay đổi, xem xét mã nguồn, và kiểm tra trước khi hợp nhất vào nhánh chính.

**5.Merge**: Là hành động kết hợp các thay đổi từ một nhánh vào nhánh khác. Khi một pull request được chấp nhận, thay đổi từ nhánh con sẽ được merge vào nhánh chính.

**6.Fork**: Là hành động tạo một bản sao của một repository vào tài khoản của bạn. Fork thường được sử dụng để đóng góp cho các dự án mà bạn không có quyền truy cập trực tiếp.

**7.Clone**: Là hành động sao chép một repository từ GitHub về máy tính của bạn để làm việc trên mã nguồn một cách offline. Bạn sẽ có bản sao đầy đủ của repository trên máy tính cá nhân.

**8.Issue**: Là cách để theo dõi các lỗi, yêu cầu tính năng, hoặc các công việc cần thực hiện trong dự án. Bạn có thể tạo, quản lý và đóng issue khi công việc liên quan đã được hoàn thành.

**9.Tag**: Là một điểm đánh dấu trong lịch sử commit để đánh dấu một phiên bản quan trọng của mã nguồn, như là phiên bản phát hành chính thức (release).

**10.Actions**: Là tính năng tự động hóa trong GitHub, cho phép bạn tạo các quy trình làm việc (workflow) để tự động hóa các tác vụ như kiểm tra mã nguồn, triển khai ứng dụng, và nhiều hơn nữa.

#### **4.Câu lệnh cơ bản của Github**

**1.Khởi tạo repository**

```
git init
```
- Tạo một kho lưu trữ Git mới trong thư mục hiện tại.

**2.Clone repository**

```
git clone <repository-url>

```
- Sao chép một repository từ GitHub về máy tính của bạn.

**3.Kiểm tra trạng thái**

```
git status
```
- Xem trạng thái hiện tại của repository, bao gồm các thay đổi đã được thêm vào hoặc chưa được commit.

**4.Thêm thay đổi vào stage**

```
git add <file>
git add .
```
- Thêm file cụ thể vào staging area hoặc thêm tất cả các thay đổi (dấu chấm . đại diện cho tất cả các file).

**5.Commit thay đổi**

```
git commit -m "Thông điệp commit"
```
- Lưu các thay đổi đã được stage với một thông điệp mô tả.

**6.Xem lịch sử commit**

```
git log
```
- Hiển thị lịch sử commit của repository.

**7.Tạo một nhánh mới**

```
git branch <tên-nhánh>
```
- Tạo một nhánh mới trong repository.

**8.Chuyển đổi giữa các nhánh**

```
git checkout <tên-nhánh>
```
- Chuyển sang nhánh khác.

**9.Hợp nhất nhánh**

```
git merge <tên-nhánh>
```
- Hợp nhất các thay đổi từ nhánh cụ thể vào nhánh hiện tại.

**10.Xóa nhánh**

```
git branch -d <tên-nhánh>
```
- Xóa nhánh không còn cần thiết nữa.

**11.Cập nhật repository từ remote**

```
git pull
```
- Kéo các thay đổi mới từ remote repository (như GitHub) về máy tính của bạn và hợp nhất chúng vào nhánh hiện tại.

**12.Đẩy thay đổi lên remote**

```
git push
```
- Đẩy các thay đổi từ repository cục bộ lên repository từ xa.

**13.Xem thông tin remote**

```
git remote -v
```
- Hiển thị URL của các remote repository được liên kết với repository cục bộ.

**14.Thay đổi cấu hình user**

```
git config --global user.name "Tên của bạn"
git config --global user.email "email@example.com"
```
- Đặt cấu hình toàn cục cho tên người dùng và email để sử dụng trong các commit.

