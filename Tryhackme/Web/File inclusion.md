
Cấu tạo của 1 URL:
![[Pasted image 20250613002943.png]]

GET request
![[Pasted image 20250613003227.png]]

Việc không lọc kĩ dữ liệu đầu vào khiến hacker có thể chèn các tệp nguy hiểm gây hại cho hệ thống
Một khi có thể đưa tệp nhạy cảm vào hệ thống, rất có thể hacker sẽ chiếm được quyền và thực hiện RCE.

### Path traversal

+ Hacker tận dụng URL của web để định vị và truy cập trái phép vào các đường dẫn/ thư mục/ tệp được lưu trữ bên ngoài thư mục gốc của ứng dụng web
+ Lỗ hổng này thường xuất hiện khi untrusted data rời vào hàm file_get_contents trong PHP
![[Pasted image 20250613004508.png]]
![[Pasted image 20250613004932.png]]
![[Pasted image 20250613005001.png]]

+ Tương tự, với hệ điều hành window, hacker có thể dùng các đường dẫn như `http://webapp.thm/get.php?file=../../../../boot.ini`hoặc `http://webapp.thm/get.php?file=../../../../windows/win.ini` để đọc nội dung file `boot.ini` 
+ Dưới đây là bảng gồm 1 số đường dẫn các tệp nhạy cảm trên hệ điều hành

|                               |                                                                                                                                                                   |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Location**                  | **Description**                                                                                                                                                   |
| `/etc/issue`                  | contains a message or system identification to be printed before the login prompt.                                                                                |
| `/etc/profile`                | controls system-wide default variables, such as Export variables, File creation mask (umask), Terminal types, Mail messages to indicate when new mail has arrived |
| `/proc/version`               | specifies the version of the Linux kernel                                                                                                                         |
| `etc/passwd`                  | has all registered users that have access to a system                                                                                                             |
| `/etc/shadow`                 | contains information about the system's users' passwords                                                                                                          |
| `/root/.bash_history`         | contains the history commands for `root` user                                                                                                                     |
| `/var/log/dmessage`           | contains global system messages, including the messages that are logged during system startup                                                                     |
| `/var/mail/root`              | all emails for `root` user                                                                                                                                        |
| `/root/.ssh/id_rsa`           | Private SSH keys for a root or any known valid user on the server                                                                                                 |
| `/var/log/apache2/access.log` | the accessed requests for `Apache` web server                                                                                                                     |
| `C:\boot.ini`                 | contains the boot options for computers with BIOS firmware                                                                                                        |
### Local file inclusion (LFI)

LFI (Local File Inclusion) hay **chèn file cục bộ** là một **lỗ hổng bảo mật web** cho phép kẻ tấn công chèn (include) các file nằm trên máy chủ vào quá trình xử lý của ứng dụng web. LFI thường xảy ra khi ứng dụng web nhận đầu vào từ người dùng (ví dụ: tên file) và sử dụng đầu vào này trong hàm include, require, hoặc các hàm tương tự mà **không kiểm tra, lọc kỹ lưỡng**.

Ví dụ:
Giả sử trang web cho tùy chọn ngôn ngữ
```php
<?PHP 
	include($_GET["lang"]);
?>
```
`http://webapp.thm/index.php?lang=language` : Với mỗi lang thì file php sẽ include file php của chính language đó(VD : `eng.php`, `vietnamese.php`,...)

Ta hoàn toàn có thể include và đọc bất kỳ file nào trong hệ thống nếu lập trình viên không validate dữ liệu. Ví dụ `http://webapp.thm/get.php?file=/etc/passwd` ta có thể đọc được file /etc/passwd

Ta hoàn toàn có thể kết hợp lỗi này với kĩ thuật path traversal.
Ví dụ :
```php
<?PHP 
	include("languages/". $_GET['lang']); 
?>
```

Ta có thể để payload `lang=../../../../etc/passwd`

Level 3
Có thể dev đã nối đuôi `.php` ở cuối file cần include dẫn tới việc xem file passwd của ta biến thành việc xem file `passwd.php` và sẽ xảy ra lỗi
````php
Warning: include(languages/../../../../../etc/passwd.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
````
=> Cách để vượt qua: Sử dụng ký tự NULL BYTE `%00`. Nó giúp đánh dấu cho việc kết thúc 1 chuỗi, sau ký tự này dù còn ký tự nào đi chăng nữa thì nó sẽ bỏ qua. Khi đó hàm include sẽ là `include("languages/../../../../../etc/passwd%00").".php");` vã sẽ tương đương với  `include("languages/../../../../../etc/passwd");` 

Level 4
Trick : Dùng ký tự `/.` chèn vào cuối đường dẫn để vượt qua filter mà vẫn giữ nguyên file muốn đọc

Level 5
Dev làm sạch input bằng cách thay tất cả các ký tự `../` thành xâu rỗng
Trick : Dùng path có dạng `....//....//....//....//....//etc/passwd`. Khi đó, sau khi làm sạch dữ liệu thì xâu sẽ trở thành `../../../../etc/passwd`
![[Pasted image 20250613232058.png]]


### Remote File Inclusion (RFI)

+ Nguyên nhân dẫn đến lỗ hổng này cũng do các hàm như `include` giống như LFI nhưng đường dẫn mà hacker chèn vào là 1 file ở server khác(do hacker chuẩn bị trước). Điều này sẽ làm cho đoạn code mà hacker đã chuẩn bị sẵn ở file trong server riêng được thực thi trên server mục tiêu. Hacker lúc này hoàn toàn có quyền RCE hệ thống
+ Điều kiện để hacker có thể khai thác được đó là trong setting của PHP thì `allow_url_fopen` phải để `on`

![[Pasted image 20250614000305.png]]
Link file tấn công : 