
# Giới thiệu về NoSQL

## MongoDB

Giống như các loại cơ sở dữ liệu khác như MySQL, MariaDB hay PostgreSQL nhưng MongoDB không sử dụng table để lưu dữ liệu mà thay vào đó là **documents** 

**Documents** giống như 1 bộ từ điển với các cặp key-value được lưu
Ví dụ , ta có 1 website quản lý các thông tin cơ bản của nhân viên. Ta có thể tạo 1 document để chứa dữ liệu của 1 nhân viên như sau
`{"_id":ObjectId("5f077332de2cdf808d26cd74"), "username" : "lphillips", "first_name" : "Logan", "last_name" : "Phillips", "age" : "65", "email" : "lphillips@example.com" }`


Nhóm nhiều document lại ta sẽ được một **colection**
![[Pasted image 20250705160133.png]]


Nhóm nhiều collection ta sẽ được **database**
![[Pasted image 20250705160221.png]]

## Truy vấn cơ sở dữ liệu




