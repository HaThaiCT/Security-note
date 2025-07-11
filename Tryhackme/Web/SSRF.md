
SSRF (Server Side Request Forgery) là lỗ hổng mà attacker khiến cho webserver gửi HTTP request đến 1 nơi mà attacker mong muốn
Có 2 loại
+ Regular SSRF : attacker nhìn được kết quả
+ Blind SSRF : attacker không nhìn được kết quả

Hậu quả
+ Truy cập vào những khu vực không được phép
+ Khả năng lây lan sang cả mạng LAN
+ Tiết lộ authentication tokens, các thông tin bảo mật quan trọng
![[Pasted image 20250614121351.png]]
Có thể kết hợp với lỗi path traversal
![[Pasted image 20250614122045.png]]
![[Pasted image 20250614122411.png]]
![[Pasted image 20250614122714.png]]


### Cách tìm và nhận biết
+ Khi sử dụng URL trên thanh tham số địa chỉ
![[Pasted image 20250614123405.png]]
+ Là 1 thuộc tính ẩn trong form
![[Pasted image 20250614123423.png]]

+ Một URL không đầy đủ như hostname
![[Pasted image 20250614123506.png]]
+ Một đường dẫn của URL:
![[Pasted image 20250614123529.png]]

### Phòng thủ

+ Deny list
+ Allow list
+ Kẻ tấn công có thể tận dụng Open redirect để chuyển hướng trang tới domain mà atttacker muốn. Cách này có thể vượt qua black list hay white list bởi vì máy chủ không kiểm soát được những thứ bên ngoài