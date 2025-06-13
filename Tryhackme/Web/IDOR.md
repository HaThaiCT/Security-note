
IDOR (Insecure Direct Object Reference) : Lỗi kiểu access control, vì việc quá tin tưởng vào input của người dùng khiến họ có thể truy cập thẳng vào các Object nhạy cảm

+ Encoded IDs : Decode data sau đó sửa đổi rồi encode lại để gửi lại cho server

![[Pasted image 20250612155658.png]]


+ Hashes IDs: Sử dụng https://crackstation.net/ để tìm xem có mã băm nào có thể giải mã ra không và sửa đổi nó giống như encode

+ Có thể tạo ra 2 tài khoản khác nhau và dùng 1 tài khoản để truy cập xem thông tin của tài khoản còn lại. Nếu xem được thì có thể phát hiện lỗ hổng IDOR
+ Dùng path/ tham số khả nghi để truyền vào URL