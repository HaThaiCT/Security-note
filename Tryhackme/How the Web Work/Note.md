# DNS in detail

## Khái niệm 

+ DNS (Domain Name System) : là 1 hệ thống chuyển đổi tên miền(domain name) thành địa chỉ IP để các thiết bị có thể giao tiếp với nhau trên mạng
## Domain Hierachy

+ TLD : Top-Level Domain : Là phần bên phải cùng của 1 tên miền như .com , .edu, .vn,..... TLD bao gồm 2 loại chính
	+ gTLD : Dùng để xác định theo mục đích của website(VD : .com : thương mại, .edu giáo dục,...)
	+ ccTLD : Dùng để xác định theo vị trí của website(.vn, .ca,.co.uk,...)
+ Second-Level Domain : Là phần bên trái của TLD, chỉ được tối đa 63 kí tự, là tên riêng của website
+ Subdomain : Nằm bên trái của second-level domain, cách bằng dấu '.', dùng để tổ chức nội dung hay phân nhánh website
## Record Types

+ A Record : Chuyển đổi tên miền thành địa chỉ IPv4
+ AAAA Record : chuyển đổi tên miền thành địa chỉ IPv6
+ CNAME Record : Trỏ 1 tên miền đến 1 tên miền khác
+ MX Record : Xác định máy chủ xử lý email cho 1 tên miền
+ TXT Record : Lưu dữ liệu văn bản
## Making a request

+ Kiểm tra bộ nhớ cache cục bộ (Local Cache Lookup) : Kiểm tra cache DNS cục bộ xem liệu đã có bản ghi DNS cho tên miền này chưa, nếu có thì sẽ lấy luôn IP từ cache
+ Gửi yêu cầu đến Recursive DNS Server: Nêu địa chỉ không có trong bộ nhớ cache, máy tính sẽ gửi yêu cầu đến Recursive DNS Server. Máy chủ này cũng có bộ nhớ cache và nó kiểm tra xem DNS có lưu trong cache hay không. Server này được cung cấp bởi nhà cung cấp dịch vụ Internet
+ Nếu Recursive DNS Server thực hiện truy vấn phân cấp qua các bước :
	+ Gửi yêu cầu đến Root Server giúp xác định TLD và chuyển hướng đến TLD Server phù hợp
	+ TLD Server xác định máy chủ tên miền (Name Server), tìm được Authoritative Name Server của tên miền
	+ Truy vấn đến Authoritative DNS Server : máy chủ này chịu trách nhiệm lưu trữ bản ghi DNS của tên miền
+ Trả kết quả về cho client và lưu vào cache
![[Pasted image 20250216173826.png]]

# HTTP
+ Tập hợp quy tắc quy tắc để giao tiếp với web server

### Request and response

+ URL : là 1 chuỗi ký tự giúp trình duyệt biết cách truy cập 1 tài nguyên trên Internet.
	+ Scheme : xác định giao thức (protocol) được sử dụng để truy cập tài nguyên
	+ User : người dùng(không phổ biến)
	+ Host : Tên miền/ IP máy chủ
	+ Port : Cổng mà trình duyệt kết nối tới
	+ Path : Định vị tài nguyên trên máy chủ
	+ Query String : Gửi thêm thông tin đến máy chủ, thường viết sau dấu `?`
	+ Fragment : Xác định vị trí cụ thể trên trang web
+ 