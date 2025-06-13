Subdomain enumeration là quá trình tìm kiếm tất cả các tên miền phụ của 1 trang web
Có 3 cách để thực hiện quét tên miền phụ :
+ Brute force
+ OSINT
+ Virtual Host

### OSINT

+ SSL/TLS Certificate : Mỗi khi có SSL/TLS certificate , sẽ có 1 trang tổng hợp các log để kiểm soát các tên miền con của trang web được cấp phép đó. Link https://crt.sh/ (dùng để kiểm tra log các lần sửa đổi tên miền của 1 trang web)
+ Sử dụng search engine (VD : `site:*.tryhackme.com -site:www.tryhackme.com`)
+ Sublist3r : 1 công cụ để quét các tên miền

### Brute force
Dùng tools để duyệt tất cả các tên miền khả dụng sử dụng word list

### Virtual host

+ `ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.126.76 -fs {size}` 
	+ -w : Sử dụng wordlist riêng
	+ -H : Thay đổi header
	+ -u : Tên miền máy chủ muốn duyệt
	+ `FUZZ` : vị trí mà muốn thay wordlist vào
	+ -fs : yêu cầu bỏ qua những kết quả có kích thước chỉ định