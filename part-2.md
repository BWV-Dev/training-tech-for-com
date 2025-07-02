# Tài liệu

## **Module 5: Git & GitHub**

### 🎯 **Mục tiêu**:

- Nắm rõ các khái niệm cơ bản về Git & GitHub.
- Thực hiện các thao tác quản lý phiên bản tài liệu.

### **Phần I: Lý thuyết**

#### **1. Khái niệm cơ bản**

**Git** là hệ thống quản lý phiên bản, giúp lưu trữ lịch sử thay đổi, kiểm soát phiên bản tài liệu hiệu quả.

Hãy tưởng tượng Git như một "cỗ máy thời gian" dành riêng cho tài liệu:
- **Theo dõi lịch sử**: Ai sửa, sửa những gì, khi nào.
- **Khôi phục dễ dàng**: Quay lại phiên bản cũ nhanh chóng.
- **Hỗ trợ cộng tác**: Nhiều người cùng làm việc hiệu quả, tránh mất dữ liệu do sửa chồng chéo.

**GitHub** là dịch vụ lưu trữ repository online, hỗ trợ cộng tác, review code, tài liệu và trao đổi hiệu quả giữa các thành viên.

#### **2. Các thuật ngữ chính**:
- **Repository (Repo)**: Thư mục chứa tài liệu, có hai dạng:
  - Local Repository (trên máy cá nhân)
  - Remote Repository (trên GitHub)
- **Commit**: Ghi lại sự thay đổi kèm mô tả ngắn (message).
- **Branch**: Nhánh riêng biệt để phát triển, chỉnh sửa tài liệu không ảnh hưởng đến nhánh chính.
- **Pull Request (PR)**: Yêu cầu gộp thay đổi vào nhánh chính, cần người khác review và duyệt.
- **Merge**: Gộp các thay đổi từ một nhánh vào nhánh khác.
- **Conflict**: Xảy ra khi cùng một dòng tài liệu được thay đổi khác nhau giữa các nhánh.

#### **3. Các thao tác cơ bản với Git**

 Lệnh Git                         | Chức năng                                                                 |
|----------------------------------|--------------------------------------------------------------------------|
| `git init`                       | Tạo một repository Git local mới                                         |
| `git clone <link_repo>`         | Sao chép repository từ GitHub về máy local                              |
| `git status`                    | Kiểm tra trạng thái các file trong repository                           |
| `git add <file>`               | Thêm file vào staging area (trạng thái chờ commit)                      |
| `git commit -m "message"`       | Lưu lại các thay đổi với mô tả đi kèm                                   |
| `git push`                      | Đẩy thay đổi từ local lên repository trên GitHub                        |
| `git pull`                      | Kéo thay đổi mới nhất từ repository trên GitHub về local                |
| `git branch <branch_name>`     | Tạo một nhánh mới                                                       |
| `git checkout <branch_name>`   | Chuyển sang làm việc trên một nhánh khác                                |
| `git stash`                     | Lưu tạm các thay đổi chưa commit                                        |
| `git stash list`               | Xem danh sách các stash đã lưu                                          |
| `git stash apply`              | Áp dụng stash gần nhất nhưng không xóa nó khỏi danh sách stash         |
| `git stash apply {n}`          | Áp dụng stash thứ `n` trong danh sách stash (ví dụ: `git stash apply stash@{1}`) |
| `git stash pop`                | Áp dụng và đồng thời xóa stash gần nhất khỏi danh sách stash           |
| `git revert <commit_id>`           | Tạo một commit mới để đảo ngược thay đổi từ commit được chỉ định                         |
| `git cherry-pick <commit_id>`      | Sao chép một commit cụ thể từ nhánh khác vào nhánh hiện tại                              |
| `git log --oneline`                | Hiển thị lịch sử commit ngắn gọn (mỗi commit trên một dòng, gồm hash và message)         |

#### **4. Các thao tác cơ bản với GitHub**

- **Fork**: Sao chép repo của người khác về tài khoản của mình.

- **Pull Request**:
  - Tạo PR
  - Thảo luận và review
  - Merge PR

#### **5. Quy trình làm việc nhóm với GitHub**

- Clone repo
- Tạo branch riêng
- Chỉnh sửa và commit
- Đẩy thay đổi lên GitHub
- Tạo Pull Request
- Chờ review và merge

### 💻 **Phần II: Thực hành**

#### 1. **Thực hành Git trên máy local**

- Tạo repository mới
- Thêm file, commit file
- Xem lịch sử thay đổi
- Tạo nhánh mới, chuyển đổi giữa các nhánh

#### 2. Thực hành làm việc với GitHub

- Tạo repo trên GitHub, clone repo về máy
- Thực hiện chỉnh sửa, commit và push lên GitHub
- Tạo và quản lý Pull Request
- Thực hành review, comment và merge PR
- Xử lý conflict thực tế