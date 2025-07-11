# Introduction

## Linux structure

**Linux** là một **hệ điều hành**, giống như Windows, macOS, iOS hoặc Android. Một hệ điều hành (OS) là phần mềm quản lý tất cả các tài nguyên phần cứng của máy tính, tạo điều kiện giao tiếp giữa các ứng dụng phần mềm và các thành phần phần cứng. Không giống như một số hệ điều hành khác, Linux có nhiều bản phân phối khác nhau—thường được gọi là "distros"—là các phiên bản Linux được tùy chỉnh cho các nhu cầu và sở thích khác nhau.

### Lịch sử
Cái này tự tìm hiểu trên youtube các thứ ....

### Triết lý
Triết lý Linux tập trung vào sự **đơn giản**, **mô-đun hóa** và **tính mở**. Nó ủng hộ việc xây dựng các chương trình nhỏ, có mục đích đơn lẻ thực hiện tốt một tác vụ. Các chương trình này có thể được kết hợp theo nhiều cách khác nhau để thực hiện các hoạt động phức tạp, thúc đẩy hiệu quả và tính linh hoạt. Linux tuân theo năm nguyên tắc cốt lõi:

| Nguyên tắc                                                           | Mô tả                                                                                                                                                             |
| -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Mọi thứ đều là một tệp                                               | Tất cả các tệp cấu hình cho các dịch vụ khác nhau chạy trên hệ điều hành Linux đều được lưu trữ trong một hoặc nhiều tệp văn bản.                                 |
| Chương trình nhỏ, một mục đích duy nhất                              | Linux cung cấp nhiều công cụ khác nhau mà chúng ta sẽ làm việc cùng, có thể được kết hợp để làm việc cùng nhau.                                                   |
| Khả năng nối chuỗi các chương trình để thực hiện các tác vụ phức tạp | Việc tích hợp và kết hợp các công cụ khác nhau cho phép chúng ta thực hiện nhiều tác vụ lớn và phức tạp, chẳng hạn như xử lý hoặc lọc các kết quả dữ liệu cụ thể. |
| Tránh giao diện người dùng bị giam cầm                               | Linux được thiết kế để hoạt động chủ yếu với shell (hoặc terminal), điều này mang lại cho người dùng quyền kiểm soát lớn hơn đối với hệ điều hành.                |
| Dữ liệu cấu hình được lưu trữ trong một tệp văn bản                  | Một ví dụ về tệp như vậy là tệp /etc/passwd, lưu trữ tất cả người dùng đã đăng ký trên hệ thống.                                                                  |
### Các thành phần

| Bootloader      | Một đoạn mã chạy để hướng dẫn quá trình khởi động để bắt đầu hệ điều hành. Parrot Linux sử dụng GRUB Bootloader.                                                                                                                                                                                                                 |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OS Kernel       | Kernel là thành phần chính của một hệ điều hành. Nó quản lý các tài nguyên cho các thiết bị I/O của hệ thống ở cấp độ phần cứng.                                                                                                                                                                                                 |
| Daemons         | Các dịch vụ chạy ngầm được gọi là "daemons" trong Linux. Mục đích của chúng là đảm bảo rằng các chức năng chính như lập lịch, in ấn và đa phương tiện đang hoạt động chính xác. Các chương trình nhỏ này tải sau khi chúng ta khởi động hoặc đăng nhập vào máy tính.                                                             |
| OS Shell        | Shell hệ điều hành hoặc trình thông dịch ngôn ngữ lệnh (còn được gọi là dòng lệnh) là giao diện giữa hệ điều hành và người dùng. Giao diện này cho phép người dùng ra lệnh cho hệ điều hành làm gì. Các shell được sử dụng phổ biến nhất là Bash, Tcsh/Csh, Ksh, Zsh và Fish.                                                    |
| Graphics server | Điều này cung cấp một hệ thống con đồ họa (máy chủ) được gọi là "X" hoặc "X-server" cho phép các chương trình đồ họa chạy cục bộ hoặc từ xa trên hệ thống X-windowing.                                                                                                                                                           |
| Window Manager  | Còn được gọi là giao diện người dùng đồ họa (GUI). Có nhiều tùy chọn, bao gồm GNOME, KDE, MATE, Unity và Cinnamon. Một môi trường desktop thường có một số ứng dụng, bao gồm trình duyệt tệp và web. Chúng cho phép người dùng truy cập và quản lý các tính năng và dịch vụ thiết yếu và thường xuyên truy cập của hệ điều hành. |
| Utilities       | Các ứng dụng hoặc tiện ích là các chương trình thực hiện các chức năng cụ thể cho người dùng hoặc một chương trình khác.                                                                                                                                                                                                         |

### Linux Architecture
Hệ điều hành Linux có thể được chia thành các lớp:

| Lớp            | Mô tả                                                                                                                                                                                                                                                                                                                       |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hardware       | Các thiết bị ngoại vi như RAM, ổ cứng, CPU của hệ thống và các thiết bị khác.                                                                                                                                                                                                                                               |
| Kernel         | Phần cốt lõi của hệ điều hành Linux có chức năng ảo hóa và kiểm soát các tài nguyên phần cứng máy tính thông thường như CPU, bộ nhớ được cấp phát, dữ liệu được truy cập và các tài nguyên khác. Kernel cung cấp cho mỗi tiến trình các tài nguyên ảo riêng và ngăn chặn/giảm thiểu xung đột giữa các tiến trình khác nhau. |
| Shell          | Một giao diện dòng lệnh (CLI), còn được gọi là shell mà người dùng có thể nhập lệnh vào để thực thi các chức năng của kernel.                                                                                                                                                                                               |
| System Utility | Cung cấp cho người dùng tất cả các chức năng của hệ điều hành.                                                                                                                                                                                                                                                              |

### File system hierachy
![[Pasted image 20250708210902.png]]

| Đường dẫn | Mô tả                                                                                                                                                                                                                                                                                                                                                |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| /         | Thư mục cấp cao nhất là hệ thống tệp gốc và chứa tất cả các tệp cần thiết để khởi động hệ điều hành trước khi các hệ thống tệp khác được gắn kết, cũng như các tệp cần thiết để khởi động các hệ thống tệp khác. Sau khi khởi động, tất cả các hệ thống tệp khác được gắn kết tại các điểm gắn kết tiêu chuẩn dưới dạng thư mục con của thư mục gốc. |
| /bin      | Chứa các binary lệnh thiết yếu.                                                                                                                                                                                                                                                                                                                      |
| /boot     | Bao gồm bootloader tĩnh, kernel executable và các tệp cần thiết để khởi động hệ điều hành Linux.                                                                                                                                                                                                                                                     |
| /dev      | Chứa các tệp thiết bị để tạo điều kiện truy cập vào mọi thiết bị phần cứng được gắn vào hệ thống.                                                                                                                                                                                                                                                    |
| /etc      | Các tệp cấu hình hệ thống cục bộ. Các tệp cấu hình cho các ứng dụng đã cài đặt cũng có thể được lưu ở đây.                                                                                                                                                                                                                                           |
| /home     | Mỗi người dùng trên hệ thống đều có một thư mục con ở đây để lưu trữ.                                                                                                                                                                                                                                                                                |
| /lib      | Các tệp thư viện chia sẻ cần thiết cho quá trình khởi động hệ thống.                                                                                                                                                                                                                                                                                 |
| /media    | Các thiết bị truyền thông di động bên ngoài như ổ USB được gắn kết ở đây.                                                                                                                                                                                                                                                                            |
| /mnt      | Điểm gắn kết tạm thời cho các hệ thống tệp thông thường.                                                                                                                                                                                                                                                                                             |
| /opt      | Các tệp tùy chọn như các công cụ của bên thứ ba có thể được lưu ở đây.                                                                                                                                                                                                                                                                               |
| /root     | Thư mục chính của người dùng root.                                                                                                                                                                                                                                                                                                                   |
| /sbin     | Thư mục này chứa các executable được sử dụng để quản lý hệ thống (tệp hệ thống nhị phân).                                                                                                                                                                                                                                                            |
| /tmp      | Hệ điều hành và nhiều chương trình sử dụng thư mục này để lưu trữ tệp tạm thời. Thư mục này thường được xóa khi hệ thống khởi động và có thể bị xóa vào những thời điểm khác mà không có bất kỳ cảnh báo nào.                                                                                                                                        |
| /usr      | Chứa các executable, thư viện, tệp man, v.v.                                                                                                                                                                                                                                                                                                         |
| /var      | Thư mục này chứa các tệp dữ liệu biến đổi như tệp nhật ký, hộp thư đến email, các tệp liên quan đến ứng dụng web, tệp cron, v.v.                                                                                                                                                                                                                     |

## Các bản phân phối Linux

Các bản phân phối Linux — hay **distros** — là các hệ điều hành dựa trên **kernel Linux**. Chúng được sử dụng cho nhiều mục đích khác nhau, từ máy chủ và thiết bị nhúng đến máy tính để bàn và điện thoại di động. Mỗi bản phân phối Linux đều khác nhau, với bộ tính năng, gói và công cụ riêng. Một số ví dụ phổ biến bao gồm:
- Ubuntu
- Fedora
- CentOS
- Debian
- Red Hat Enterprise Linux
### Debian
Cái này tự tìm hiểu

## Giới thiệu về shell

Cái này tự tìm hiểu

### Mô tả các câu lệnh

Ở đầu mỗi dòng lệnh đều có dạng `<username>@<hostname><current working directory>$`
Nếu là root thì có dạng `root@htb[/htb]#`

### Dấu nhắc
Giúp hiển thị những thông tin cần thiết trước mỗi lệnh, mặc định là có username, password và current working directory

| Ký tự đặc biệt | Mô tả                                          |
| -------------- | ---------------------------------------------- |
| \d             | Ngày (Thứ Hai, 6 tháng 2)                      |
| \D{%Y-%m-%d}   | Ngày (YYYY-MM-DD)                              |
| \H             | Tên máy chủ đầy đủ                             |
| \j             | Số lượng công việc được quản lý bởi shell      |
| \n             | Dòng mới                                       |
| \r             | Xuống dòng và về đầu dòng                      |
| \s             | Tên của shell                                  |
| \t             | Thời gian hiện tại 24 giờ (HH:MM:SS)           |
| \T             | Thời gian hiện tại 12 giờ (HH:MM:SS)           |
| \@             | Thời gian hiện tại                             |
| \u             | Tên người dùng hiện tại                        |
| \w             | Đường dẫn đầy đủ của thư mục làm việc hiện tại |
## Getting Help

Sử dụng lệnh `man` hoặc tùy chọn `--help`
Một trang web giải thích tập lệnh hữu ích : https://explainshell.com/

### System Information

Dưới đây là 1 số lệnh lấy thông tin hệ thống cơ bản: 

| Lệnh     | Mô tả                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------- |
| whoami   | Hiển thị tên người dùng hiện tại.                                                                                          |
| id       | Trả về định danh người dùng.                                                                                               |
| hostname | Đặt hoặc in tên của hệ thống máy chủ hiện tại.                                                                             |
| uname    | In thông tin cơ bản về tên hệ điều hành và phần cứng hệ thống.                                                             |
| pwd      | Trả về tên thư mục làm việc.                                                                                               |
| ifconfig | Tiện ích ifconfig được sử dụng để gán hoặc xem địa chỉ cho một giao diện mạng và/hoặc cấu hình các tham số giao diện mạng. |
| ip       | ip là một tiện ích để hiển thị hoặc thao tác định tuyến, thiết bị mạng, giao diện và đường hầm.                            |
| netstat  | Hiển thị trạng thái mạng.                                                                                                  |
| ss       | Một tiện ích khác để điều tra các socket.                                                                                  |
| ps       | Hiển thị trạng thái tiến trình.                                                                                            |
| who      | Hiển thị ai đang đăng nhập.                                                                                                |
| env      | In môi trường hoặc đặt và thực thi lệnh.                                                                                   |
| lsblk    | Liệt kê các thiết bị khối.                                                                                                 |
| lsusb    | Liệt kê các thiết bị USB.                                                                                                  |
| lsof     | Liệt kê các tệp đã mở.                                                                                                     |
| lspci    | Liệt kê các thiết bị PCI.                                                                                                  |
### Đăng nhập thông qua SSH
**Secure Shell (SSH)** đề cập đến một giao thức cho phép máy khách truy cập và thực thi lệnh hoặc hành động trên các máy tính từ xa. Trên các máy chủ và máy chủ dựa trên Linux, cũng như các hệ điều hành giống Unix khác, **SSH** là một trong những công cụ tiêu chuẩn được cài đặt vĩnh viễn và là lựa chọn ưu tiên của nhiều quản trị viên để cấu hình và bảo trì máy tính thông qua truy cập từ xa. Nó là một giao thức cũ và đã được chứng minh rất nhiều, không yêu cầu hoặc cung cấp **giao diện người dùng đồ họa (GUI)**. Vì lý do này, nó hoạt động rất hiệu quả và chiếm rất ít tài nguyên.
