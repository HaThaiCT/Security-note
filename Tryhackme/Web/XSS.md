Lỗi xảy ra khi nội dung của request từ client (untrusted data) rơi vào đoạn mã nguồn của server


### Reflected XSS

- **Mô tả:** Mã độc không được lưu trữ mà được phản hồi lại từ server qua URL hoặc input người dùng. Nó thường xảy ra khi server trả lại dữ liệu đầu vào không được lọc.
    
- **Ví dụ:** Tấn công qua URL:
```php
http://example.com/search?q=<script>alert("XSS")</script>

```

- **Nguy hiểm:** Không tồn tại lâu, chỉ ảnh hưởng nếu người dùng click vào liên kết độc.
![[Pasted image 20250702231303.png]]


Thằng hacker lừa để mớm cho máy nạn nhân chạy mã JS mà nó đã chuẩn bị trước

Cần phải kiểm tra kĩ:
+ Parameter trong URL query
+ URL file path
+ HTTP headers(ít khả năng xảy ra)

### Stored XSS
- **Mô tả:** Mã độc được lưu trữ vĩnh viễn trong cơ sở dữ liệu, tệp tin, hoặc bất kỳ nơi lưu trữ nào trên server.
    
- **Ví dụ:** Một bình luận chứa script độc được lưu trong CSDL. Khi người khác xem bài viết, script được tải và thực thi.
    
- **Nguy hiểm:** Rất nguy hiểm vì mã độc tồn tại lâu dài và ảnh hưởng đến nhiều người dùng.
![[Pasted image 20250702231953.png]]
### DOM Based XSS

### Blind XSS