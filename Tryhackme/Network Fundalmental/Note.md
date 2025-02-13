

## Identifying Devices on a Network
##### IP Address
+ Cấu tạo bởi 4 octets, mỗi octet là 1 số có giá trị từ 0-255
+ Có thể chuyển từ thiết bị này sang thiết bị khác nhưng không xuất hiện đồng thời 2 lần trong cùng 1 mạng
+ Tương ứng với thiết bị năm ở private network hay public network, ta sẽ có public hoặc private IP address
+ Tuân theo giao thức(protocol)
+ Các thiết bị trong private truyền thông tin cho nhau bằng private IP nhưng để truyền thông tin ra Internet thì cần phải dùng public IP, public IP address sẽ được cung cấp bởi Internet **S**ervice **P**rovider(ISP)
+ IPv6 vs IPv4
##### Media Access Control (MAC) Address

+ Biểu diễn bởi 1 chuỗi 12 ký tự thập lục phân, cứ 2 ký tự tạo thành 1 nhóm và các nhóm ngăn cách nhau bởi dấu `:` (Ví dụ `a4:c3:f0:85:ac:2d`)
+ 6 ký tự đầu đại diện cho cơ sở sản xuất giao diện mạng, 6 ký tự sau là 1 số độc nhất trong cơ sở đó
+ Giống như dấu vân tay, mỗi thiết bị chỉ có 1 cái và không được thay đổi
+ Có thể bị giả mạo bằng cách spoofing.

### Ping

+ Sử dụng các packets ICMP(**I**nternet **C**ontrol **M**essage **P**rotocol) để xác định hiệu suất kết nối giữa các thiết bị
+ Cú pháp : `ping <địa chỉ IP/URL>`
+ Đo bằng cách sử dụng gói echo của ICMP và gói echo của ICMP nhận được từ máy đích

## Intro to LAN
### Local Area Network (LAN) Topologies

##### Star topology
![[Pasted image 20250212000134.png]]
+ Ưu : Dễ dàng mở rộng
+ Nhược : Tốn chi phí, dễ bị lỗi nếu máy tập trung bị lỗi
##### Bus Topology

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/27e9ff166d2d4ad5436e27c8c9b62e6d.png)  

+ Ưu : Chi phí thấp
+ Nhược : Dễ bị ách tắc, khó xác định lỗi ở thiết bị nào, không có dự phòng nếu lỗi
##### Ring Topology

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/4cea7a4b48eacbd4db0b0d5e32068596.png)

### What is a Switch?
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/2504bf9d718556c764c28843f43febe0.png)
+ Là thiết bị chuyên dụng để tập hợp các thiết bị khác nhau trong cùng 1 mạng sử dụng các cáp mạng dùng ethernet.
+ Theo dõi được thiết bị nào nối với cổng nào, khi nhận 1 gói tin sẽ gửi được thẳng đến đích
+ Mọi switches và routers có thể nối với nhau, khi 1 đường dẫn bị hỏng thì sẽ có đường dẫn khác dự phòng

### What is a Router

+ Router giúp kết nối các mạng và truyền dữ liệu giữa chúng
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/e83d39192c6a3e8168f842d9a680a7c3.png)

### Subneting

+ Subneting là thuật ngữ chỉ việc chia 1 mạng thành các mạng nhỏ hơn
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/dfdda87fb215cd723555bde32345e05e.png)  

+ Subnets sử dụng địa chỉ IP theo 3 cách : 
+ Network Address : Xác định điểm bắt đầu của mạng
+ Host Address : Là IP Address để xác định 1 thiết bị nằm trong subnet
+ Default Gateway : Là địa chỉ giao cho các thiết bị nằm trong mạng mà nó có gửi thông tin cho các mạng khác.
### ARP

+ Address Resolution Protocol 
+ Liên kết địa chỉ MAC và địa chỉ IP
+ Giao thức ARP dùng để tìm kiếm 1 thiết bị khác có trong mạng theo địa chỉ MAC
+ Cách hoạt động : Gửi request đến mạng để tìm thiết bị nào có địa chỉ IP tương ứng với yêu cầu và máy có địa chỉ IP đó sẽ respond lại địa chỉ MAC của nó. Sau đó nó sẽ được lưu vào bộ nhớ cache.

![[Pasted image 20250212103030.png]]

### DHCP

+ Cấp địa chỉ IP cho 1 thiết bị mới tham gia vào mạng
+ DHCP Discover : 
+ DHCP Offer : 
+ DHCP Request : 
+ DHCP ACK :

![[Pasted image 20250212103938.png]]

## OSI Model

### What is OSI Model

+ Là một mô hình chuẩn hóa giúp mô tả cách các hệ thống mạng giao tiếp với nhau. OSI chia quá trình truyền dữ liệu thành **7 tầng (layers)**, mỗi tầng có một nhiệm vụ riêng.
1. Physical
2. Data link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

![[Pasted image 20250212224225.png]]

⟶ **Tầng thấp (1-3):** Chuyển dữ liệu thô giữa các thiết bị.  
⟶ **Tầng trung (4):** Đảm bảo dữ liệu truyền tin cậy.  
⟶ **Tầng cao (5-7):** Giao tiếp với ứng dụng và người dùng.

#### 🔵 **1️⃣. Physical Layer (Tầng vật lý)**

- Chuyển đổi dữ liệu thành tín hiệu điện, quang, sóng radio.
- Quy định về cáp mạng, sóng Wi-Fi, tốc độ truyền, điện áp.

📌 **Ví dụ:**

- Cáp đồng (Ethernet), cáp quang (Fiber), Wi-Fi, Bluetooth.
- Thiết bị: **Hub, Repeater, Cáp mạng**.

---

#### 🟢 **2️⃣. Data Link Layer (Tầng liên kết dữ liệu)**

- Chia dữ liệu thành **frame (khung dữ liệu)**.
- Gán **địa chỉ MAC** để xác định thiết bị trong mạng LAN.
- Kiểm tra lỗi cơ bản (CRC - Cyclic Redundancy Check).

📌 **Ví dụ:**

- **Switch** hoạt động ở tầng này (dùng MAC Address để gửi dữ liệu).
- **Giao thức ARP** giúp tìm địa chỉ MAC của một địa chỉ IP.
- **Wi-Fi sử dụng giao thức CSMA/CA để tránh xung đột dữ liệu**.

---

#### 🟡 **3️⃣. Network Layer (Tầng mạng)**

- Định tuyến dữ liệu giữa nhiều mạng khác nhau.
- Gán **địa chỉ IP** cho từng thiết bị.
- Xử lý đường đi của gói tin qua các Router.

📌 **Ví dụ:**

- **Router hoạt động ở tầng này** (chọn đường đi tốt nhất cho gói tin).
- **IP Address (IPv4, IPv6)** giúp nhận dạng thiết bị trong mạng.
- **ICMP (ping, tracert)** kiểm tra kết nối mạng.

---

#### 🟠 **4️⃣. Transport Layer (Tầng vận chuyển)**

- Chia dữ liệu thành các **segment** (đoạn).
- Đảm bảo dữ liệu **truyền đúng thứ tự, không bị mất**.
- Dùng **cổng (port)** để phân biệt ứng dụng.

📌 **Ví dụ:**

- **TCP (Transmission Control Protocol):** Đảm bảo dữ liệu chính xác (dùng cho web, email).
- **UDP (User Datagram Protocol):** Truyền nhanh nhưng không đảm bảo (dùng cho video call, game online).
- **Port số 80 (HTTP), 443 (HTTPS), 22 (SSH), 53 (DNS), 25 (SMTP), v.v.**

---

#### 🔴 **5️⃣. Session Layer (Tầng phiên)**

- Thiết lập, duy trì và kết thúc kết nối giữa hai thiết bị.
- Kiểm soát thời gian kết nối (timeout).

📌 **Ví dụ:**

- **NetBIOS** giúp các máy tính Windows chia sẻ file.
- **API (Application Programming Interface)** giúp ứng dụng giao tiếp với hệ điều hành.
- **Các dịch vụ đăng nhập từ xa (SSH, Telnet, RDP).**

---

#### 🟣 **6️⃣. Presentation Layer (Tầng trình bày)**

- Chuyển đổi định dạng dữ liệu (mã hóa, giải mã, nén, giải nén).

📌 **Ví dụ:**

- **SSL/TLS (mã hóa dữ liệu HTTPS, bảo mật giao tiếp web).**
- **MP3, JPEG, PNG (chuyển đổi định dạng file).**
- **ASCII, Unicode (mã hóa ký tự trong văn bản).**

---

#### 🟤 **7️⃣. Application Layer (Tầng ứng dụng)**

- Cung cấp giao diện cho người dùng và phần mềm.
- Giao tiếp với ứng dụng như trình duyệt web, email.

📌 **Ví dụ:**

- **HTTP, HTTPS (truy cập web).**
- **SMTP, IMAP, POP3 (email).**
- **FTP (truyền file), SSH (điều khiển từ xa).**

## Packet & Frame

### Khái niệm 

+ Cả frame và packet đều là những mảnh nhỏ của dữ liệu.
+ Frame : là 1 đơn vị dữ liệu tại tầng 2 (Data link layer), giúp truyền dữ liệu giữa các thiết bị trong cùng 1 mạng LAN bằng địa chỉ MAC
+ Packet  : là 1 đơn vị dữ liệu tại tầng 3 (Network Layer). Nó chứa địa chỉ IP của thiết bị gửi và nhận để định tuyến qua nhiều mạng khác nhau
+ Encapsulation : Là quá trình đóng gói dữ liệu từ tầng trên xuống tầng dưới, mỗi tầng sẽ thêm thông tin điều khiển vào dữ liệu gốc