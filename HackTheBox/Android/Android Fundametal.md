
# Introdution
Android là một hệ điều hành di động được xây dựng dựa trên phiên bản sửa đổi của Linux Kernel, được thiết kế chủ yếu cho các thiết bị màn hình cảm ứng như điện thoại và máy tính bảng. Hệ điều hành này được phát triển bởi một tập đoàn các nhà phát triển được gọi là Open Handset Alliance và được Google tài trợ về mặt thương mại.

**Kiến trúc** : Phần lớn thiết bị Android sử dụng kiến trúc ARM. Các bản Android sau này có bổ sung thêm kiến trúc x86 và x86-64 khi có bộ xử lý Intel
## Android OS

Sử dụng base của Linux Kernel, nên shell sẽ có lệnh tương tự giống các lệnh linux thông thường

Nền tảng phần mềm của Android gồm 6 phần như hình bên dưới:
![[Pasted image 20250708075457.png]]

### Linux Kernel
Chịu trách nhiệm quản lý 1 số thiết bị phần cứng như màn hình, máy ảnh, bluetooth, usb, wifi,...
Android cũng kế thừa 1 số chức năng bảo mật của Linux Kernel như cấu trúc phân quyền

### Hardware Abstraction Layer (HAL)

**HAL** là một lớp phần mềm cho phép cung cấp giao diện chuẩn để tương tác giữa hệ điều hành và các thiết bị phần cứng như camera, bluetooth, cảm biến và các thiết bị đầu vào. Nó đóng vai trò là cầu nối giữa phần cứng và các lớp phần mềm cấp cao hơn, đảm bảo tính nhất quán trong cách các phần mềm truy cập các chức năng phần cứng.

HAL giải quyết vấn đề viết phần mềm để hoạt động trên nhiều thiết bị khác nhau bằng cách chia sẻ các thư viện được Android framwork tải động trong lúc runtime.

### Android Runtime (ART)

**Android Runtime** là môi trường runtime mà hệ điều hành Android sử dụng để biên dịch và thực thi các ứng dụng. ART có khả năng chạy nhiều máy ảo đồng thời. Một số lợi ích của ART bao gồm:
+ Cải thiện garbage collection
+ Quản lý bộ nhớ tốt
+ Hỗ trợ debugging
+ Tối ưu hóa việc nén tệp
ART được thực thi các file `dex`
### Native C/C++ Libraries

+ Các developer thường dùng các thư viện này để viết mã cấp thấp để tương tác trực tiếp với phần cứng hoặc dùng để tối ưu hiệu suất
+ Các thành phần như HAL hay ART được viết bằng **native code**.

### Java API Framework

Cung cấp các công cụ và giao diện để xây dựng các ứng dụng Android. Java API Framework bao gồm các thành phần:
- **View System**
- **Resource Manager**
- **Notification Manager**
- **Activity Manager**
- **Content Providers**
- **Location Manager**
- **Package Manager**

### System apps

Bao gồm các ứng dụng mặc định đi kèm với hệ điều hành như Danh bạ, Máy ảnh, Trình duyệt, Lịch,...


### Davilk VM
Là bản runtime đời đầu được phát triển trước khi ART ra đời
Các ứng dụng Android được viết bằng Java hoặc Kotlin được biên dịch thành Java bytecode và sau đó được chuyển đổi thành **Dalvik bytecode**, đóng gói trong các định dạng tệp **.dex (Dalvik Executable)** hoặc **.odex (Optimized Dalvik Executable)**. Không giống như **Java Virtual Machine (JVM)** vốn dựa trên ngăn xếp (**stack-based**), **Dalvik VM** là một máy ảo dựa trên thanh ghi (**register-based**). Sự khác biệt về kiến trúc này cho phép thực thi hiệu quả hơn trên các thiết bị có tài nguyên **CPU** và bộ nhớ hạn chế, điều này lý tưởng cho môi trường di động.


### Rooting
Android phân tách bộ nhớ flash thành hai phân vùng chính sau đây.
- **/system/** : Dành cho hệ điều hành, chỉ có root mới có full quyền
- **/data/** : Dành cho người dùng bình thường

### Important Directories

| Thư mục                             | Mô tả                                                                                                                                    |     |     |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | --- | --- |
| **/data/data**                      | Chứa tất cả các ứng dụng do người dùng cài đặt.                                                                                          |     |     |
| **/data/user/0**                    | Chứa dữ liệu mà chỉ ứng dụng đó mới có thể truy cập.                                                                                     |     |     |
| **/data/app**                       | Chứa các tệp **APK** của các ứng dụng do người dùng cài đặt.                                                                             |     |     |
| **/system/app**                     | Chứa các ứng dụng được cài đặt sẵn của thiết bị.                                                                                         |     |     |
| **/system/bin**                     | Chứa các tệp nhị phân (**binary files**).                                                                                                |     |     |
| **/data/local/tmp**                 | Một thư mục có thể ghi bởi mọi người dùng (**world-writable**).                                                                          |     |     |
| **/data/system**                    | Chứa các tệp cấu hình hệ thống.                                                                                                          |     |     |
| **/etc/apns-conf.xml**              | Chứa cấu hình mặc định của **Access Point Name (APN)**. APN được sử dụng để thiết bị kết nối với mạng của nhà cung cấp dịch vụ hiện tại. |     |     |
| **/data/misc/wifi**                 | Chứa các tệp cấu hình **WiFi**.                                                                                                          |     |     |
| **/data/misc/user/0/cacerts-added** | Kho chứng chỉ người dùng. Chứa các chứng chỉ do người dùng thêm vào.                                                                     |     |     |
| **/etc/security/cacerts/**          | Kho chứng chỉ hệ thống. Người dùng không phải **root** không được cấp quyền.                                                             |     |     |
| **/sdcard**                         | Chứa một liên kết tượng trưng (**symbolic link**) đến các thư mục **DCIM**, **Downloads**, **Music**, **Pictures**, v.v.                 |     |     |
|                                     |                                                                                                                                          |     |     |

# Android App & OS Security
## Security features

Các ứng dụng Android thường được phát triển bởi 2 ngôn ngữ là Java và Kotlin. Android sử dụng công cụ **Android SDK** để biên dịch mã nguồn ứng dụng cùng với các tệp tài nguyên assets tạo thành một Android Package (APK) và lưu dưới dạng file với đuôi `.apk` . Package này chứa toàn bộ các thành phần cần thiết để cài đặt và chạy một ứng dụng Android, bao gồm bytecode(.dex) đã biên dịch, siêu dữ liệu manifest, tài nguyên và các thư viện native.

Mỗi ứng dụng Android sẽ chạy trong một **sandbox** bảo mật riêng của nó. Mô hình **sandboxing** hỗ trợ 1 số tính năng bảo mật như:
+ Vì Android là một hệ thống Linux đa người dùng => Mỗi ứng dụng được coi như là một người dùng riêng biệt
+ Theo mặc định, hệ thống sẽ gán cho mỗi ứng dụng một **Linux user ID (UID)** duy nhất, giúp hệ thống kiểm soát truy cập
+ Quyền truy cập hệ thống tệp đảm bảo chỉ ứng dụng được gán một UID cụ thể mới có thể truy cập các tệp của chính nó
+ Mỗi ứng dụng sẽ chạy trong một process riêng, một phiên bản riêng của máy ảo **Android Runtime(ART) virtual machine**, đảm bảo cô lập bộ nhớ.
+ Hệ thống khởi chạy process của ứng dụng khi cần và chấm dứt khi không cần thiết.
+ Các ứng dụng chỉ nhận được các quyền cần thiết để thể hiện chức năng cốt lõi của chúng. Các quyền bổ sung phải khai báo rõ ràng và phải được người dùng chấp thuận.

### Application Sandbox

Mỗi ứng dụng sẽ có UID riêng và sẽ được chạy trong process riêng. Các ứng dụng không thể tương tác với nhau hoặc truy cập tài nguyên hệ thống ngoài các đặc quyền của chúng trừ khi được cấp quyền rõ ràng. Tất cả các biện pháp bảo vệ này được áp dụng cho tất cả các mã chạy bên trong kernel, bao gồm các tệp nhị phân native, dịch vụ hệ điều hành, thư viện hay ứng dụng người dùng. Việc thoát khỏi sandbox đòi hỏi phải xâm phạm quyền ở kernel, thường trong các lỗi leo thang đặc quyền.

![[Pasted image 20250708112738.png]]
![[Pasted image 20250708113012.png]]
+ Cột đầu tiên là phân quyền và loại file (d là directory)
+ Cột thứ hai là số lượng `hard links` đến thư mục (Các thư mục con và `.` hoặc `..`) 
+ Cột thứ 3 là UID của chủ sở hữu (ứng dụng) sử dụng UID này
+ Cột thứ 4 là UID của nhóm sở hữu
+ Cột thứ 5 là kích thước file/thư mục
+ Cột thứ 6,7 là thời gian sửa đổi lần cuối
+ Cột thứ 8 là tên package của ứng dụng tương ứng

**Các biện pháp bảo vệ bổ sung**
- **SELinux Mandatory Access Control (MAC):** Tách biệt hệ thống khỏi các ứng dụng.
- **SELinux sandbox extension:** Cô lập các ứng dụng giữa những người dùng vật lý khác nhau.
- Bộ lọc **seccomp-bpf:** Đặt ra giới hạn cho các **syscalls** (lời gọi hệ thống) mà ứng dụng được phép sử dụng.
- **Individual SELinux sandboxes** và **Mandatory Access Control (MAC):** Tồn tại cho tất cả các ứng dụng không có đặc quyền với `targetSdkVersion >= 28`.
- Giới hạn chế độ xem thô của hệ thống tệp: Không có quyền truy cập trực tiếp vào các đường dẫn như `/sdcard/DCIM`.

### Chu kỳ của một ứng dụng

Để tải hoặc upload 1 ứng dụng lên GooglePlay Store, tệp APK của ứng dụng đó phải được ký (sign). Việc này nhằm tránh cho ứng dụng bị nhiễm các mã độc gây hại. Hiện tại chữ ký mới nhất là bản v4, nó được được lưu trữ trong một tệp riêng và yêu cầu phải có chữ ký **v2** hoặc **v3** tương ứng.
![[Pasted image 20250708114428.png]]

Chữ ký v2 và v3 sẽ vô hiệu hóa tệp apk nếu nó bị sửa đổi, do đó sẽ ngăn chặn các cuộc tấn công như chèn tệp `DEX` vào tệp `APK`.
Tuy nhiên, chữ ký v1 lại dễ bị tấn công theo kiểu này.Lỗ hổng **Janus (CVE-2017-13156)** cho phép kẻ xấu chèn tệp **DEX** vào **APK** mà không ảnh hưởng đến chữ ký trong trường hợp **APK** được ký bằng **Signature Scheme v1**.

**Các cách ký ứng dụng**
+ Android Studio, thông qua build `Generate Signed App Bundle/ APK`
+ Các công cụ như `jarsigner/apksigner`
+ GooglePlay App Signing
Các certificate dùng để ký cho 1 ứng dụng được gọi là `self-signed`.
Ví dụ ta có thể ký cho 1 file APK bằng công cụ `apksigner` như sau :
```shell
0xlc13n@htb[/htb]
$echo -e "password\npassword\njohn doe\ntest\ntest\ntest\ntest\ntest\nyes"
> params.txt
0xlc13n@htb[/htb]$ cat params.txt | keytool -genkey -keystore key.keystore -validity 1000 -keyalg RSA -alias john
0xlc13n@htb[/htb]$ zipalign -p -f -v 4 myapp.apk myapp_signed.apk
0xlc13n@htb[/htb]$ echo password | apksigner sign --ks key.keystore myapp_signed.apk
```

Các bước ký:
	+ Tạo 1 tệp `params.txt` với dữ liệu đầu vào cần thiết để keytool có thể gen ra 1 cặp khóa
	+ Truyền nội dung của `params.txt` vào keytool để tạo khóa và lưu vào `key.keystore`
	+ `zipalign` giúp cho các tệp không được nén trong `myapp.apk` được truy cập trực tiếp thông qua `mmap`, tạp ra một ứng dụng được tối ưu hóa là `myapp_signed.apk`.
	+ Cuối cùng, ứng dụng được ký bằng `apksigner` bằng cách truyền mật khẩu và sử dụng khóa đã được lưu trong `key.keystore`.

### Verified Boot

**Verified Boot** là một tính năng bảo mật của Android nhằm đảm bảo tính toàn vẹn của hệ điều hành. Điều này đạt được bằng cách sử dụng một bộ khóa mật mã độc nhất để ký và xác minh **boot image** (ảnh khởi động) và đảm bảo rằng chỉ các bên được ủy quyền mới có thể sửa đổi hệ thống. Trong khi Android đang khởi động, mỗi giai đoạn sẽ xác minh tính toàn vẹn và tính xác thực của giai đoạn tiếp theo, và nếu chữ ký hợp lệ, thiết bị sẽ khởi động bình thường. Nếu không, thiết bị sẽ không khởi động, hoặc sẽ cung cấp cho người dùng một thông báo cập nhật rằng thiết bị đã bị can thiệp.

Ngoài ra, **Verified Boot** còn sử dụng **Rollback Protection** (Bảo vệ chống hạ cấp) để ngăn chặn các lỗ hổng khai thác trở nên dai dẳng. Điều này được thực hiện bằng cách đảm bảo rằng Android chỉ cập nhật lên các phiên bản mới nhất. Luồng khởi động (**boot flow**) được đề xuất cho một thiết bị như sau:

![[Pasted image 20250708122207.png]]

## APK Structure

Một tệp APK lưu trữ mọi thành phần cần thiết để một ứng dụng Android hoạt động.
Khi một ứng dụng được biên dịch, mã nguồn Java hoặc Kotlin sẽ chuyển thành **Java bytecode** sau đó sẽ được chuyển đổi và tối ưu hóa thành một tệp `DEX`. Tệp `DEX` này sẽ được thực thi bằng DVM (Dalvik Virtual Machine) hoặc ART (Android Runtime) tùy thuộc vào phiên bản Android.

Ngoài mã biên dịch, tập tin apk còn chứa các tài nguyên khác như : assets, hình ảnh, UI layout và tệp **AndroidManifest.xml**.
Dưới đây là danh sách các phần của 1 tệp apk:
```
0xlc13n@htb[/htb]$ unzip myapp.apk
0xlc13n@htb[/htb]$ ls -l
total 27584
-rw-r--r--    1 bertolis  bertolis     4220 Jan  1  1981 AndroidManifest.xml
drwxr-xr-x   49 bertolis  bertolis     1568 May 10 13:36 META-INF
drwxr-xr-x    3 bertolis  bertolis       96 May 10 13:36 assets
-rw-r--r--    1 bertolis  bertolis  8285624 Jan  1  1981 classes.dex
drwxr-xr-x    9 bertolis  bertolis      288 May 10 13:36 kotlin
drwxr-xr-x    6 bertolis  bertolis      192 May 10 13:36 lib
drwxr-xr-x  545 bertolis  bertolis    17440 May 10 13:36 res
-rw-r--r--    1 bertolis  bertolis   922940 Jan  1  1981 resources.arsc
```

Các tệp và mã nguồn được giải nén từ apk đều được mã hóa và con người không thể đọc được
``` 
0xlc13n@htb[/htb]$ vim AndroidManifest.xml
```

![[Pasted image 20250708164733.png]]
Dưới đây là cấu trúc giải nén của một file apk
![[Pasted image 20250708164809.png]]

### META-INF

Thư mục này được tạo ra khi ứng dụng đã được ký và nó chứa thông tin xác minh cho ứng dụng. Bất kỳ hành động sửa đổi nào tệp APK đều sẽ bị vô hiệu hóa nếu không được ký lại. Bên trong thư mục này sẽ có các tệp sau:
```
0xlc13n@htb[/htb]$ ls -l META-INF/
total 664
-rw-r--r--  1 bertolis  bertolis   1103 Jan  1  1981 CERT.RSA
-rw-r--r--  1 bertolis  bertolis  77917 Jan  1  1981 CERT.SF
-rw-r--r--  1 bertolis  bertolis  77843 Jan  1  1981 MANIFEST.MF
<SNIP>
```
+ `CERT.RSA` : Chứa public key và chữ ký của `CERT.SF`
+ `CERT.SF` : Chứa 1 danh sách tên / hàm băm của các dòng tương ứng trong tệp `MANIFEST.MF`
+ `MANIFEST.MF` : Chứa 1 danh sách tên / hàm băm (thường là SHA256 hoặc Base64) cho tất cả các tệp của APK, và sử dụng để vô hiệu hóa APK nếu bất kỳ tệp nào bị sửa đổi

### assets
Thư mục này chứa các dữ liệu như hình ảnh, video, tài liệu, cơ sở dữ liệu,... và có thể được truy xuất bởi `AssetsManager`.

### lib
Chứa các thư viện native với mã đã được biên dịch để dành cho các thiết bị khác nhau. Các ứng dụng Android sử dụng **Native Development Kit (NDK)** có thể bao gồm các thành phần được viết bằng C hoặc C++. Khi một ứng dụng bao gồm các thư viện native, chúng được lưu trữ trong thư mục `lib` dưới dạng các tệp đối tượng chia sẻ (shared object files) với phần mở rộng là `.so`. Các tệp SO riêng biệt được tạo ra cho mỗi kiến trúc được hỗ trợ, thường được tổ chức dưới các thư mục con theo cấu trúc này.

```shell
0xlc13n@htb[/htb]$ ls -l lib/
total 0
drwxr-xr-x  3 bertolis  bertolis  96 May 10 13:36 arm64-v8a
drwxr-xr-x  3 bertolis  bertolis  96 May 10 13:36 armeabi-v7a
drwxr-xr-x  3 bertolis  bertolis  96 May 10 13:36 x86
drwxr-xr-x  3 bertolis  bertolis  96 May 10 13:36 x86_64
```

### res
Là thư mục chứa các resource của trang web mà không thể bị thay đổi khi đang chạy runtime, không giống như assets. Nó thường bao gồm các tệp XML định nghĩa trạng thái màu sắc, UI layouts, phông chữ, các giá trị, cấu hình cho các phiên bản hệ điều hành,...
```
0xlc13n@htb[/htb]$ ls -l res/
<SNIP>
drwxr-xr-x 1 bertolis bertolis 10762 Jan 27 16:05 color
drwxr-xr-x 1 bertolis bertolis  6624 Jan 27 16:05 drawable
drwxr-xr-× 1 bertolis bertolis    30 Jan 27 16:05 raw
drwxr-xr-× 1 bertolis bertolis   466 Jan 27 16:05 xml
```

Sự khác biệt giữa `res/` và `assets` :

| Tiêu chí                             | `res/` (resources)                                                   | `assets/`                                                        |
| ------------------------------------ | -------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Chức năng chính**                  | Chứa tài nguyên được **xử lý và định danh (indexed)** bởi Android.   | Chứa dữ liệu **nguyên bản, không xử lý** bởi Android.            |
| **Truy cập trong code**              | Thông qua **R class**, ví dụ: `R.drawable.logo` hoặc `R.raw.audio1`  | Thông qua `AssetManager`, ví dụ: `getAssets().open("data.json")` |
| **Biên dịch**                        | Android **biên dịch và chuyển mã XML → nhị phân**, tổ chức lại file. | Dữ liệu **không thay đổi**, được đóng gói nguyên gốc vào APK.    |
| **Tổ chức thư mục**                  | Phân loại nghiêm ngặt: `drawable/`, `layout/`, `values/`,...         | Linh hoạt, bạn tạo bất kỳ cấu trúc thư mục nào.                  |
| **Hỗ trợ đa ngôn ngữ, độ phân giải** | Có (ví dụ: `values-en/`, `drawable-hdpi/`...)                        | Không, bạn phải tự xử lý điều này trong code.                    |
| **Dùng cho**                         | Giao diện, hình ảnh, string, màu sắc, layout, styles,...             | File nhạc, JSON, text, font đặc biệt, file nhị phân, scripts,... |
| **Kích thước file**                  | Có thể bị nén hoặc chuyển dạng khác bởi trình biên dịch              | Giữ nguyên kích thước và định dạng file                          |
| **Truy cập thời gian chạy**          | Nhanh hơn (đã biên dịch sẵn, truy cập theo ID)                       | Chậm hơn một chút vì truy xuất file theo đường dẫn               |

### AndroidManifest.xml

Tệp này chứa các metadata về ứng dụng. Nó định nghĩa các thuộc tính và thành phần thiết yếu mà hệ thống sử dụng để quản lý ứng dụng, bao gồm:
+ Package name
+ SDK Version
+ Build Version
+ Permissions
+ NetworkSecurityConfig
+ Activities
+ Providers
+ Services

### classes.dex
Tệp này chứa tất cả các Java (hoặc Kotlin) class đã được biên dịch ở đinh dạng `DEX` và được thực thi bởi ART hoặc Dalvik VM. Các ứng dụng lớn có thể có nhiều tệp DEX được đặt tên giống như là `classes2.dex , classes3.dex , v.v.`

### resource.arsc
Tệp này chứa các tài nguyên đã được biên dịch trước mà ứng dụng sử dụng vào lúc **runtime**. Nó ánh xạ các định danh tài nguyên trong mã (ví dụ: `R.string.app_name`) đến các giá trị thực tế của chúng, chẳng hạn như chuỗi, màu sắc, bố cục, và kiểu dáng. Nó cũng bao gồm một biểu diễn nhị phân của các tài nguyên **XML**. Trong một số **APK**, bạn cũng có thể tìm thấy thư mục `kotlin/`, tồn tại trong các ứng dụng được viết bằng Kotlin và chứa siêu dữ liệu dành riêng cho Kotlin được sử dụng bởi **runtime** và các công cụ.
File `resources.arsc` chứa:

- Tất cả **chuỗi ký tự (strings)** trong `res/values/strings.xml`
- **Tên và ID** của mọi tài nguyên trong `res/` (ví dụ: layout, drawable, color…)
- Các **bản dịch ngôn ngữ** (localizations) nếu có (`values-en/`, `values-vi/`,...)
- Thông tin về các **theme**, **style**, **dimension**, v.v.
Nói cách khác, file này là nơi **liên kết giữa tên tài nguyên (res name)** và **ID nhị phân (R.java)** mà bạn sử dụng trong code.

# Android Apps & Development

## Android Studio
Cái này tự cài
### Cấu trúc dự án

| Thư mục | Tệp      | Mô tả                                                                                                                                                                                              |
| ------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app     | manifest | Chứa siêu dữ liệu cần thiết về ứng dụng, bao gồm tên gói (package name), các thành phần (activities, services, v.v.), quyền (permissions), cấu hình mạng, cấp độ API (API level) và nhiều hơn nữa. |
|         | java     | Chứa mã nguồn Java của ứng dụng.                                                                                                                                                                   |
|         | res      | Chứa các tài nguyên ứng dụng như chuỗi giao diện người dùng (UI strings), hình ảnh, tệp XML bố cục (layout XML files) và các tài sản tĩnh khác được ứng dụng sử dụng.                              |

### Gradle Scripts
| Tệp                                             | Mô tả                                                                                                                                                                                                      |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| build.gradle                                    | Định nghĩa các cấu hình xây dựng (build configurations) cho dự án hoặc module, bao gồm các dependency, loại bản dựng (build types) và liệu các công cụ tối ưu hóa mã (như ProGuard) có được bật hay không. |
| [proguard-rules.pro](http://proguard-rules.pro) | Chỉ định các quy tắc tùy chỉnh cho ProGuard.                                                                                                                                                               |

### Các loại ứng dụng
+ Native apps : Là các ứng dụng được xây dựng riêng cho 1 hệ điều hành cụ thể, thường được code  bằng Java hoặc Kotlin, có quyền truy cập trực tiếp vào các tính năng bảo mật và các API hệ thống
+ Web apps : Chỉ là web trên điện thoại.
+ Hybrid apps : Lai giữa cả Native apps và Web apps, có thể hoạt động đa nền tảng


## Native Apps

Đầu tiên ở mục `app/res/layout`, vào file  `activity_main.xml`
![[Pasted image 20250709142049.png]]
Layout được định nghĩa là 1 `user interface` của ứng dụng và Android sử dụng **XML** để tạo các file layout. Trong tệp `activity_main.xml` này, ta có thể thêm các `text` , `button` , `image`,... và chúng sẽ được hiển thị cho người dùng. Đoạn mã sau đây sẽ tạo **layout** của một **application** in một thông báo lên màn hình khi nút được nhấn.
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="My Application"
        android:textSize="32sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.097" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/title"
        app:layout_constraintVertical_bias="0.403" />

    <TextView
        android:id="@+id/message"
        android:layout_width="380dp"
        android:layout_height="31dp"
        android:text="@string/message"
        android:textSize="20sp"
        android:textAlignment="center"
        android:textIsSelectable="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/button"
        app:layout_constraintVertical_bias="0.25" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

Đoạn mã trên bao gồm ba đối tượng: hai **TextView** và một **Button**. Các thuộc tính sau đây đáng chú ý:

| Thuộc tính                    | Mô tả                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| tools:context=".MainActivity" | Định nghĩa Activity mà layout sẽ được sử dụng. Thuộc tính này chủ yếu được dùng trong trình chỉnh sửa layout cho mục đích xem trước và không ảnh hưởng đến hành vi khi chạy (runtime behavior) của app.                                                                                                                                                                                                                             |
| android:id                    | Gán một định danh duy nhất cho đối tượng, cho phép nó được tham chiếu trong mã Java (chẳng hạn như MainActivity.java) và các resources khác. Tiền tố @+id cho biết nó sẽ được tạo thành một resource mới, trong khi @id sẽ được sử dụng nếu resource đã được định nghĩa.                                                                                                                                                            |
| android:text                  | Đặt nội dung văn bản của TextView hoặc Button. Giá trị có thể là một chuỗi được mã hóa cứng, như android:text="My Application", hoặc một tham chiếu đến một string resource từ tệp res/values/strings.xml tương đối so với project. Tham chiếu string resources là cách tiếp cận được khuyến nghị để bản địa hóa (localization) và dễ bảo trì. Ví dụ dưới đây cho thấy nội dung của tệp strings.xml được sử dụng trong project này. |
```xml
<resources>
    <string name="app_name">My Application</string>
    <string name="message">Hello World!</string>
</resources>
```

Tất cả các giá trị trên đều có thể được truy cập trong mã Java bằng cách sử dụng lớp **R**.Lớp **R**, được Android tự động tạo, chứa các **ID** của tất cả các **resources** trong thư mục `res/`

Bây giờ chúng ta xem nội dung của tệp `MainActivity.java`, chứa mã java của app
```java
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView message;
    Button button;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        message = (TextView)findViewById(R.id.message);
        button = (Button)findViewById(R.id.button);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                message.setText("Hello from Java!");
            }
        });
    }
}
```

Lớp `MainActiity` bao gồm phương thức `onCreate()` phương thức này sẽ gọi khi activity được khởi động. Dòng `setContentView(R.layout.activity_main);` chỉ ra rằng tệp `activity_main.xml` sẽ được sử dụng để thiết lập layout cho activity này. Các biến `message` và `button` được khởi tạo để trỏ tới các đối tượng tương ứng trong tệp `activity_main.xml`

Sử dụng tệp **R.java**, `R.id.message` trỏ đến thuộc tính `android:id="@+id/message"` trong tệp **activity_main.xml** mà chúng ta đã thấy trước đó. Cuối cùng, dòng `message.setText("Hello from Java!");` sẽ được thực thi ngay khi nút được nhấp, như dòng `button.setOnClickListener` chỉ ra. Một khi nó được nhấn, văn bản **Hello from Java!** sẽ được đặt trong **TextView**.
![[Pasted image 20250709230421.png]]

Đoạn mã dưới đây cho thấy cùng một **app** được viết bằng **Kotlin**. Để cấu hình **project** sử dụng **Kotlin** làm ngôn ngữ lập trình mặc định, chúng ta phải chọn **Kotlin** trong trường **Language** trên cửa sổ **New Project** khi tạo một **new project** trong **Android Studio**. Sau đó, tùy chọn, chúng ta cũng có thể chọn **Kotlin DSL (build.gradle.kts)** trong trường **Build configuration language** để tận dụng cú pháp **Kotlin** cho các **Gradle build scripts**.

```kotlin
package com.example.myapplication

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.TextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val message = findViewById<TextView>(R.id.message)
        val button = findViewById<Button>(R.id.button)

        button.setOnClickListener {
            message.text = "Hello from Java!"
        }
    }
}
```

Mặc dù **Kotlin** và **Java** sử dụng cú pháp khác nhau, nhưng hầu hết các công cụ sẽ tạo ra cùng một **pseudocode** khi phân tích ngược (**reverse engineering**) **app**. Điều này có nghĩa là chúng ta không cần thiết phải thành thạo cả hai ngôn ngữ lập trình. Một khi **app** được phát triển, chúng ta có thể xuất một tệp **APK** đã ký (**signed APK file**) sẵn sàng để cài đặt. Dưới **Build** -> **Generate Signed Bundle / APK...**, chúng ta chọn **APK** và nhấp **Next**.

![[Pasted image 20250709231316.png]]
Ở cửa sổ tiếp theo, ta ấn `Create New...` để tạo 1 key mới
![[Pasted image 20250709231358.png]]
Sau đó, ta thiết lập các trường : 
+ Key store path : Đường dẫn để lưu key
+ Password
+ Alias : bí danh
+ Firstname and lastname
![[Pasted image 20250709231617.png]]

Tiếp theo, chọn `Next`
![[Pasted image 20250709231705.png]]
Cuối cùng, ta chọn option `release` rồi ấn `Finish`
![[Pasted image 20250709231735.png]]
File APK đã ký sẽ được tìm thấy ở thư mục
`~/AndroidStudioProjects/MyApplication/app/release/` với tên là `app-release.apk`
```shell
0xlc13n@htb[/htb]$ ls -l ~/AndroidStudioProjects/MyApplication/app/release/

total 8856
-rw-r--r--@ 1 bertolis  bertolis  4527105 May  3 01:44 app-release.apk
-rw-r--r--@ 1 bertolis  bertolis      379 May  3 01:44 output-metadata.json
```

## Native code
**Native code** là mã được biên dịch để chạy trên một kiến trúc bộ xử lý cụ thể, điều này có thể mang lại lợi thế về hiệu suất cho các **app** được viết bằng **native code** trên phần cứng tương thích. **Android Studio** hỗ trợ việc đưa **native code** vào thông qua **Native Development Kit (NDK)**, cho phép các nhà phát triển viết các phần của **app** bằng **C** hoặc **C++**. Việc này thường được thực hiện để giảm độ trễ (**latency**), tối ưu hóa khả năng phần cứng, hoặc trong một số trường hợp để tăng cường bảo mật cho một **application**.

**Native code** thường được bao gồm trong **application** dưới dạng các thư viện chia sẻ (**shared libraries** - tệp `.so`). Các thư viện này sau đó có thể được gọi từ **Java** hoặc **Kotlin** bằng cách sử dụng **Java Native Interface (JNI)**. **JNI** là một framework định nghĩa cách mã được quản lý (**managed code** - **Java/Kotlin**) tương tác với mã **native** không được quản lý (**unmanaged native code** - **C/C++**), cho phép các cuộc gọi phương thức **cross-language** và trao đổi dữ liệu.

![[Pasted image 20250710082026.png]]

Để hiểu rõ hơn cách **native code** hoạt động, chúng ta hãy tạo một **project Native C++**. Để thực hiện điều này, trước tiên hãy khởi chạy **Android Studio** và điều hướng đến **New Project** -> **Native C++**. Tiếp theo, đặt tên cho **app** của bạn, sau đó trong cửa sổ tiếp theo, dưới phần **C++ Standard**, chọn **Toolchain Default** từ menu thả xuống. Cuối cùng, nhấp **Finish**.
![[Pasted image 20250710082556.png]]
Khi **project** được tạo, chúng ta thấy tệp **native-lib.cpp** nằm trong thư mục **App** -> **cpp** ở phần bên trái của **Android Studio**. Ta sẽ thấy đoạn code sau
```c
#include <jni.h>
#include <string>

extern "C" JNIEXPORT jstring JNICALL
Java_com_example_myapplication_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}
```
Tên hàm **Java_com_example_myapplication_MainActivity_stringFromJNI** tuân theo quy ước đặt tên **JNI** và cho biết rằng nó sẽ được gọi từ lớp **MainActivity**. Dòng `return env->NewStringUTF(hello.c_str());` trả về một **string** cho **Java layer**. Điều quan trọng là phải hiểu cách hàm này xử lý các cuộc gọi từ **Java**, vì mẫu này thường xuyên xuất hiện trong quá trình phân tích ngược (**reverse engineering**). Chúng ta hãy cùng xem tệp **MainActivity.java** để xem thư viện **native-lib.cpp** được tải như thế nào và hàm **native** được gọi ra sao.
```java
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView message;

    // Used to load the 'myapplication' library on application startup.
    static {
        System.loadLibrary("myapplication");
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        message = (TextView)findViewById(R.id.sample_text);
        message.setText(stringFromJNI());
    }

    /**
     * A native method that is implemented by the 'myapplication' native library,
     * which is packaged with this application.
     */
    public native String stringFromJNI();
}
```

Bên trong lớp **MainActivity**, chúng ta có thể thấy dòng `System.loadLibrary("myapplication");`. Đây là nơi thư viện được tải một cách tĩnh (**statically**), được định nghĩa bởi tên **myapplication**. Liệt kê nội dung của tệp **App** -> **cpp** -> **CMakeLists.txt** cho thấy đoạn mã sau đây.
```c
add_library( # Sets the name of the library.
        myapplication

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        native-lib.cpp)
```

---
Như chúng ta có thể thấy, tên của tệp **native-lib.cpp** được đặt thành **myapplication**. Tệp **CMakeLists.txt** được sử dụng để mô tả các tệp của **native C++ project**. Quay lại tệp **MainActivity.java**, chúng ta cũng có thể thấy dòng `public native String stringFromJNI();`, dòng này chỉ ra khai báo của phương thức **native** `stringFromJNI()`. Phương thức này trả về chuỗi **Hello from C++** mà chúng ta đã thấy trước đó trong tệp **native-lib.cpp**, và sau đó nó được in ra màn hình thông qua đối tượng **TextView message**.

