

# Visual Studio

### Debugger

+ Khi gặp lời gọi hàm, debugger có 3 cách xử lý
	+ Step Into : Debugger sẽ đi vào trong hàm
	+ Step Over : Chạy toàn bộ hàm nhưng không đi vào bên trong, dừng lại ở dòng tiếp theo
	+ Step Out : Chạy nốt phần còn lại của hàm hiện tại và quay lại điểm gọi hàm trước đó
	+ Run to Cusor : Nhảy vào các lệnh bằng chuột
+ Call stack : Hiện stack các hàm từ trên xuống dưới và vị trí của hàm đó trong chương trình
+ Breakpoints : Hiển thị các breakpoint đã được đặt và có thể đặt breakpoint mới
+ Output : Hiển thị đầu ra của quá trình thực thi như tên và đường dẫn của tệp thực thi và các thư viện liên kết động(dll) đã được tải vào cùng không gian bộ nhớ với tệp thực thi.
+ Xem nội dung của memory khi đang debug : `Menu Bar -> Debug -> Windows -> Memory -> Memory 1`.