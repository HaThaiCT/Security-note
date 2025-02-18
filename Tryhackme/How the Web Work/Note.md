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

## Request and response
![[Pasted image 20250217172843.png]]
+ URL : là 1 chuỗi ký tự giúp trình duyệt biết cách truy cập 1 tài nguyên trên Internet.
	+ Scheme : xác định giao thức (protocol) được sử dụng để truy cập tài nguyên
	+ User : người dùng(không phổ biến)
	+ Host : Tên miền/ IP máy chủ
	+ Port : Cổng mà trình duyệt kết nối tới
	+ Path : Định vị tài nguyên trên máy chủ
	+ Query String : Gửi thêm thông tin đến máy chủ, thường viết sau dấu `?`
	+ Fragment : Xác định vị trí cụ thể trên trang web
+ Khi truy cập 1 trang web, trình duyệt gửi HTTP Request và nhận lại HTTP Response từ máy chủ
+ Cấu trúc của HTTP Request : 
		![[Pasted image 20250217174556.png]]
	+ Dòng 1 : Gửi đi Get method, sử dụng HTTP version 1.1
	+ Dòng 2 : Nói với server rằng tôi muốn website tryhackme.com
	+ Dòng 3 : Nói với server rằng tôi đang sử dụng trình duyệt Firefox version 87
	+ Dòng 4 : Nói với server rằng `https://tryhackme.com` trước đó đã giới thiệu tôi đến yêu cầu này
	+ Dòng 5 : 1 dòng trống báo hiệu yêu cầu đã hoàn tất
+ Cấu trúc của HTTP Response :
		![[Pasted image 20250217174932.png]]
	+ Dòng 1 : Phiên bản HTTP và mã trạng thái(status code) `200 OK`
	+ Dòng 2 : Phiên bản và phần mềm server đang sử dụng
	+ Dòng 3 : Thời gian thực mà máy chủ phản hồi
	+ Dòng 4 : Content-Type : kiểu nội dung phản hồi
	+ Dòng 5 : Content-Length : Đội dài của nội dung phản hồi (tính theo byte)
	+ Dòng 6 : Dòng trống : Xác định kết thúc phần header của phản hồi
	+ Dòng 7-14 : Nội dung phản hồi'

## HTTP Methods

+ Các HTTP methods là cách để client thể hiện ý định của mình khi request đến server
+ GET Request : Sử dụng để lấy thông tin từ máy chủ web
+ POST Request : Dùng để gửi dữ liệu lên máy chủ và có thể tạo ra bản ghi mới
+ PUT Request : Gửi dữ liệu lên máy chủ để cập nhật thông tin đã có (khác với POST, PUT có thể ghi đè thông tin lên 1 bản ghi hiện có)
+ DELETE Request : Dùng để xóa thông tin/bản ghi khỏi máy chủ

![[Pasted image 20250217180024.png]]

## HTTP Status Codes

+ Dòng đầu tiên của phàn hồi từ máy chủ luôn chứa 1 status code cho biết kết quả của yêu cầu và cách xử lý tiếp theo
+ Có 5 nhóm chính
	+ 100-199 : Information Response : Chỉ ra rằng phần đầu của yêu cầu đã được chấp nhận, client nên tiếp tục gửi phần còn lại (ít phổ biến)
	+ 200-299 : Success : Cho biết yêu cầu của client đã được xử lý thành công
	+ 300-399 : Redirection : Chuyển hướng : Dùng để chuyển hướng client đến 1 resource khác
	+ 400-499 : Client Errors : Thông báo với Client rằng đã có lỗi trong yêu cầu của họ
	+ 500-599 : Server Errors : Xảy ra khi máy chủ gặp lỗi khi xử lý yêu cầu, thường là lỗi nghiêm trọng
+ Các mã phổ biến :
		![[Pasted image 20250217181903.png]]

## Headers

+ Headers là phần dữ liệu bổ sung được gửi kèm trong HTTP request hoặc HTTP response
+ Request Header phổ biến
	+ Host : Xác định website nào cần truy cập trên máy chủ(vì 1 máy chủ có thể có nhiều trang web)
	+ User-Agent : Cung cấp thông tin về trình duyệt và phiên bản hiện đang sử dụng của client, giúp server trả về 1 web hiển thị nội dung phù hợp
	+ Content-Length : Chỉ ra kích thước dữ liệu mà client sẽ gửi lên server
	+ Accept-Encoding : Cho máy chỉ biết biết trình duyệt hỗ trợ các phương thức nén dữ liệu nào để giảm dung lượng tải xuống
	+ Cookie : Gửi dữ liệu đã được lưu từ trước trong phiên trước đến máy chủ
+ Response Header phổ biến
	+ Set-Cookie : Server yêu cầu trình duyệt lưu cookie, thường dùng để ghi nhớ phiên làm việc của người dùng
	+ Cache-Control : Xác định thời gian lưu dữ liệu vào bộ nhớ cache để giảm số lần tải lại từ server
	+ Content-type : Chỉ ra loại nội dung được trả về cho client, giúp trình duyệt hiển thị đúng định dạng
	+ Content-Encoding : Cho biết dữ liệu phản hồi được nén bằng phương pháp nào
## Cookies

+ Cookies là 1 đoạn dữ liệu nhỏ được lưu trên máy tính của người dùng khi họ truy cập 1 trang web. Dữ liệu này sẽ được gửi đến server qua header HTTP `set-cookie`
+ Mỗi khi người dùng gửi 1 HTTP Request đến server, trình duyệt sẽ tự động gửi lại cookie trong đó giúp máy chủ bớt nhiệm vụ phải xử lý thông tin
+ => Vì HTTP là giao thức 'sateless'(không nhớ trạng thái) nên cookies giúp web server lưu trạng thái của người dùng
+ Các bước cookie hoạt động
	+ **Bước 1**: **Client gửi yêu cầu truy cập website** 
	+ **Bước 2**: **Server phản hồi với Set-Cookie**
	+ **Bước 3**: **Client gửi dữ liệu (POST request)**
	+ **Bước 4**: **Server phản hồi và đặt cookie**
	+ **Bước 5**: **Client gửi lại cookie trong yêu cầu tiếp theo**
	+ **Bước 6**: **Server nhận cookie và hiển thị thông tin phù hợp**

## How the websites works

+ JS thường được nhúng trong thẻ `<script>` hoặc được nhúng từ xa bằng attribute `<script src = "link file .js"></script>`
 + Load balancers (Bộ cân bằng tải) : giúp phân phối tải giữa nhiều máy chủ, giúp trang web chạy ổn định và tránh tình trạng quá tải, nếu server bị lỗi, nó cũng sẽ tự chuyển hướng lưu lượng sang các server khác còn hoạt động
	 + Khi người dùng gửi yêu cầu truy cập website, nó sẽ đi qua load balancers trước để nó chọn 1 server phù hợp phía sau để xử lý
	 + Nó có chức năng health check định kỳ cho các server, nếu 1 server nào đó bị lỗi, nó sẽ tạm dừng gửi yêu cầu đến server đó cho đến khi server được kích hoạt trở lại
 + CDN (Content Delivery Networks) : Giúp giảm tải cho các máy chủ bằng cách lưu trữ các file tĩnh(JS, CSS, hình ảnh, video,...). CDN có nhiều máy chủ trên toàn cầu, giúp người dùng truy cập nhanh hơn bằng cách gửi nội dung từ máy chủ gần họ nhất
+ Database : Lưu trữ và truy xuất dữ liệu của website, máy chủ có thể gửi query đến database hoặc lưu dữ liệu
+ WAF (Web Application Firewall) : Bảo vệ trang web khỏi các cuộc tấn công mạng, ngăn chặn các request độc hại gửi đến server
+ Web server : phần mềm phục vụ nội dung web(Apache, Nginx, IIS, NodeJS)
+ Virtual Host : Cho phép chạy nhiều website trên 1 server
+ Static vs Dynamic Content :
	+ Static : không đổi (hình ảnh, css, js,...)
	+ Dynamic : Thay đổi dựa trên dữ liệu back-end



## Wram-up

Ví dụ lần lượt các bước : 
+ Request tryhackme.com in your browser
+ Check Local Cache for IP Address
+ Check your recursive DNS Server for Address
+ Query root server to find authoritative DNS Server
+ Authoritative DNS Server advises the IP address for the website
+ Request passes through a Web Application Firewall
+ Request passes throught Load Balancer
+ Connect to Webserver on port 80 or 443
+ Web server receives the GET request
+ Web Application talks to Database
+ Your browser renders the HTML into a viewable website
