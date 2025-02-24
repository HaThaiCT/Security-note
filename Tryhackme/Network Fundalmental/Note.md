

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
+ - **Packet** giống như bức thư được viết và ghi địa chỉ người nhận (IP).
- **Frame** giống như phong bì được dán tem và gửi qua từng bưu cục (trạm trung gian - switch) để đến đích.
+ Frame : là 1 đơn vị dữ liệu tại tầng 2 (Data link layer), giúp truyền dữ liệu giữa các thiết bị trong cùng 1 mạng LAN bằng địa chỉ MAC
+ Packet  : là 1 đơn vị dữ liệu tại tầng 3 (Network Layer). Nó chứa địa chỉ IP của thiết bị gửi và nhận để định tuyến qua nhiều mạng khác nhau
	+ Header :
		+ Time to live : Đặt hạn cho packet
		+ Checksum : Kiểm tra tính toàn vẹn của dữ liệu
		+ Source Address : Địa chỉ gửi đi
		+ Destination Address : Địa chỉ đến
+ Encapsulation : Là quá trình đóng gói dữ liệu từ tầng trên xuống tầng dưới, mỗi tầng sẽ thêm thông tin điều khiển vào dữ liệu gốc


### TCP/IP

+ Gồm 4 layer : 
	+ Application : Giao tiếp với phần mềm, ứng dụng
	+ Transport : Chia nhỏ dữ liệu thành các gói tin, kiểm soát luồng dữ liệu
	+ Internet : Định tuyến gói tin đến đích
	+ Network Interface : Xử lý phần cứng (Ethernet, Wi-fi,...)
+ Sử dụng quy trình encapsulation(đóng gói), từng mảnh dữ liệu sẽ đi qua từng lớp và được đóng gói lại
+ Connection-based : TCP cần phải kết nối giữa client-server trước khi gửi dữ liệu
+ Advantages of TCP
	+ Đảm bảo tính toàn vẹn dữ liệu
	+ Đồng bộ hóa dữ liệu giữa 2 thiết bị, tránh thứ tự dữ liệu bị sai
	+ Thực hiện nhiều process có độ tin cậy
+ Disadvantages of TCP 
	+ Cần 1 kết nối ổn định
	+ Kết nối chậm có thể làm nghẽn tắc
	+ Chậm hơn UDP vì phải xử lý nhiều thông tin hơn
+ TCP packets gồm nhiều phần thông tin được gọi là headers
	+ Source Port : Được chọn ngãu nhiên từ 0-65535
	+ Destination Port : Không được chọn ngẫu nhiên
	+ Source IP : IP của thiết bị gửi
	+ Destination IP : IP thiết bị nhận
	+ Sequence Number : Phần dữ liệu được truyền đi đầu tiên sẽ được gán bằng 1 số ngẫu nhiên
	+ Acknowledgement Number
	+ Checksum : Kiểm tra xem kết quả tính toán dữ liệu có giống với kết quả trước khi gửi đi hay không
	+ Data : Header lưu dữ liệu
	+ Flag : Điều khiển cách xử lý packet

+ Three-way handshake : Quá trình kết nối giữa 2 thiết bị SYN->SYN/ACK->ACK
	+ SYN : message được gửi bởi client để đồng bộ và kết nối 2 thiết bị (VD : Client : tôi muốn kết nối, STT ban đầu của tôi là 0)
	+ SYN/ACK : Gửi bởi server để xác nhận nỗ lực đồng bộ từ client(VD : Client : Ok, số thứ tự của tao là 5000, xác nhận số thứ tự của mày là 0)
	+ ACK  : Xác nhận rằng 1 loạt message/packets được gửi thành công (Client : Tao xác nhận STT của mày là 5000, bây giờ tao sẽ gửi dữ liệu với số thứ tự là 1)
	+ DATA : dữ liệu chính được gửi thông qua DATA message
	+ FIN : Đóng kết nối 1 cách sạch sẽ
	+ RST : Đột ngột chấm dứt kết nối. Là giải pháp cuối cùng để xử lý lỗi trong quá trình truyền tin
	+ ![[Pasted image 20250216143519.png]]

+ Quá trình đóng kết nối
	+ Client gửi FIN -> yêu cầu đóng kết nối
	+ Server gửi ACK : xác nhận đã nhận được FIN
	+ Server gửi FIN : Server cũng yêu cầu đóng kết nối
	+ Client gửi ACK : Xác nhận đóng kết nối hoàn tất

### UDP/IP

+ Khác với TCP là không cần thiết lập kết nối liên tục giữa 2 thiết bị

|                   | TCP                                                 | UDP                                                 |
| ----------------- | --------------------------------------------------- | --------------------------------------------------- |
| **Kiểm soát lỗi** | Có kiểm tra lỗi và đảm bảo dữ liệu đến đúng thứ tự. | Không đảm bảo dữ liệu đến đúng thứ tự hoặc đến nơi. |

|            | TCP                                           | UDP                                      |
| ---------- | --------------------------------------------- | ---------------------------------------- |
| **Tốc độ** | Chậm hơn do phải kiểm tra và đảm bảo dữ liệu. | Nhanh hơn vì không có kiểm tra phức tạp. |

|              | TCP                                                                                                   | UDP                                                                              |
| ------------ | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Ứng dụng** | Dùng cho các ứng dụng yêu cầu tính toàn vẹn của dữ liệu như web (HTTP/HTTPS), email (SMTP/IMAP/POP3). | Dùng cho ứng dụng không yêu cầu độ tin cậy cao như video call, game online, DNS. |


+ Cấu trúc header : 
	+ Source Port
	+ Destination Port
	+ Source Address
	+ Destination Address
	+ Time to live
	+ Data
+ ![[Pasted image 20250216150732.png]

### Port

+ Điểm kết nối để dữ liệu được trao đổi theo 1 đường phù hợp
+ Được xác định bởi 1 số nguyên từ 0 đến 65535
+ 1 số port phổ biến
	+ 80 : HTTP
	+ 443: HTTPS
	+ 21: FTP
	+ 22: SSH
+ Có thể tự điều chỉnh cổng kết nối ko theo tiêu chuẩn

## Extending Network

### Port forwarding

+ Là 1 phương pháp quan trọng để giúp các ứng dụng/ dịch vụ trong mạng nội bộ có thể kết nối ra bên ngoài Internet
+ Ví dụ :
	![[Pasted image 20250216152906.png]]
	+ Router trong Network #1 được cấu hình trên router để chuyển tiếp lưu lượng từ cổng 80 của địa chỉ **82.62.51.70** (địa chỉ IP công khai của router) đến **192.168.1.10**.
	- Khi máy tính từ Network #2 gửi yêu cầu đến địa chỉ **82.62.51.70:80**, router sẽ chuyển tiếp yêu cầu đó đến **192.168.1.10:80** trong mạng nội bộ.
	- Điều này giúp máy tính từ Network #2 có thể truy cập trang web đang chạy trong Network #1.
### Firewalls 

+ Là thiết bị/ phần mềm có nhiệm vụ xác định luồng dữ liệu nào được phép vào/ra khỏi mạng
+ Hoạt động dựa trên các yếu tố : 
	+ Nguồn gốc của lưu lượng
	+ Điểm đến của lưu lượng
	+ Port của mạng sử dụng
	+ Giao thức(protocol) mạng sử dụng
+ Có 2 loại chính
	+ Stateful(có trạng thái)  : Phân tích toàn bộ kết nối thay vì riêng lẻ từng gói tin, có thể nhận biết trạng thái của kết nối để ra quyết định, cần nhiều tài nguyên hơn sateless, nếu phát hiện 1 kết nối xấu có thể chặn luôn cả thiết bị gửi
	+ Stateless(không trạng thái) : Chỉ dựa trên 1 tập quy tắc cố định để kiểm tra từng gói nguyên riêng lẻ, không lưu trạng thái kết nối, tốn ít tài nguyên hơn, hiệu quả khi phải xử lý lượng lớn dữ liệu

+ Chủ yếu hoạt động ở layer 3 và layer 4 trong mô hình OSI

### VPN

+ Virtual Private Network
+ Là công nghệ cho phép các thiết bị trên các mạng riêng biệt giao tiếp an toàn bằng cách tạo 1 đường hầm bảo mật(tunnel) trên Internet. Khi sử dụng VPN, các thiết bị có thể kết nối như thể chúng đang cùng 1 mạng nội bộ, dù có ở vị trí khác nhau
+ Ví dụ
		![[Pasted image 20250216160603.png]]
	+ **Network #1**: Văn phòng 1 (Office #1).
	- **Network #2**: Văn phòng 2 (Office #2).
	- **Network #3 (VPN)**: Các thiết bị từ Network #1 và Network #2 được kết nối với nhau thông qua VPN, tạo thành một mạng riêng an toàn mà **chỉ các thiết bị trong VPN mới có thể giao tiếp với nhau**.
+ Lợi ích của VPN :
	+ Kết nối các mạng ở xa nhau
	+ Bảo mật dữ liệu
	+ Ẩn danh & Bảo vệ quyền riêng tư
+ Các công nghệ VPN :
	+ PPP : Hỗ trợ xác thực và mã hóa dữ liệu
	+ PPTP : Giúp dữ liệu của PPP truyền lên mạng công cộng như Internet
	+ IPSec : Giao thức bảo mật dựa trên giao thức IP

### Thiết bị của mạng LAN

#### Router
+ Router : Là thiết bị có nhiệm vụ kết nối các mạng với nhau và truyền dữ liệu giữa chúng, được thực hiện qua quá trình routing
+ Routing là quá trình dữ liệu di chuyển giữa các mạng khác nhau, router sẽ tạo ra các đường dẫn giữa các mạng để dữ liệu có thể được truyền thành công.
+ Router thường có giao diện quản lý, cho phép quản trị viên thiết lập các quy tắc hoặc tường lửa

+ Lưu ý : Router là thiết bị chuyên dụng và không thực hiện chức năng của switch
#### Switch
+ Switch : Là thiết bị giúp kết nối nhiều thiết bị với nhau. Có thể kết nối từ 3 đến 63 thiết bị thông qua cáp Ethernet
+ Có thể hoạt động ở layer 2 hoặc layer 3
	+ Switch Layer 2 : Chỉ hoạt động ở tầng 2, chuyển tiếp dữ liệu thông qua địa chỉ MAC
	+ Switch Layer 3 : Sử dụng 1 số chức năng định tuyến giống router, giúp gửi dữ liệu giữa các mạng bằng giao thức IP
+ VLAN (Virtual Local Area Network) : Cho phép 1 mạng vật lý chia thành nhiều mạng logic khác nhau, mặc dù tất cả các thiết bị đều kết nối cùng 1 switch nhưng chúng có thể được phân tách để hoạt động độc lập, giúp tăng tính bảo mật


![[Pasted image 20250223014415.png]]![[Pasted image 20250223121414.png]]