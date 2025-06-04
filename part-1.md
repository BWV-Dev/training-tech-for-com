# Tài liệu

## 📑 **MỤC LỤC**

### **Phần I: Xử lý dữ liệu và công cụ cơ bản**
- [Module 1: Định dạng file - CSV, Excel, JSON](#module-1-định-dạng-file---csv-excel-json)
- [Module 2: HTTP Status Codes](#module-2-http-status-codes)
- [Module 3: Công cụ so sánh file (Diff Tools)](#module-3-công-cụ-so-sánh-file-diff-tools)

### **Phần II: Công nghệ và hạ tầng**
- [Module 4: Cơ bản về AWS](#module-4-cơ-bản-về-aws)
- [Module 5: Cơ bản về Git](#module-5-cơ-bản-về-git)
  
---

## **Module 1: Định dạng file - CSV, Excel, JSON**

### 📋 **Khái niệm và định nghĩa**

**CSV (Comma-Separated Values)**:
- Bản chất: File text thuần túy (plain text)
- Cấu trúc: Chỉ chứa dữ liệu thô, phân cách bằng dấu phẩy (hoặc dấu chấm phẩy)
- Không có format: Không lưu thông tin về font, màu sắc, định dạng ngày tháng
- Encoding: Phụ thuộc vào encoding được sử dụng (UTF-8, UTF-16, Windows-1252...)

**Excel (.xlsx/.xls)**:
- Bản chất: File binary phức tạp
- Cấu trúc: Lưu trữ cả dữ liệu và metadata (thông tin định dạng)
- Có format: Lưu font, màu sắc, định dạng số, ngày tháng, công thức
- Encoding: Tự động xử lý charset

|          | CSV (Comma-Separated Values)                              | Excel (.xlsx/.xls)                                      |
|------------------|----------------------------------------------------------|--------------------------------------------------------|
| **Bản chất**     | File text thuần túy (plain text)                         | File binary phức tạp                                   |
| **Cấu trúc**     | Chỉ chứa dữ liệu thô, phân cách bằng dấu phẩy (hoặc chấm phẩy) | Lưu trữ cả dữ liệu và metadata (thông tin định dạng)   |
| **Format**       | Không lưu thông tin về font, màu sắc, định dạng ngày tháng | Lưu font, màu sắc, định dạng số, ngày tháng, công thức |
| **Encoding**     | Phụ thuộc vào encoding (UTF-8, UTF-16, Windows-1252...)  | Tự động xử lý charset                                  |

- Ví dụ nội dung file CSV:
  ```
  "ID","Name","Age"
  "1","Nguyễn Văn A","25"
  "2","Trần Thị B","30"
  ```

**JSON (JavaScript Object Notation)**:
- Là định dạng dữ liệu dạng "cây" (key-value), nhẹ và dễ đọc.
- Thường dùng trong API để trao đổi dữ liệu.
- Ví dụ file JSON:
  ```json
  {
    "ID": 1,
    "Name": "Nguyễn Văn A",
    "Age": 25,
  }

  "{\"comment\" : \"このレポートはテストのため無視してください\"}"

  ```

### 📌 **Tại sao CSV bị "format sai" khi mở bằng Excel?**

**Vấn đề 1: Auto-detection sai**
- File CSV có: 2025-06-04 (năm-tháng-ngày)
- Excel hiểu thành: 04/06/2025 (ngày/tháng/năm)

**Vấn đề 2: Encoding không khớp**
- Tình huống: File CSV được tạo bằng Shift-JIS, nhưng Excel mở bằng UTF-8
- Ví dụ:
  - Dữ liêu gôc: `案件番号`
  - Hiển thị sai: `ˆÄŒ”Ô†`

**Vấn đề 3: Separator không đúng**

Ví dụ:
  - File CSV dùng dấu chấm phẩy: `Name;Date;Amount`
  - Excel expect dấu phẩy → Tất cả data nằm trong 1 cột

### 🛠️ **Giải pháp**

1. **Dùng Text Editor (Notepad++, VS Code)**:
   - Mở file để xem dữ liệu gốc
   - Kiểm tra encoding (UTF-8, Shift-JIS) bằng VS Code (góc dưới bên phải)
2. **Import vào Excel đúng cách**:
   - Excel → Data → From Text/CSV
   - Chọn delimiter (dấu phẩy/chấm phẩy/...)

**Thực hành**:
- Tạo file CSV với dữ liệu mẫu, mở bằng Notepad++ và Excel, so sánh sự khác biệt
- Import file CSV vào Excel, chọn định dạng ngày tháng đúng
- Kiểm tra file JSON mẫu từ API, tìm lỗi cú pháp (VD: thiếu dấu phẩy)

---

## **Module 2: HTTP Status Codes**

### 📋 **Khái niệm và định nghĩa**

**HTTP Status Code** là mã số 3 chữ số mà server trả về để báo trạng thái của yêu cầu (request) từ client. Nó giúp xác định request thành công, thất bại, hay cần xử lý thêm.

**Phân loại chính**:
- **2xx (Success - Thành công)**: "Mọi thứ OK!"
- **3xx (Chuyển hướng)**: Client cần thực hiện thêm hành động, như chuyển đến URL mới
- **4xx (Lỗi từ phía client)**: Request sai (VD: URL không tồn tại, thông tin gửi sai)
- **5xx (Lỗi từ phía server)**: Server gặp vấn đề, không xử lý được request

**Các mã phổ biến**:
- **200 OK**: Request thành công hoàn toàn
  - Ví dụ: GET `/api/users` → trả về danh sách user
- **201 Created**: Request tạo mới dữ liệu (VD: thêm user) thành công
  - Ví dụ: POST `/api/users` → tạo user mới thành công
- **204 No Content**: Thành công nhưng không có data trả về
  - Ví dụ: DELETE `/api/users/123` → xóa thành công, không cần trả data
- **400 Bad Request**: Request sai cú pháp hoặc thiếu thông tin
- **401 Unauthorized**: Thiếu hoặc sai thông tin xác thực (VD: password sai)
- **404 Not Found**: Không tìm thấy tài nguyên (VD: endpoint không tồn tại)
- **422 Unprocessable Entity**: Request hợp lệ nhưng có lỗi validation (VD: thiếu thông tin)
- **429 Too Many Requests**: Client gửi request quá nhiều, server tạm thời không xử lý
- **500 Internal Server Error**: Server gặp lỗi nội bộ, không phải lỗi client
- **503 Service Unavailable**: Server tạm thời quá tải hoặc bảo trì
- **504 Gateway Timeout**: Server không phản hồi trong thời gian quy định

### 📌 **Vấn đề thường gặp**

1. **Nhầm lẫn 401 vs 403**:

   ```
   401 Unauthorized: "Bạn là ai?"
   → Cần đăng nhập

   403 Forbidden: "Tôi biết bạn là ai, nhưng bạn không được phép"
   → Cần quyền cao hơn
   ```
2. **Khi nào dùng 400 vs 422?**

   ```
   400 Bad Request: "Bạn gửi sai cú pháp"
   → Cần fix request

   422 Unprocessable Entity: "Bạn gửi đúng cú pháp, nhưng có lỗi validation"
   → Cần fix data
   ```

### 🛠️ **Thực hành**

- Dùng Postman gửi request đến httpbin.org (VD: GET `/status/200`, POST `/status/400`)
- Kiểm tra status code trong DevTools khi truy cập một trang web

**Công cụ kiểm tra**:
1. **Browser DevTools**:
   - Nhấn F12 → Network → reload trang → xem status code của mỗi request
2. **Postman**:
   - Gửi request → kiểm tra status code trong response
   - Viết test tự động trong tab Tests (VD: `pm.response.to.have.status(200)`)

**Cách đọc status code**:
```
GET /api/users/123
Response: 404 Not Found
→ User ID 123 không tồn tại.

POST /api/login
Response: 401 Unauthorized
→ Username/password sai.

GET /api/products
Response: 500 Internal Server Error
→ Server gặp lỗi, cần kiểm tra log.
```

## **Module 3: Công cụ so sánh file (Diff Tools)**

### 📋 **Khái niệm và định nghĩa**

**Diff Tools** là công cụ so sánh hai file hoặc đoạn văn bản để tìm ra sự khác biệt (thêm, xóa, sửa).

**Kết quả hiển thị**:
- Dòng bị xóa: Màu đỏ, dấu `-`
- Dòng được thêm: Màu xanh, dấu `+`
- Dòng bị sửa: Màu vàng, dấu `~` (tùy tool sử dụng)
- Dòng không đổi: Không highlight

**Ví dụ**:
```
File A:                File B:
ID: 1                  ID: 1
Name: A                Name: B   ← Sửa
Age: 25                Age: 25
                       Email: an@example.com ← Thêm
```

### 📌 **Tại sao cần biết và khi nào sử dụng**

Cần dùng diff tools để kiểm tra thay đổi và debug lỗi dễ dàng:
- **Debug lỗi**: So sánh config hoặc dữ liệu giữa các môi trường (dev, production) để tìm nguyên nhân bug
- **Test chính xác**: So sánh kết quả thực tế (actual) với kết quả mong đợi (expected)
- **Kiểm tra thay đổi**: Xác minh API response hoặc file config có đúng như yêu cầu không

**Ví dụ thực tế**:
- API trả về kết quả khác nhau giữa các môi trường
- Config file sai → dùng diff tool để tìm khác biệt
- So sánh dữ liệu test (trước và sau khi update)

### 🛠️ **Thực hiện như thế nào**

**Công cụ phổ biến**:
1. **VS Code**:
   - Mở 2 file → chuột phải → "Compare selected"
   - Hoặc Ctrl+Shift+P → "File: Compare Active File With..."
2. **WinMerge (Windows)**:
   - Kéo thả 2 file vào giao diện → tự động highlight khác biệt
3. **Diffchecker.com**:
   - Copy/paste 2 đoạn text (CSV, JSON) để so sánh online

**So sánh JSON**:
- Format JSON trước bằng VS Code hoặc jsonformatter.org
- Dùng diff tool để tìm khác biệt (VD: field bị thiếu, giá trị thay đổi)

**Thực hành**:
- So sánh 2 file JSON từ database
- Dùng VS Code hoặc Diffchecker để highlight khác biệt

---

## **Module 4: Cơ bản về AWS**

### 📋 **Khái niệm và định nghĩa**

1. **EC2 (Elastic Compute Cloud)**
  - Khái niệm: EC2 là dịch vụ cung cấp máy chủ ảo (virtual server) trên cloud computing platform của Amazon Web Services. EC2 cho phép người dùng thuê tài nguyên tính toán (CPU, RAM, Storage) theo nhu cầu và thanh toán theo mức sử dụng.

      ```
      Mua máy tính thật = Mua nhà
      - Phải trả tiền lớn một lần
      - Tự bảo trì, sửa chữa
      - Khó thay đổi cấu hình

      Thuê EC2 = Thuê nhà
      - Trả tiền theo tháng/giờ
      - Chủ nhà lo bảo trì
      - Dễ dàng chuyển nhà (thay đổi cấu hình)
      ```

2. **Security Group**:
  - Khái niệm: Security Group là bộ quy tắc kiểm soát truy cập vào EC2, quyết định ai được kết nối và qua cổng nào (VD: HTTP port 80, SSH port 22)

      ```
      Security Group giống như bảo vệ tòa nhà:
      - Kiểm tra ai được vào (Inbound Rules)
      - Kiểm tra ai được ra (Outbound Rules)
      - Có danh sách cho phép/từ chối
      ```

      ```
      Inbound Rules (Ai được vào?):
      - Port 80 (HTTP)    ← Từ Internet (0.0.0.0/0)
      - Port 443 (HTTPS)  ← Từ Internet (0.0.0.0/0)
      - Port 22 (SSH)     ← Chỉ từ IP công ty (1.2.3.4)

      Outbound Rules (Được đi đâu?):
      - All Ports ← Đi mọi nơi (0.0.0.0/0)
      ```
3. **IP Address - "Địa chỉ nhà"**
  - Private IP (IP nội bộ):
      ```
      Như số phòng trong tòa nhà:
      - 10.0.1.5 = Tòa A, Phòng 105
      - 10.0.2.10 = Tòa B, Phòng 210
      - Chỉ người trong tòa nhà biết
      ```


  - Public IP (IP công khai):
      ```
      Như địa chỉ tòa nhà:
      - 52.123.45.67 = Số 115 Võ Văn Tần
      - Ai cũng có thể gửi thư đến
      - Thay đổi khi restart EC2 (như chuyển nhà)
      ```

  - Elastic IP (IP cố định):
      ```
      Như thuê địa chỉ cố định:
      - Trả phí để giữ IP không đổi
      - Dễ nhớ
      ```

  - Ví dụ thực tế:
      ```
      Website bán hàng:
      - Private IP: 10.0.1.100 (server nội bộ)
      - Public IP: 54.123.45.67 (khách truy cập)
      - Elastic IP: 3.123.45.67 (đã trả phí để cố định)

      Khi restart server:
      - Private IP: không đổi
      - Public IP: có thể thành 54.200.10.30 (mới)
      - Elastic IP: vẫn là 3.123.45.67
      ```
4. **Domain - "Tên gọi dễ nhớ"**
  - Khái niệm: Domain là tên miền dễ nhớ thay cho IP cố định, giúp người dùng truy cập dễ dàng hơn.

      ```
      Domain giống như tên miền trong đời sống:
      Khó nhớ: http://54.123.45.67/shop
      Dễ nhớ: https://myshop.com
      ```

5. **VPC (Virtual Private Cloud)**
  - Khái niệm: VPC là mạng riêng ảo trên AWS, giúp tạo môi trường test riêng biệt, có thể kết nối với internet hoặc mạng nội bộ.

      ```
      VPC: Khu đô thị "MyCompany" (10.0.0.0/16)
      - Public Subnet: Khu thương mại (10.0.1.0/24)
        - Load Balancer (10.0.1.10)
        - Web Server (10.0.1.20)
      - Private Subnet: Khu dân cư (10.0.2.0/24)
        - App Server (10.0.2.10)
        - Database (10.0.2.20)
      ```
## **Module 5: Cơ bản về Git**

### 📋 **Khái niệm và định nghĩa**

**Git** là hệ thống quản lý phiên bản, lưu trữ lịch sử thay đổi của code hoặc tài liệu, cho phép nhiều người làm việc cùng lúc.

**Khái niệm chính**:
- **Repository (Repo)**: Thư mục dự án chứa tất cả code và lịch sử thay đổi
- **Commit**: Lưu một phiên bản thay đổi, kèm message mô tả (VD: "Fix login bug"), mỗi commit có ID duy nhất (hash)
- **Branch**: Nhánh riêng để làm việc, không ảnh hưởng nhánh chính (main). Ví dụ: `feature/login` để phát triển tính năng đăng nhập
- **Merge**: Gộp thay đổi từ nhánh phụ vào nhánh chính
- **Pull Request (PR)**: Đề xuất merge nhánh phụ vào nhánh chính, có thể kèm review

### 📌 **Tại sao cần biết và khi nào sử dụng**

Cần hiểu Git để hợp tác với team và theo dõi thay đổi:
- **Hợp tác nhóm**: Git giúp nhiều người làm việc trên cùng dự án mà không xung đột
- **Theo dõi thay đổi**: Xem ai sửa gì, khi nào, để điều tra bug hoặc review

**Thời điểm sử dụng**: Khi đối ứng các task coding/design/bug, ...

**Ví dụ thực tế**:
- Review PR để kiểm tra thay đổi trước khi merge
- Research bug → xem commit gần đây để tìm nguyên nhân
- Đối ứng feature mới → checkout branch tương ứng

### 🛠️ **Thực hiện như thế nào**

**Lệnh cơ bản**:
1. **Pull code mới**:
   ```bash
   git pull origin main
   # Cập nhật code mới nhất từ server.
   ```
2. **Kiểm tra trạng thái**:
   ```bash
   git status
   # Xem file nào đã thay đổi.
   ```
3. **Commit thay đổi**:
   ```bash
   git add .
   git commit -m "Update test data"
   # Lưu thay đổi với mô tả.
   ```
4. **Push code**:
   ```bash
   git push origin feature-branch
   # Gửi thay đổi lên server.
   ```
5. **Làm việc với branch**:
   ```bash
   git branch feature-login    # Tạo nhánh mới.
   git checkout feature-login  # Chuyển sang nhánh.
   git merge feature-login     # Merge nhánh vào main.
   ```

**Xem Pull Request**:
- Vào GitHub → tab "Pull Requests" → xem "Files changed" để kiểm tra thay đổi

**Thực hành**:
- Clone một repo mẫu
- Tạo branch mới, commit file test
- Tạo PR trên GitHub và xem thay đổi
- Resolve conflict đơn giản (VD: sửa file bị trùng)