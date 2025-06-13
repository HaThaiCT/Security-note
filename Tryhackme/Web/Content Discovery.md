Có 3 cách để khám phá nội dung trên 1 trang web
+ Manually (Thủ công)
+ Automated (Tự động)
+ OSINT(Open-Source Intelligence)

### Manual Discovery

+ robot.txt : Chứa danh sách các tệp mà hạn chế các search engine không được phép tìm ra
+ Favicon database:  [OWASP favicon database - OWASP](https://wiki.owasp.org/index.php/OWASP_favicon_database) Tổng hợp những mã hash của favicon
+ Sitemap.xml : Chứa danh sách mọi đường dẫn mà gợi ý cho search engine tìm ra
+ `curl + address + -v` : Gửi request và in cụ thể ra request và response
+ `HTTP Header` : Chứa  thông tin của đối tượng, rất hữu ích để recon
+ Khi có thông tin của framework trang web sử dụng, tiến hành điều tra vào framework đó

### OSINT

#### Google Hacking/ Dorking
[Google hacking - Wikipedia](https://en.wikipedia.org/wiki/Google_hacking)

Sử dụng công cụ search của google để tra cứu những thuộc tính có thể có trong trang web 

Ví dụ :

|            |                    |                                                              |
| ---------- | ------------------ | ------------------------------------------------------------ |
| **Filter** | **Example**        | **Description**                                              |
| site       | site:tryhackme.com | returns results only from the specified website address      |
| inurl      | inurl:admin        | returns results that have the specified word in the URL      |
| filetype   | filetype:pdf       | returns results which are a particular file extension        |
| intitle    | intitle:admin      | returns results that contain the specified word in the title |
|            |                    |                                                              |


#### Wappalyzer
https://www.wappalyzer.com/
Là 1 công cụ online giúp xác định những công nghệ mà trang web đang sử dụng

#### Wayback machine
[https://archive.org/web/](https://archive.org/web/)
+ Hiển thị các bản ghi của trang web đó ở quá khứ qua từng lần chỉnh sửa

#### S3 Bucket
+ Là kho lưu trữ dữ liệu bên trong dịch vụ đám mây của AWS (có thể lưu trang web tĩnh)
+ Thường format của S3 buckets là  http(s)://**{name}.**[**s3.amazonaws.com**](http://s3.amazonaws.com/) với name là do người sở hữu đặt
+ Có thể đoán tên miền S3 bucket như sử dụng tên của công ty cộng với 1 số terms phổ biến như **{name}**-assets, **{name}**-www, **{name}**-public, **{name}**-private, etc

#### Github
+ Là 1 nguồn để tìm hiểu về trang web muốn tấn công nếu nó public code trên git


### Automated Discovery

+ Word list: có thể dùng list các từ khóa phổ biến để quét qua 1 trang web
+ https://github.com/danielmiessler/SecLists : Word list tool
+ Các công cụ phổ biến : ffuf, dirb, gobuster