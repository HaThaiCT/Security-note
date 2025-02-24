
# Little Endian vs Big Endian

Là 2 cách sắp xếp thứ tự byte trong bộ nhớ khi lưu trữ nhiều byte.

+ Little Endian : byte có trọng số thấp nhất sẽ lưu tại địa chỉ bộ nhớ thấp nhất (VD : số nguyên 4 byte 0x12345678 -> Little Endian theo thứ tự địa chỉ từ thấp -> cao sẽ là 0x78 0x56 0x34 0x12)
+ Big Endian : byte có trọng số cao nhất sẽ lưu tại địa chỉ bộ nhớ thấp nhất (VD : số nguyên 4 byte 0x12345678 -> Big Endian theo thứ tự địa chỉ từ thấp -> cao sẽ là 0x12 0x34 0x56 0x78)