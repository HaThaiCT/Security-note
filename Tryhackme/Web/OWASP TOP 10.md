 1. Broken Access Control

### Khái niệm
**Broken Access Control** xảy ra khi một hệ thống **không thực thi đúng các quy tắc kiểm soát quyền truy cập**, cho phép người dùng **truy cập vào các tài nguyên hoặc chức năng mà họ không được phép**.

**Ví dụ đơn giản:**  
Một người dùng bình thường truy cập vào trang `/admin` mà không cần đăng nhập với quyền quản trị viên, và có thể xem hoặc sửa dữ liệu của người khác. Điều đó cho thấy kiểm soát truy cập đã bị "broken" (phá vỡ).

### Các dạng lỗi phổ biến

| Dạng lỗi                                     | Giải thích                                                                                   |
| -------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **IDOR (Insecure Direct Object References)** | Truy cập tài nguyên bằng cách đoán hoặc thay đổi ID. VD: `/user/123`, đổi thành `/user/124`. |
| **Forced Browsing**                          | Truy cập URL ẩn hoặc bị cấm mà không qua kiểm tra quyền.                                     |
| **Privilege Escalation**                     | Người dùng tăng quyền truy cập (ví dụ: từ user thành admin) bất hợp pháp.                    |
| **Missing Function-Level Access Control**    | Không kiểm tra quyền người dùng khi gọi một chức năng backend.                               |
| **CORS misconfigurations**                   | Cho phép trang web bên ngoài truy cập API mà không kiểm tra nguồn gốc.                       |
# 2. Cryptographic Failure

### Khái niệm
**Cryptographic Failures** là lỗ hổng xảy ra khi **dữ liệu nhạy cảm không được mã hóa đúng cách**, hoặc **thiếu mã hóa**, dẫn đến nguy cơ bị rò rỉ, đánh cắp hoặc chỉnh sửa dữ liệu trong quá trình truyền hoặc lưu trữ.

> 📌 Dữ liệu nhạy cảm bao gồm: mật khẩu, token xác thực, thông tin thẻ tín dụng, thông tin cá nhân (PII), hồ sơ sức khỏe, v.v.

### Nguyên nhân
| Nguyên nhân                                  | Giải thích                                                              |
| -------------------------------------------- | ----------------------------------------------------------------------- |
| ❌ Không sử dụng HTTPS                        | Dữ liệu truyền đi không được mã hóa, dễ bị nghe lén (MITM).             |
| 🔓 Mật khẩu lưu trữ dưới dạng _plain text_   | Mật khẩu không được băm hoặc mã hóa an toàn.                            |
| 🧂 Thiếu **salt** khi băm mật khẩu           | Làm cho việc tấn công brute-force hoặc rainbow table dễ dàng hơn.       |
| 🔁 Sử dụng thuật toán mã hóa yếu             | Dùng MD5, SHA-1, hoặc DES đã lỗi thời và dễ bị phá vỡ.                  |
| 📤 Mã hóa nhưng lưu khóa ở nơi không an toàn | Khóa mã hóa nằm trong code, dễ bị lộ nếu hacker truy cập được mã nguồn. |
| 🗝️ Quản lý khóa kém                         | Không xoay vòng khóa định kỳ, không bảo vệ khóa đúng cách.              |
### Tác hại
- Dữ liệu người dùng bị **rò rỉ**, **đánh cắp**, hoặc **thay đổi**.
- Mật khẩu có thể bị giải mã nếu hacker truy cập được database.
- Hacker có thể thực hiện **tấn công Man-in-the-Middle (MITM)**.
- Vi phạm nghiêm trọng **quy định bảo mật (VD: GDPR, PCI DSS)** dẫn đến phạt nặng.

### Cách phòng chống

| Cách phòng tránh                                    | Mô tả ngắn gọn                                  |
| --------------------------------------------------- | ----------------------------------------------- |
| ✅ Luôn sử dụng HTTPS (TLS 1.2 hoặc 1.3)             | Mã hóa dữ liệu khi truyền qua mạng.             |
| ✅ Băm mật khẩu với thuật toán mạnh (bcrypt, Argon2) | Không bao giờ lưu mật khẩu gốc (plain text).    |
| ✅ Thêm salt khi băm                                 | Giúp tránh tấn công với rainbow table.          |
| ✅ Tránh dùng thuật toán mã hóa yếu (MD5, SHA-1)     | Dùng AES-256, SHA-256 trở lên.                  |
| ✅ Bảo vệ khóa mã hóa                                | Lưu trong môi trường an toàn (vault, env file). |
| ✅ Hạn chế lưu dữ liệu nhạy cảm nếu không cần thiết  | Giảm thiểu rủi ro khi bị tấn công.              |
# 3. Injection

Cái này quá nhiều rồi không note nữa =))))


# 4. Insecure design

### Khái niệm
**Insecure Design** là khi ứng dụng hoặc hệ thống được thiết kế **thiếu các biện pháp bảo mật phù hợp**, tạo điều kiện cho hacker khai thác, ngay cả khi lập trình và cấu hình đều đúng kỹ thuật.
📌 Nói cách khác: "Viết code đúng nhưng **viết đúng một thiết kế sai**."

### 1 số tình huống thường gặp

| Tình huống                                                  | Mô tả                                                                      |
| ----------------------------------------------------------- | -------------------------------------------------------------------------- |
| 🔓 **Không xác thực quyền trước hành động nhạy cảm**        | Ví dụ: không kiểm tra người dùng có phải chủ tài khoản khi thay đổi email. |
| ❌ **Không giới hạn số lần đăng nhập sai**                   | Hacker có thể brute-force mật khẩu vô hạn lần.                             |
| 🧾 **Cho phép tải lên file nhưng không kiểm tra loại file** | Người dùng tải lên `.php`, hacker chạy shell.                              |
| 🗺️ **Thiết kế logic business sai**                         | Ví dụ: website cho phép thay đổi số tiền phải thanh toán qua request.      |
| 👁️ **Không có quy trình bảo vệ dữ liệu nhạy cảm**          | Ví dụ: không có cơ chế ẩn/ẩn số thẻ tín dụng khi hiển thị lại.             |
### Cách phòng chống

| Biện pháp                                                 | Mô tả                                                             |
| --------------------------------------------------------- | ----------------------------------------------------------------- |
| ✅ **Security by design**                                  | Tích hợp bảo mật ngay từ giai đoạn thiết kế hệ thống.             |
| ✅ **Threat modeling**                                     | Phân tích các mối đe dọa tiềm ẩn trong kiến trúc trước khi code.  |
| ✅ **Xác định rõ quyền truy cập và hành vi người dùng**    | Gắn chức năng theo vai trò rõ ràng (RBAC).                        |
| ✅ **Đưa ra quy tắc kinh doanh (business rules) chặt chẽ** | Ví dụ: người mua không thể tự sửa giá tiền.                       |
| ✅ **Kiểm thử logic ứng dụng (Business Logic Testing)**    | Không chỉ kiểm thử lỗi kỹ thuật mà còn kiểm thử hành vi sai lệch. |
# 5. Security Misconfiguration

### Khái niệm

**Security Misconfiguration** là khi hệ thống, server, ứng dụng hoặc mạng có **thiết lập bảo mật sai, thiếu sót, hoặc không được cấu hình đầy đủ**, khiến nó dễ bị tấn công.

> Ví dụ: mở cổng không cần thiết, để **trang quản trị public**, dùng **mật khẩu mặc định**, hoặc **hiển thị thông báo lỗi chi tiết cho người dùng**.

### 1 số trường hợp dính
| Tình huống sai cấu hình                  | Mô tả                                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------- |
| 🛠️ **Dùng cấu hình mặc định**           | Tài khoản admin mặc định như `admin:admin`, `root:toor`,...               |
| 🔓 **Để dashboard quản trị public**      | Ví dụ: `http://example.com/phpmyadmin` hoặc `/admin` không cần đăng nhập. |
| 🗂️ **File nhạy cảm công khai**          | `.env`, `.git/`, `config.php` hiển thị công khai trên web.                |
| 🧯 **Bật debug/verbose trên production** | Hiển thị lỗi với stack trace ⇒ hacker biết cấu trúc hệ thống.             |
| 🧰 **Cài dịch vụ không cần thiết**       | Mở cổng SSH, FTP, hoặc RDP mà không dùng đến.                             |
| 🧪 **Không tắt chức năng test/demo**     | Một số hệ thống để nguyên script mẫu có lỗ hổng.                          |
| 📦 **Không cập nhật phần mềm/công cụ**   | Dùng version cũ có lỗ hổng đã biết (exploitable CVE).                     |
# 6.Vulnerable and Outdated Components

Đây là lỗ hổng xảy ra khi hệ thống phần mềm sử dụng:

- **Phiên bản cũ** của thư viện, framework, hoặc phần mềm.
    
- **Thành phần có lỗ hổng đã biết** (có mã CVE).
    
- Không cập nhật kịp thời khi có bản vá bảo mật.
    
- Hoặc không xác minh tính an toàn của các thư viện được sử dụng.
    

> 👉 Nói đơn giản: **dùng phiên bản cũ, chưa vá lỗi bảo mật hoặc không rõ nguồn gốc**.
> => Hacker có thể dễ dàng tấn công mà không cần nỗ lực nhiều


# 7.Identification and Authentication Failures

Lỗi này liên quan đến việc xác minh danh tính và Authentication

### Các trường hợp dính đạn
| Dạng lỗi                                        | Mô tả                                                             |
| ----------------------------------------------- | ----------------------------------------------------------------- |
| ❌ **Không giới hạn số lần đăng nhập sai**       | Dễ bị brute-force mật khẩu                                        |
| ❌ **Mật khẩu yếu hoặc mặc định**                | Ví dụ: admin/admin, 123456                                        |
| ❌ **Quản lý session kém**                       | Không hết hạn session sau logout hoặc bị đánh cắp cookie          |
| ❌ **Gửi mật khẩu qua HTTP hoặc lưu plain text** | Hacker có thể chặn hoặc đọc trực tiếp                             |
| ❌ **Bỏ qua xác thực ở backend**                 | Chỉ kiểm tra quyền trên client-side (JS)                          |
| ❌ **Lỗi logic đăng nhập**                       | Ví dụ: user có thể đăng nhập chỉ bằng username không cần mật khẩu |
| ❌ **Không kiểm tra token hoặc OTP đúng cách**   | Hacker có thể đoán hoặc vượt qua bước xác thực 2 yếu tố           |
### Biện pháp
| Biện pháp                                           | Mô tả                                                          |
| --------------------------------------------------- | -------------------------------------------------------------- |
| ✅ **Giới hạn số lần đăng nhập sai (rate limiting)** | Dùng delay, CAPTCHA hoặc khóa tài khoản tạm thời               |
| ✅ **Băm mật khẩu với thuật toán mạnh**              | Dùng `bcrypt`, `scrypt`, `argon2`, không lưu plain text        |
| ✅ **Hết hạn session đúng cách**                     | Tự động logout sau X phút không hoạt động                      |
| ✅ **Dùng HTTPS bắt buộc**                           | Tránh bị chặn thông tin đăng nhập qua mạng                     |
| ✅ **Bảo vệ token xác thực (JWT, cookie)**           | Không lưu token trong localStorage, nên dùng `HttpOnly` cookie |
| ✅ **Kiểm tra xác thực ở phía server**               | Không bao giờ tin vào client-side                              |
| ✅ **Thêm xác thực 2 yếu tố (2FA)**                  | Đặc biệt với tài khoản admin hoặc người dùng quan trọng        |
# 8. Software and Data Integrity Failures

Lỗi này liên quan đến tính toàn vẹn dữ liệu
Do hệ thống **không xác minh dữ liệu có bị chỉnh sửa hay giả mạo không**, tạo điều kiện cho hacker **chèn mã độc, script độc hại, hoặc dữ liệu bị thay đổi**.

# 9. Security Logging and Monitoring Failures

Lỗi liên quan đến ghi log và giám sát an ninh


# 10. Server-Side Request Forgery

