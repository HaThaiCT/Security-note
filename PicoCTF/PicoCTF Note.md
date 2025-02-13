
# Primer

## The shell 

![[Pasted image 20250202232549.png]]
+ `Q0h313th` mean : username logged into the shell.
+ `pico-2019-shell1` mean : The shell is on the computer named `pico-2019-shell1`
+ `~` mean : /home/Q0h313th
+ `$` mean : Everything before it is the computer generated prompt and everything after is the user typed command



+ Sheet tra cứu : ![[CLI-cheatsheet-dark.pdf]]
+ Giải thích các lệnh : [explainshell.com - date](https://explainshell.com/explain?cmd=date)

## Forensic

### How to search for strings and filenames
+ file + file cần chọn : Hiển thị ra loại file của file đó 
+ wget + link : Tải tệp từ link về
+ grep : In ra các dòng có chứa mẫu cần tìm
+ grep -r <ký tự cần tìm> : tìm đệ quy trên tất cả file và folder con
+ unzip + file zip : Giải nén file zip
+ gunzip + file gz : Giải nén file gz
+ find : Tìm kiếm file trong linux ([How To Find a File In Linux From the Command Line - Plesk Tips](https://www.plesk.com/blog/various/find-files-in-linux-via-command-line/)) (find . -name <tên file> : tìm file có trong thư mục và các thư mục con của thư mục đang đứng)

### Disk analysis

+ mmls [tùy_chọn] thiết_bị_hoặc_file : Hiện bảng phân vùng của 1 ổ đĩa
+ nc + host + port : kết nối với máy có địa chỉ host qua cổng port(ít bảo mật hơn lệnh ssh)
+ Disk image : Là bản sao toàn bộ của thiết bị lưu trữ, chứa tất cả các dữ liệu đã bị xóa nhưng chưa bị ghi đè
	4 layers tool : media, block, inode, filename  được liệt kê từ thấp đến cao
+ media : `mm` (mmls) : Thông tin về cấu trúc phân vùng trên đĩa
+ block : Dữ liệu trên đĩa được lưu trên các khối có kích thước cố định. Một tập tin thường không nằm gọn trong một khối mà có thể phân tán nhiều khối khác nhau (`blkcat`  Đọc nội dung một khối dữ liệu cụ thể)
+ inode: Nơi lưu trữ siêu dữ liệu về tập tin, giống mục lục trong sách, chứa các thông tin như : Tệp tập tin, quyền truy cập, thời gian tạo/sửa, danh sách các khối dữ liệu mà tập tin sử dụng(`icat` Trích xuất tập tin dựa trên inode number)
+ filename : Danh sách các tập tin và thư mục(`fls` : liệt kê danh sách tập tin trên ảnh đĩa)

##### Packet(gói tin)

Là đơn vị cơ bản để truyền tải dữ liệu từ nguồn đến đích qua các thiết bị mạng.

1 packet thường được đóng gói bởi nhiều layers :
+ Header : Phần chứa các thông tin điều khiển cần thiết để định tuyến và xử lý gói tin. Header bao gồm :
	+ Địa chỉ nguồn và đích
	+ Thông tin định tuyến : địa chỉ IP, ....
	+ Các thông tin về giao thức
	+ Thông tin về kiểm tra lỗi 
+ Payload : Phần dữ liệu người gửi thực sự muốn gửi cho người nhận
+ Trailer(không phải lúc nào cũng có) : Các thông tin bổ sung như mã kiểm tra lỗi.
Network Layers : 
+ Application Layer
+ Transport Layer
+ Network Layer
+ Data link Layer
+ Physical Layer
`Đoạn này chưa hiểu lắm, cần học thêm về mạng`

## Programing in python

+ Chạy lệnh : `$ python3 <tên file>`
+ Cách chạy 1 dòng python ngay trên terminal : `python3 -c 'code'`
+ Biến : `<tên biến> = <giá trị>` 
+ Vòng lặp : `for i in range (n):`
+ List : `my_list = ["I", "love", "you"]` 
		`for i in my_list:`
		`my_ordered_list = my_list.sort()`
+ Functions : 
```python
def even_odd(x):
	if (x % 2 == 0):
		return True
	else:
		return False
my_number = int(input())

if even_odd(my_number):
	print("even")
else:
	print("odd")
```
+ Input and output
	Input : input()
	Output : print
	File
	```python
filepath_read = "pico.txt"
filepath_write = "outputpico.txt"
i = 1

with open(filepath_read, "r") as file_read:
    with open(filepath_write, "w") as file_write:
       for line in file_read:
            file_write.write(str(i) + "\n")
            file_write.write(line + "\n")
            i += 1

print("look inside your folder...")
```

+ Xử lý ngoại lệ 
``` python
num1 = 8

print("Input the number that will divide:")

try:
    num2 = int(input())
    result = num1 / num2
    print(result)
except ZeroDivisionError:
    print("Do not divide by zero, that is forbidden.")
except ValueError:
    print("Your input value must be an integer.")

print("The program keeps executing to do other stuff...")
```

+ Truyền đối số vào chương trình python
	```python
import sys # thư viện
# sys.argv là 1 danh sách các đối số khi truyền vào dòng lệnh
print('Number of arguments:', len(sys.argv), 'arguments.')
print('Argument List:', str(sys.argv))

# The number of iterations is taken from the second argument.
# (Remember that in an array [0] is the first one, [1] is the second one.)
# Bắt đầu từ đối số 1 vì đối số 0 chính là lệnh chạy chương trình
number_iterations = sys.argv[1]

f = open("output2.txt", "w")

for i in range(int(number_iterations)):
    if i < 5:
        f.write("The following number is less than 5\n")
    else:
        f.write("The following number is greater than or equal to 5\n")
    f.write(str(i)+"\n")

f.close()
print("look inside your folder...")
```
+ pwntools
+ Http requests in python : Sau khi xong web thì quay lại làm
### Web Exploits

##### HTML
##### Javascript
+ Thẻ script
```html
<html>
    <head>
        <title>This is a picoCTF JS Example</title>
        <script>
            function myFunctionSum(){
                var number1 = document.getElementById("number1").value;
                var number2 = document.getElementById("number2").value;
                var result = Number(number1) + Number(number2);
                alert(result);
            }
        </script>
    </head>
    <body>
        <h1>JavaScript example to add2 numbers</h1>
        Input the first number<br>
        <input type="text" id="number1"  ><br>
        Input the second number<br>
        <input type="text" id="number2" ><br>
        <!-- onclick = "myFunctionSum()" : khi ấn vào button thì chạy hàm -->
        <button onclick="myFunctionSum()"> Show alert! </button>
    </body>
</html>

```

##### Server code

###### PHP
+ 1 file php có thể chứa html, javascript, code php sẽ nằm trong thẻ <?php code ?>
+ PHP là 1 ngôn ngữ sử dụng server máy chủ để chạy. Ta sẽ gửi file code php tới máy chủ và máy chủ thực hiện chuyển chúng thành file script và chuyển về máy ta.
###### Cross Site Scripting (XSS)
+ Thay vì nhập dữ liệu bình thường để trang web ghi vào thì ta nhập 1 đoạn mã script để khai thác
+ Cookie : Là 1 tệp nhỏ được trình duyệt lưu trữ trên máy tính của người dùng giúp trang web nhớ thông tin người dùng.
+ Trong ví dụ , hacker đã nhúng 1 đoạn mã script để lấy đi cookie của người dùng
+ Lý do dẫn tới việc này là khi sử dụng php để echo dữ liệu từ database ra mà không sử dụng mã hóa, dẫn tới việc lệnh script vào không bị mã hóa và được thực hiện bởi server.

### Cryptography(đọc sau)

4 tính chất
 + Tính bảo mật(Confidentiality) : không ai ngoài ý muốn có thể đọc được nội dung
 + Tính toàn vẹn (Integrity) : Nếu thông điệp bị thay đổi, nó sẽ bị phát hiện
 + Tính xác thực (Autheentication) : Danh tính của 1 người luôn được xác minh
 + Tính không phủ nhận (Nonrepudiation) : Nếu 1 người gửi đi 1 thông điệp thì người đó phải thừa nhận rằng thông điệp đó là do họ gửi đi.


+ Cách để nén 1 directory thành file zip và có mật khẩu `zip --encrypt -r <tên file zip> <tên directory cần nén>`
Các loại mã hóa cổ đại : 
+ Substitution ciphers : Thay thế mỗi kí tự trong chuỗi thành 1 ký tự khác mà không làm xáo trộn thứ tự
+ Transpsition ciphers : Hoán đổi vị trí các ký tự trong bản mà không thay đổi bản thân các ký tự 

##### AES

+ ECB : "Electronic Code Book"
+ CBC : "Cipher Block Chaining"

### The network

Đoạn này hướng dẫn dùng Wireshark(đọc sau)


### Database

##### SQL 
+ Tạo bảng : create table <tên bảng> (các cột tham số)
+ Chèn thêm thông tin : insert into <tên bảng> (các cột tham số) values (các giá trị của các tham số theo đúng thứ tự)
+ Lọc dữ liệu : select ... from <tên bảng> where ...
##### SQL Injection
+ Khai thác cú pháp lệnh SQL để đánh cắp dữ liệu trong cơ sở dữ liệu. 
+ Sẽ tiêm 1 biểu thức or luôn luôn đúng để truy xuất ra tất cả dữ liệu

##### Blind SQL Injection

### Levels of Code

##### High-levels languages
+ Trừu tương nhất
+ Nim, Python, Perl
+ Dễ tránh được buffer overflows
##### Low-levels languages
+ Ít trừu tượng hơn high-leveks languages
+ C, Assembly, Rust
+ Dài dòng hơn, ít trừu tượng

##### Intermediate Representation

+ **Intermediate Representation (IR)** (biểu diễn trung gian) là một dạng biểu diễn dữ liệu được sử dụng trong quá trình biên dịch và xử lý mã nguồn của một chương trình trước khi tạo ra mã máy thực thi. Nó đóng vai trò trung gian giữa mã nguồn ban đầu và mã đích cuối cùng (mã máy hoặc mã bytecode).
+ Assembly
##### Machine Instructions
+ Cấp thấp nhất của code
+ Sẽ là thứ dùng để thông dịch hoặc biên dịch trực tiếp ra mã máy

### C language

+ Biên dịch : `gcc <tên file code> (-o <tên file binary muốn tạo)>`
+ Chạy file binary : `./<tên file>`

### Binary Exploitation

###### Stack overflow attack
+ Làm cho tràn bộ nhớ đệm
+ GDB : có thể sinh ra Assembly từ mã máy