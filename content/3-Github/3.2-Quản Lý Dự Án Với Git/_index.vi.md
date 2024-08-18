---
title : "Quản Lý Dự Án Với Git"
date :  "`r Sys.Date()`"
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---


#### **Bước 1: Cài Đặt Git**
(Nếu chưa cài đặt Git) Tải và cài đặt Git trên máy tính của bạn từ **git-scm.com**.

#### **Bước 2: Cấu Hình Git**
(Nếu chưa cấu hình) Cấu hình tên và email của bạn

#### **Bước 3: Khởi Tạo Kho Lưu Trữ (Repository)**
**1. Tạo thư mục cho dự án:**

+ Mở terminal (hoặc Command Prompt trên Windows).
Sử dụng lệnh sau để tạo một thư mục mới cho dự án:

```
mkdir ten-du-an
```
+ Di chuyển vào thư mục vừa tạo:

```
cd ten-du-an
```
**2. Khởi tạo Git repository:**

+ Trong thư mục dự án, sử dụng lệnh sau để khởi tạo một kho lưu trữ Git:

```
git init
```
=> Lệnh này sẽ tạo một thư mục ẩn **.git** trong thư mục dự án của bạn, nơi Git sẽ lưu trữ tất cả các thông tin cần thiết để theo dõi các thay đổi trong dự án.
#### **Bước 4: Thêm và Cam Kết (Commit) Thay Đổi**
**1. Tạo tệp README.md và viết mô tả về dự án:**

+ Trong thư mục dự án của bạn, tạo một tệp README.md với nội dung mô tả dự án bằng lệnh:

```
echo "# AdvancedGitProject" >> README.md
```
+ Lệnh này sẽ tạo một tệp **README.md** và thêm dòng **# AdvancedGitProject** vào tệp. Bạn có thể mở tệp này trong trình soạn thảo văn bản của mình để thêm nội dung mô tả chi tiết hơn về dự án.
**2. Thêm tệp vào chỉ mục (staging area):**

+ Sử dụng lệnh sau để thêm README.md vào chỉ mục của Git:

```
git add README.md
```
+ Nếu bạn muốn thêm tất cả các tệp trong thư mục vào chỉ mục, bạn có thể sử dụng:
```
git add .
```
**3. Cam kết (commit) các thay đổi:**

+ Sau khi đã thêm các tệp vào chỉ mục, cam kết các thay đổi với một thông điệp mô tả. Sử dụng lệnh:
```
git commit -m "Thêm tệp README.md với mô tả dự án"
```
+ Thông điệp cam kết (commit message) nên mô tả ngắn gọn về các thay đổi mà bạn đã thực hiện.
**4. Kiểm tra trạng thái và lịch sử cam kết:**

+ Để kiểm tra trạng thái hiện tại của kho lưu trữ và xem các thay đổi đã được thêm vào chỉ mục hay chưa, bạn có thể sử dụng:
```
git status
```
+ Để xem lịch sử các cam kết, bạn có thể sử dụng:
```
git log
```
=> Bây giờ, bạn đã thêm và cam kết tệp **README.md** vào kho lưu trữ Git của mình.

#### **Bước 5: Tạo Nhánh Mới và Sử Dụng Rebase**
**1. Tạo và chuyển sang nhánh mới feature-branch**
+ Tạo nhánh mới và chuyển sang nhánh đó:
```
git checkout -b feature-branch
```
+ Tạo tệp **feature.txt** và thêm nội dung:
```
echo "This is a new feature" >> feature.txt
```
+ Thêm tệp **feature.txt** vào chỉ mục và cam kết:
```
git add feature.txt
git commit -m "Thêm tệp feature.txt với nội dung mới"
```
**2. Chuyển về nhánh chính (main) và thực hiện các thay đổi**
+ Chuyển về nhánh chính (main):
```
git checkout main
```
+ Tạo tệp hotfix.txt và thêm nội dung:
```
echo "This is a hotfix" >> hotfix.txt
```
+ Thêm tệp **hotfix.txt** vào chỉ mục và cam kết:
```
git add hotfix.txt
git commit -m "Thêm tệp hotfix.txt với nội dung hotfix"
```
**3. Rebase nhánh feature-branch lên nhánh main**
+ Chuyển sang nhánh feature-branch:
```
git checkout feature-branch
```
+ Thực hiện rebase nhánh **feature-branch** lên nhánh **main**:

```
git rebase main
```
**4. Giải quyết xung đột (nếu có)**
+ Trong trường hợp có xung đột trong quá trình rebase, Git sẽ thông báo cho bạn biết. Bạn cần phải giải quyết các xung đột này bằng cách chỉnh sửa các tệp bị xung đột, sau đó tiếp tục quá trình rebase với:
```
git add <tệp đã giải quyết xung đột>
git rebase --continue
```
+ Nếu bạn muốn hủy bỏ quá trình rebase và quay lại trạng thái trước đó, bạn có thể sử dụng:
```
git rebase --abort
```
**5. Kiểm tra trạng thái và lịch sử**
+ Kiểm tra trạng thái:
```
git status
```
+ Xem lịch sử cam kết:
```
git log
```
=> Các bước này sẽ giúp bạn tạo và sử dụng các nhánh, cũng như thực hiện rebase để tích hợp các thay đổi từ một nhánh vào nhánh khác.

#### **Bước 6: Sử Dụng Cherry-pick**
**1. Tạo commit mới trên nhánh main**

+ Chuyển sang nhánh main (nếu bạn chưa ở nhánh này):
```
git checkout main
```
+ Tạo tệp anotherfix.txt và thêm nội dung:
```
echo "Another fix" >> anotherfix.txt
```
+ Thêm tệp anotherfix.txt vào chỉ mục và cam kết:
```
git add anotherfix.txt
git commit -m "Thêm tệp anotherfix.txt với nội dung 'Another fix'"
```
**2. Chọn (cherry-pick) commit vào nhánh feature-branch**

+ Xác định mã commit (commit hash):

+ Sử dụng lệnh git log để xem lịch sử commit và tìm mã commit của commit mới nhất trên nhánh main.
```
git log
```
+ Ghi lại mã commit (hash) của commit bạn muốn cherry-pick (ví dụ: abcd1234).
+ Chuyển sang nhánh feature-branch:
```
git checkout feature-branch
```
+ Thực hiện cherry-pick commit từ nhánh main:

+ Sử dụng lệnh cherry-pick với mã commit bạn đã ghi lại:
```
git cherry-pick abcd1234
```
**3. Giải quyết xung đột (nếu có)**

+ Trong trường hợp có xung đột khi thực hiện cherry-pick, Git sẽ thông báo cho bạn biết. Bạn cần phải giải quyết các xung đột này bằng cách chỉnh sửa các tệp bị xung đột, sau đó tiếp tục cherry-pick với:
```
git add <tệp đã giải quyết xung đột>
git cherry-pick --continue
```
+ Nếu bạn muốn hủy bỏ quá trình cherry-pick và quay lại trạng thái trước đó, bạn có thể sử dụng:
```
git cherry-pick --abort
```
**4. Kiểm tra trạng thái và lịch sử**
+ Kiểm tra trạng thái:
```
git status
```
+ Xem lịch sử commit để xác nhận cherry-pick:
```
git log
```
=> Bằng cách làm theo các bước này, bạn đã thực hiện cherry-pick một commit từ nhánh **main** vào nhánh **feature-branch**, cho phép bạn đưa các thay đổi quan trọng từ nhánh khác vào nhánh hiện tại mà không cần phải hợp nhất toàn bộ nhánh.

#### **Bước 7: Sử Dụng Stash**
**1. Thực hiện các thay đổi tạm thời và stash các thay đổi**
+ Tạo và chỉnh sửa tệp temp.txt trên nhánh feature-branch:
```
echo "Some temporary changes" >> temp.txt
```
+ Stash các thay đổi:

+ Stash các thay đổi chưa cam kết với lệnh:
```
git stash
```
+ Nếu bạn muốn thêm một mô tả cho stash, bạn có thể sử dụng:
```
git stash save "Mô tả cho stash"
```
**2. Thực hiện công việc khác và commit các thay đổi**

+ Chuyển sang một nhánh khác hoặc tiếp tục làm việc trên nhánh feature-branch. Trong trường hợp này, bạn đang tiếp tục trên nhánh feature-branch.

+ Tạo tệp another_task.txt và thêm nội dung:
```
echo "Work on another task" >> another_task.txt
```
+ Thêm tệp another_task.txt vào chỉ mục và cam kết:
```
git add another_task.txt
git commit -m "Thêm tệp another_task.txt với nội dung công việc khác"
```
**3. Lấy lại các thay đổi từ stash**
+ Xem danh sách các stash hiện có (nếu bạn có nhiều stash):
```
git stash list
```
+ Lấy lại các thay đổi từ stash:

+ Áp dụng stash mới nhất với lệnh:
```
git stash apply
```
+ Nếu bạn có nhiều stash và muốn lấy lại một stash cụ thể, bạn có thể chỉ định stash đó. Ví dụ, để lấy stash đầu tiên trong danh sách:
```
git stash apply stash@{0}
```
+ Xóa stash sau khi áp dụng (tùy chọn):

+ Sau khi đã lấy lại các thay đổi từ stash, bạn có thể muốn xóa stash để giữ cho danh sách stash gọn gàng:
```
git stash drop stash@{0}
```
**4. Kiểm tra trạng thái và lịch sử**
+ Kiểm tra trạng thái để đảm bảo các thay đổi đã được khôi phục:
```
git status
```
+ Xem lịch sử commit để kiểm tra các thay đổi đã được cam kết:
```
git log
```
=> Bằng cách làm theo các bước này, bạn có thể lưu tạm thời các thay đổi chưa cam kết, thực hiện các công việc khác, và sau đó khôi phục lại các thay đổi đã được stash.

#### **Bước 8: Sử Dụng Submodule**

**1. Thêm Submodule**
1.1 Chuyển đến thư mục gốc của dự án:

+ Đảm bảo bạn đang ở thư mục gốc của dự án nơi bạn muốn thêm submodule.
1.2 Thêm submodule:

+ Sử dụng lệnh git submodule add để thêm submodule. Bạn cần cung cấp URL của kho lưu trữ submodule và tùy chọn cho thư mục mà bạn muốn lưu trữ submodule.
```
git submodule add <URL-của-submodule> <thư-mục-lưu-trữ>
```
+ Ví dụ, nếu bạn muốn thêm kho lưu trữ submodule từ GitHub vào thư mục submodules/example, bạn sẽ thực hiện:
```
git submodule add https://github.com/example/repo.git submodules/example
```
1.3 Cam kết thay đổi:

+ Sau khi thêm submodule, bạn cần cam kết các thay đổi. Git sẽ tạo một thư mục mới trong dự án của bạn và lưu trữ thông tin về submodule trong tệp **.gitmodules.**
```
git add .gitmodules submodules/example
git commit -m "Thêm submodule vào thư mục submodules/example"
```
**2. Cập nhật và Quản lý Submodule**
+ Cập nhật submodule:

+ Để cập nhật submodule, bạn có thể sử dụng lệnh:
```
git submodule update --remote
```
+ Lệnh này sẽ cập nhật submodule để đồng bộ với phiên bản mới nhất trên nhánh mà submodule đang theo dõi.
+ Xem trạng thái submodule:

+ Để kiểm tra trạng thái của các submodule, bạn có thể sử dụng:
```
git submodule status
```
+ Khôi phục submodule (nếu bạn cần thêm lại submodule đã bị xóa hoặc không có):

+ Nếu bạn đã clone kho lưu trữ chính mà không có các submodule, bạn có thể sử dụng lệnh sau để khôi phục submodule:
```
git submodule update --init --recursive
```
**3. Xóa Submodule (nếu cần)**
+ Xóa submodule:
+ Để xóa submodule, bạn cần thực hiện các bước sau:
3.1 Xóa thư mục submodule:
```
rm -rf submodules/example
```
3.2 Xóa mục nhập trong tệp .gitmodules:

+ Mở tệp **.gitmodules** và xóa mục nhập tương ứng với submodule bạn muốn xóa.
3.3 Xóa mục nhập trong .git/config:

+ Mở tệp **.git/config** và xóa mục nhập tương ứng với submodule.
+ Cam kết thay đổi:
```
git rm --cached submodules/example
git commit -m "Xóa submodule submodules/example"
```
=> Với các bước này, bạn có thể thêm, cập nhật, và quản lý các submodule trong dự án Git của bạn.

#### **Bước 9: Đẩy (Push) Lên GitHb**
