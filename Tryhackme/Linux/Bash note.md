
+ Tài liệu : https://devhints.io/bash
+ Bắt buộc dòng đầu phải có `#!/bin/bash` để trình thông dịch hiểu 
+ File có đuôi .sh
+ Comment : `#`
+ Cấp quyền thực thi cho file `chmod +x <tên file>`
+ Chạy file : `./`
+ Variable : 
	+ `name="Jammy"` (Chú ý là không được cách ở chỗ dấu '=') 
	+ `echo $name`	
+ `bash -x ./<tên file>` : Debug (Chạy từng dòng)
+ `set -x #code muốn debug set +x` : Debug 1 đoạn nhất định
+ `+` nếu lệnh thực thi, `-` nếu lệnh bị lỗi

+ Parameter : `tên biến=$<stt>`
+ `read <tên biến>` đọc dữ liệu cho biến
+ `$#` : cung cấp số lượng parameter cần truyền vào file script
+ Truy cập parameter thứ i : `$i`
+ `$0` : tên file script, cũng là parameter đầu tiên
+ Mảng : 
	+ Khai báo : `<tên mảng>=('car' 'train' 'bus')`
	+ Truy cập giá trị của phần tử : `${tên mảng[chỉ số]}` 
	+ Xóa phần tử : `unset tên mảng[chỉ số]`
	+ Thay đổi phần tử : `tên mảng[chỉ số] = giá trị cần gán`
	+ In ra giá trị của phần tử : `"${tên mảng[chỉ số]}"` (chỉ số = @ nếu muốn in toàn bộ mảng)
+ Câu lệnh điều kiện : 
```shell
# Defining the Interpreter 
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
        echo "Welcome Stewart! Here is the secret: THM_Script"
else
        echo "Sorry! You are not authorized to access the secret."
fi
```

+ `-eq` : =
+ `-ne` : != 
+ `-gt` : >
+ `-lt` : <
+ `-ge` : >=

+ `-f <tên file>` : kiểm tra file có tồn tại hay không
+ `-w <tên file>` : kiểm tra có thể ghi được lên file hay không
+ `-r <tên file>` : kiểm tra có quyền đọc file không
+ `-d <tên file>` : kiểm tra file có phải là 1 directory hay không

+ Vòng lặp : 
	``` bash
	for i in {1..10};
	do
		echo $i
	done
```
