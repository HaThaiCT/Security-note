
# 26/2/2025
+ Các thanh ghi trong x86_64
	+ `rax` : 64 bit
	+ `eax` : 32 bit, phần thấp của rax
	+ `ax` : 16 bit, thấp hơn nữa
	+ `ah,al` :  mỗi cái 8-bit, đại diện cho phần cao/thấp của `ax`
	+ Khi ghi vào 1 thanh ghi lớn, có thể sẽ làm `zero extend` hoặc thay đổi phần còn lại của thanh ghi lớn
	![[Pasted image 20250227010526.png]]
+ Biểu diễn số âm :
	+ Cách tối ưu là dùng bù hai (two's complement) : lật ngược các bit , sau đó +1
	+ Sử dụng 1 bit dấu , khi đó số âm có bit đầu bằng 1 và có giá trị bằng $2^n$ - giá trị dương.
+ `mov` : set giá trị từ 1 thanh ghi cho 1 thanh ghi khác
+ Khi `mov` từ register nhỏ -> lớn cần mở rộng dấu bằng `movsx hoặc movsxd` ví dụ có `eax = 0xfffffff`  thì `movsx rax, eax` biến rax thành `0xffffffffffffffff` thay vì `0x00000000ffffffff` (sẽ copy bit dấu của thanh ghi nhỏ đè lên tất cả phần còn lại của thanh lớn) 
+ `.intel_syntax noprefix` : báo cho assembler biết ta dùng Intel Syntax
+ `syscal` là cách chương trình tương tác với hệ điều hành, mỗi syscal sẽ được gán với 1 số. 
![[Pasted image 20250227012153.png]]
+ `rax` thường chứa mã `syscal` 
+ `rdi` chứa tham số thứ nhất
+ `rsi` chứa tham số thứ hai
![[Pasted image 20250227011914.png]]


+ Các bước chạy chương trình assembly : 
	+ Dịch sang object file `as -o <tên file>.o <tên file>.s`
	+ Link các phần file object với nhau `ld -o <tên file> <danh sách các file.o>`
	+ Chạy file 
+ `_start:` : đánh dấu bắt đầu của chương trình
+ `.global _start` : đánh dấu file bắt đầu của cả 1 tập



# 27/2/2025

+ `strace + <chương trình>` : chức năng của Linux, kiểm tra và ghi lại từng lệnh gọi hệ thống mà chương trình thực hiện cùng với kết quả trả về của chúng
+ `gdb + file_path` : khởi chạy GDB 
+ `starti` : lệnh trong GDB để chạy từ đầu chương trình


# 28/2/2025

+ `[address]` : dùng để lấy dữ liệu của 1 địa chỉ

# 4/3

+ `1` : system call cho write file
+ `0` : system call cho read file
+ 