# Lời mở đầu

Đây là bản dịch / diễn giải room Android Fundamental trong HackTheBox. Phần lớn nội dung được dịch lại và được diễn giải một cách dễ hiểu hơn. Có một số phần được điều chỉnh bố cục, nội dung gốc để phù hợp hơn với người mới học. Tài liệu này chỉ dùng để bổ trợ trong quá trình học HTB chứ không thể thay thế hoàn toàn tài liệu gốc. Trong quá trình làm bản dịch này chắc chắn sẽ không thiếu những sai sót, các bạn có thể đóng góp ý kiến cho bản dịch dưới phần comment.

Mặc dù tiêu đề của box là Fundalmental nhưng nội dung chủ yếu là lý thuyết và khó học với người mới. Theo quan điểm của mình, các bạn nên có kiến thức cơ bản về hệ điều hành Linux cùng với kĩ năng lập trình Java căn bản. Các bạn có thể xem trước về lập trình Android bằng Java trên youtube để có cái nhìn tổng thể trước khi học box này. Mình highly recommend các bạn kênh youtube này để học :
[Tự học Lập Trình Android từ A đến Z - YouTube](https://www.youtube.com/playlist?list=PL6aoXCbsHwIayYCo9aDuzZ3dMC9oShs1u)
# Introdution
Android là một hệ điều hành di động được xây dựng dựa trên phiên bản sửa đổi của Linux Kernel, được thiết kế chủ yếu cho các thiết bị màn hình cảm ứng như điện thoại và máy tính bảng. Hệ điều hành này được phát triển bởi một tập đoàn các nhà phát triển được gọi là Open Handset Alliance và được Google tài trợ về mặt thương mại.

**Kiến trúc** : Phần lớn thiết bị Android sử dụng kiến trúc ARM. Các bản Android sau này có bổ sung thêm kiến trúc x86 và x86-64 khi có bộ xử lý Intel
## Android OS

Sử dụng base của Linux Kernel, nên sẽ có dòng lệnh tương tự giống các lệnh linux thông thường
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
Là bản runtime đời đầu được phát triển trước khi ART ra đời. Các ứng dụng Android được viết bằng Java hoặc Kotlin được biên dịch thành Java bytecode và sau đó được chuyển đổi thành **Dalvik bytecode**, đóng gói trong các định dạng tệp **.dex (Dalvik Executable)** hoặc **.odex (Optimized Dalvik Executable)**. Không giống như **Java Virtual Machine (JVM)** vốn dựa trên ngăn xếp (**stack-based**), **Dalvik VM** là một máy ảo dựa trên thanh ghi (**register-based**). Sự khác biệt về kiến trúc này cho phép thực thi hiệu quả hơn trên các thiết bị có tài nguyên **CPU** và bộ nhớ hạn chế, điều này lý tưởng cho môi trường di động.


### Rooting
Android phân tách bộ nhớ flash thành hai phân vùng chính sau đây.
- **/system/** : Dành cho hệ điều hành, chỉ có root mới có full quyền
- **/data/** : Dành cho người dùng bình thường

### Important Directories

| Thư mục                             | Mô tả                                                                                                                                    |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **/data/data**                      | Chứa tất cả các ứng dụng do người dùng cài đặt.                                                                                          |
| **/data/user/0**                    | Chứa dữ liệu mà chỉ ứng dụng đó mới có thể truy cập.                                                                                     |
| **/data/app**                       | Chứa các tệp **APK** của các ứng dụng do người dùng cài đặt.                                                                             |
| **/system/app**                     | Chứa các ứng dụng được cài đặt sẵn của thiết bị.                                                                                         |
| **/system/bin**                     | Chứa các tệp nhị phân (**binary files**).                                                                                                |
| **/data/local/tmp**                 | Một thư mục có thể ghi bởi mọi người dùng (**world-writable**).                                                                          |
| **/data/system**                    | Chứa các tệp cấu hình hệ thống.                                                                                                          |
| **/etc/apns-conf.xml**              | Chứa cấu hình mặc định của **Access Point Name (APN)**. APN được sử dụng để thiết bị kết nối với mạng của nhà cung cấp dịch vụ hiện tại. |
| **/data/misc/wifi**                 | Chứa các tệp cấu hình **WiFi**.                                                                                                          |
| **/data/misc/user/0/cacerts-added** | Kho chứng chỉ người dùng. Chứa các chứng chỉ do người dùng thêm vào.                                                                     |
| **/etc/security/cacerts/**          | Kho chứng chỉ hệ thống. Người dùng không phải **root** không được cấp quyền.                                                             |
| **/sdcard**                         | Chứa một liên kết tượng trưng (**symbolic link**) đến các thư mục **DCIM**, **Downloads**, **Music**, **Pictures**, v.v.                 |

----------------------------------------------------------------------------------------------------------------------------------------------------

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

----------------------------------------------------------------------------------------------------------------------------------------------------
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

![[Pasted image 20250711084600.png]]
Chúng ta không chỉ giới hạn ở việc tải thư viện một cách tĩnh (**statically**). Các thư viện cũng có thể được tải khi **application** đang chạy. Đoạn mã dưới đây cho thấy một lớp tải thư viện khi **app** đang chạy.
```java
public class Update {
    // Method declaration
    public native String stringFromJNI();

    // Copy the file locally and load it
    public String update(String path_sd_card, String filesDir){
        FileOutputStream outputStream;
        FileInputStream inputStream;
      
        try {
            inputStream = new FileInputStream(new File(path_sd_card + "/Download/libupgrade.so"));
            outputStream = new FileOutputStream(new File(filesDir + "/libupgrade.so"));

            FileChannel inChannel = inputStream.getChannel();
            FileChannel outChannel = outputStream.getChannel();
            inChannel.transferTo(0, inChannel.size(), outChannel);
            inputStream.close();
            outputStream.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

        System.load(filesDir + "/libupgrade.so");

        // Returns the value of the function stringFromJNI() from the libupgrade.so file
        return stringFromJNI();
    }
}
```

Sau khi tệp được sao chép vào thư mục chính của **application**, dòng `System.load(filesDir + "/libupgrade.so");` sẽ tải thư viện.

 Note : 
+ Tên của hàm để tải lên thư viện tĩnh : `System.loadLibrary()` 
+ Tên của hàm để tải lên thư viện động : `System.load()`
+ Tên của hàm trả về string trong 1 file cpp : `NewStringUTF()`

## Javascript & WebViews

WebViews là một component giúp nhúng và hiển thị trực tiếp nội dung web vào trong một Android app. Điều này có thể dẫn đến 1 số lỗ hổng liên quan đến Web như SQLi, XSS, LFI,... Vì vậy, theo tài liệu của Android thì ta nên sử dụng trình duyệt mặc định của Android thay vì dùng WebViews để hạn chế rủi ro.

Đoạn mã **XML** sau đây sẽ định nghĩa một phần tử **WebView** bên trong tệp **activity_main.xml layout**.

```xml
<WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

Trong tệp `MainActivity.java` , ta tạo tham chiếu tới `WebView`

```java
package com.example.myapplication;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.webkit.WebView;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        WebView webview = (WebView) findViewById(R.id.webview);
        // WebView sẽ được phép thực thi mã JS
        webview.getSettings().setJavaScriptEnabled(true); 
        // Tải lên tệp index.html
        webview.loadUrl("file:///android_asset/html/index.html");
    }
}
```
![[Pasted image 20250711095139.png]]
Các tệp **HTML** và **Javascript** thường được đặt dưới thư mục **app/assets** (hoặc từ chế độ xem **Project**: **app/src/main/assets**). Nếu thư mục này bị thiếu, chúng ta có thể đơn giản nhấp chuột phải vào **app** và tạo một thư mục mới có tên là **assets**. Dưới đây là ví dụ về cấu trúc **project** bao gồm **HTML**, **CSS** và **Javascript**.
![[Pasted image 20250711095308.png]]

```html
//File html
<html>
<head>
    <link rel="stylesheet" href="../css/style.css">
    <script src="../js/script.js"></script>
</head>
<body>
<h1>
    <script>printMessage()</script>
</h1>
</body>
</html>
```

```javascript
//File js
function printMessage() {
    document.write("Hello from Javascript");
}
```

File `html` đã gọi tới hàm `printMessage()` của file JS và in ra màn hình dòng chữ `Hello from Javascript`
![[Pasted image 20250711095522.png]]

Ngoài ra, WebView cũng cho phép chúng ta load nội dung từ các nguôn bên ngoài local. Ví dụ ta có thể tải trang chủ của Google trong app bằng cách thêm dòng
`webview.loadUrl("https://www.google.com/");` và thêm quyền
`<uses-permission android:name="android.permission.INTERNET" />` vào trong file 
**AndroidManifest.xml** , trước các thể `<application> </application>`

![XML code snippet for Android manifest. Includes permission for internet access: <uses-permission android:name="android.permission.INTERNET" />.](https://academy.hackthebox.com/storage/modules/195/javascript_permissions-2.png)
Thành quả :
![[Pasted image 20250711100029.png]]

## Một số FrameWorks hay dùng

### Flutter

**Flutter** là một **open-source mobile application framework** được phát triển bởi Google. Với **Flutter**, các nhà phát triển có thể xây dựng **applications** bằng ngôn ngữ lập trình **Dart**, sử dụng các **widget** có thể tùy chỉnh và có thể kết hợp để tạo ra các giao diện người dùng phức tạp. Là một **cross-platform application framework**, việc phát triển có thể thực hiện cho các **Android, iOS, Web**, và **Desktop applications** cung cấp hiệu suất cao thông qua **compiled native code**.

Phát triển **Flutter application** có thể được thực hiện bằng cách tải xuống **Flutter SDK** từ **website** chính thức và thiết lập một **IDE** (như **Android Studio**) với các **plugin Flutter** và **Dart**.

Dưới đây là đoạn mã viết `Hello World` bằng Dart : 
```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Hello World App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('My Flatter App'),
        ),
        body: Center(
          child: Text(
            'Hello from Flutter',
            style: TextStyle(fontSize: 28),
          ),
        ),
      ),
    );
  }
}
```
Thành quả :
![[Pasted image 20250711100757.png]]

Cấu trúc project :
![[Pasted image 20250711101237.png]]


Vì Flutter là ngôn ngữ biên dịch native code nên app sẽ lưu trữ mã C++ đã được biên dịch trong các **shared libraries** thành tệp tệp `.so` . Tuy nhiên, pentester vẫn có thể giải mã và kiểm tra các **resources** trong quá trình phân tích tĩnh bằng các công cụ thích hợp. Để đọc được native code đòi hỏi chúng ta có khả năng dịch ngược (reverse enginerring) , cần phải có công cụ và kỹ thuật chuyên biệt.

### Xamarin

**Xamarin** là một **cross-platform application development framework** hỗ trợ xây dựng các **Android, iOS** và **desktop applications**. Thuộc sở hữu của Microsoft, **Xamarin** cho phép các nhà phát triển tạo **Android apps** sử dụng **C#** làm ngôn ngữ lập trình chính trong **Visual Studio**. Để bắt đầu, bạn có thể cài đặt **Mobile development with .NET workload** trong **Visual Studio**. Đoạn mã sau đây cho thấy một **simple "Hello World" application** được viết bằng **C#** sử dụng **Xamarin**.

```c
using Android.App;
using Android.OS;
using Android.Runtime;
using Android.Widget;
using AndroidX.AppCompat.App;

namespace MyApplication
{
    [Activity(Label = "@string/app_name", Theme = "@style/AppTheme", MainLauncher = true)]
    public class MainActivity : AppCompatActivity
    {
        Button button;
        TextView message;
      
        protected override void OnCreate(Bundle savedInstanceState)
        {
            base.OnCreate(savedInstanceState);
            Xamarin.Essentials.Platform.Init(this, savedInstanceState);
            // Set our view from the "main" layout resource
            SetContentView(Resource.Layout.activity_main);
          
            message = FindViewById<TextView>(Resource.Id.message);
            button = FindViewById<Button>(Resource.Id.button);

            button.Click += (sender, args) =>
            {
                message.Text = "Hello World!";
            };
        }
        public override void OnRequestPermissionsResult(int requestCode, string[] permissions, [GeneratedEnum] Android.Content.PM.Permission[] grantResults)
        {
            Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);
            base.OnRequestPermissionsResult(requestCode,permissions, grantResults);
        }
    }
}
```

![[Pasted image 20250711102338.png]]

Cấu trúc project:
![[Pasted image 20250711102358.png]]Khi tạo một **Xamarin app**, mã nguồn **C#** được biên dịch thành **Common Intermediate Language (CIL)** bằng trình biên dịch **.NET**. Mã trung gian này sau đó được thông dịch hoặc biên dịch kịp thời (**just-in-time compiled**) thành mã máy dành riêng cho nền tảng (**platform-specific machine code**) tại thời điểm chạy (**runtime**), tùy thuộc vào môi trường mục tiêu. Không giống như mã **native C++** được biên dịch thành các thư viện chia sẻ (tệp **.so**), các **Xamarin application** đóng gói mã trung gian của chúng dưới dạng **.NET assemblies** (tệp **.dll**), thường được đóng gói trong một tệp duy nhất như **assemblies.blob**.
Vì các **Xamarin app** chứa mã trung gian thay vì các **native binaries**, quá trình phân tích ngược (**reverse engineering**) khác với việc phân tích các **application native C++** hoặc **Java/Kotlin**. Các tệp **.dll** được trích xuất có thể được tải vào các công cụ phân tích ngược **.NET** (chẳng hạn như ILSpy, dnSpy hoặc dotPeek) để khôi phục **pseudocode** dễ đọc. 

### Một số framework khác

Có rất nhiều framework khác có thể được sử dụng để tạo Android app khác như **React Native**, **Apache Cordova** (trước đây là **PhoneGap**), và **Ionic**. Các **framework** này có thể tạo ra các **hybrid cross-platform applications** chạy trên **Android, iOS**, và các trình duyệt web bằng cách sử dụng các công nghệ dựa trên web như **Javascript, HTML**, và **CSS**. Chúng ta có thể cài đặt các **framework** này bằng công cụ dòng lệnh **NPM (Node Package Manager)** và bắt đầu phát triển trên **Android Studio**. Các **application** sau đó có thể chạy trên một thiết bị vật lý (**Physical device**) hoặc thiết bị ảo (**virtual device**).

Dưới đây là đoạn mã Hello World sử dụng React Native : 
```js
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello From React Native</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    fontSize: 28,
  },
});
```
![[Pasted image 20250711103002.png]]

Khi một app được phát triển bằng **React Native**, phần lớn logic và UI của app được viết bằng **JavaScript**. Framework này cũng sẽ tạo ra **MainActivity** và các lớp **Java** cần thiết khác hoạt động như là entry point. Khi app được chuẩn bị để phát hành, mã JavaScript sẽ được đóng gói vào một tệp độc lập có tên **index.android.bundle**. Tệp này được tối ưu hóa và thu nhỏ  để cải thiện hiệu suất và giảm kích thước tổng thể của app. Khi dịch ngược các **app** được tạo bằng React Native, ngoài việc phân tích mã Java để xác định các entry points cần thiết, người kiểm thử cũng nên phân tích mã Javascript được đóng gói trong tệp **index.android.bundle**. Một điều khác mà người kiểm thử nên ghi nhớ là attack surface sẽ khác so với các native app. Các app được tạo bằng các framework như vậy có thể dễ bị tổn thương bởi các lỗ hổng web vì chúng sử dụng các công nghệ web.


Mặt khác, các **app** được tạo bằng các framework **Cordova** và **Ionic** sử dụng một **WebView component** để hiển thị giao diện người dùng và thực thi  **HTML, CSS** và **JavaScript**. Khi chúng ta xây dựng một **app** bằng **Cordova** hoặc **Ionic**, các tài sản web (**web assets** - tệp **HTML, CSS, JavaScript**) được đóng gói trong **application** như một phần của cấu trúc **project** và có thể được tìm thấy trong quá trình phân tích ngược dưới các thư mục **assets/www/** và **assets/public/** tương ứng. 


----------------------------------------------------------------------------------------------------------------------------------------------------


# Android Application Components and Interprocess Communication

Application **components** là các khối được xây dựng cho các thành phần khác nhau của một Android app, chẳng hạn như giao diện người dùng và các chức năng cốt lõi. Các **components** này được khai báo trong tệp `AndroidManifest.xml` .

Interprocess Communication (IPC) là một cơ chế giúp giao tiếp giữa các app hoặc các process khác nhau.

Các app thường bao gồm các component chạy trong các process khác nhau, bao gồm **Activities, Services, Broadcast Receivers**, và **Content Providers**. Vì các ứng dụng sẽ chạy trong tiến trỉn riêng của nó, và IPC sẽ đảm nhiệm vai trò tạo ra cách giao tiếp khi cần thiết giữa các chương trình khác nhau.


## Activity 

### Giới thiệu
Activity là một component cơ bản, đại diện cho một màn hình đơn lẻ của UI và có thể trình bày ở một số chế độ như **full-screen, floating, embedded**, hoặc **multi-window**. Activity là một đối tượng chính giúp cho người dùng và app, nó cũng có thể được khởi động bởi một activity khác, app hoặc các sự kiện hệ thống. Activity cũng có trách nhiệm quản lý vòng đời (lifecycle) của app.

### Acitvity Lifecycle

Vòng đời (**lifecycle**) của một **activity** bao gồm sáu giai đoạn chính được gọi là các **callback**. Lớp dưới đây định nghĩa toàn bộ vòng đời của một **activity**.

```java
public class Activity extends ApplicationContext {
     protected void onCreate(Bundle savedInstanceState);
     protected void onStart();
     protected void onRestart();
     protected void onResume();
     protected void onPause();
     protected void onStop();
     protected void onDestroy();
 }
```
Hệ thống gọi **callback** tương ứng bất cứ khi nào một **Activity** bước vào một trạng thái mới. Lưu ý rằng một ứng dụng có thể chỉ sử dụng một số **callback**. Sơ đồ dưới đây cho thấy vòng đời của một **Activity**.

![[Pasted image 20250711111157.png]]


#### onCreate()

Trong giai đoạn này, **activity** được tạo lần đầu tiên, và nhà phát triển có thể khởi tạo các tác vụ như thiết lập giao diện người dùng (**user interface**), liên kết dữ liệu với các **views**, và cấu hình các **listeners** hoặc **handlers**.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
  
		Toast.makeText(this, "This message will be displayed on the app start-up.", Toast.LENGTH_SHORT).show();
}
```

Phương thức này chỉ nhận một tham số `Bundle savedInstanceState` chứa trạng thái đã lưu trước đó của activity. Đoạn mã trên sẽ hiện lên thông báo ra màn hình ngay khi ứng dụng được khởi động. Vì đây thường là nơi để khởi tạo mọi thông tin cho 1 app nên nó như 1 entry point mà pentester cần chú ý. Mặt khác, chúng ta có thể lưu trữ một số dữ liệu của activity cho `Intent` (đoạn sau sẽ nói tới) để chuyển sang một acitivity khác chẳng hạn như `session tokens`.

#### onStart()
Phương thức **onStart()** được gọi khi **activity** được đưa ra tiền cảnh (**foreground**) và bắt đầu tương tác với người dùng. Các **resources** thường được khởi tạo trong giai đoạn vòng đời này.
#### onResume()
Phương thức này được gọi khi acitity bắt đầu tương tác với người dùng. Nó sẽ tải các tài nguyên và hình ảnh động để người dùng tương tác. Ta có thể gọi phương thức `onPause()` bất cứ khi nào khi đang chạy phương thức này.
#### onPause()
Phương thức này giúp cho chương trình tạm dừng và giải phóng một số tài nguyên tạm thời để tập trung chạy một chương trình khác. Ta có thể gọi phương thức `onResume()` hoặc `onStop()` trong lúc chạy phương thức này.
#### onStop()
Phương thức này giúp ngừng hẳn một chương trình, giải phóng tất cả các resources.
#### onDestroy()
Hủy tất cả những tài nguyên (có thể là cả activity) để tối ưu không gian cho hệ thống.
#### onRestart()
Khởi động lại activity sau khi đã bị dừng.

### Launching an Acitvity

Một activity đại diện cho một màn hình đơn lẻ với giao diện để quản lý tương tác giữa người dùng và ứng dụng. Các bước sau mô tả những gì xảy ra khi một activity đang được chạy.

#### Tạo intent
Một đối tượng `Intent` như là cầu nối để truyền thông tin giữa các component với nhau. Nó có thể dùng để chuyển màn hình, gửi dữ liệu, mở sang app khác hoặc thực hiện một hành động nào đó ở hệ thống. Ví dụ : 
```java
// In the source Activity (e.g., MainActivity.java)
Intent intent = new Intent(this, TargetActivity.class);
// Optionally, you can add extra data to the Intent
intent.putExtra("key", "test");
```

Intent ở trên đóng vai trò thực hiện giao tiếp giữa `MainActivity` và `TargetActivity`. Nó được lưu trữ 1 cặp giá trị `key-value` bằng hàm `putExtra()` ở `MainActivity` và gửi sang cho `TargetActivity`.

### Requesting Activity launch
Để khởi chạy 1 acitivity nào đó, ta có thể dùng hàm `startActivity()`
hoặc `startActivityForResult` và bắt buộc phải truyền một đối tượng `Intent` làm tham số. Sự khác nhau của 2 hàm trên là 1 hàm không mong đợi kết quả từ Activity được khởi chạy, hàm còn lại mong đợi nhận được kết quả từ Activity được khởi chạy.
**Lưu ý** : Hàm `startActivityForResult`  không bắt buộc Activity được khởi chạy phải trả về kết quả. Nếu Activity được chạy không trả về kết quả thì nó sẽ mặc định kết quả là `null`.

```java
// For launching an Activity without expecting any result back
startActivity(intent);

// For launching an Activity and expecting a result back
int requestCode = 1; // A unique integer request code to identify the result
startActivityForResult(intent, requestCode);
```
### Activity Stack management

Hệ điều hành Android luôn duy trì 1 stack để quản lý hoạt động của các Activity. Khi một Activity được khởi chạy, nó sẽ được đặt lên đầu stack và trở thành Activity chính đang được hoạt động. Các Activity khác sẽ bị đẩy xuống dưới. Khi một Activity đang chạy bị destroy thì nó sẽ xóa activity đó đi và chạy tiếp activity ở bên dưới.
![[Pasted image 20250711141400.png]]

### Acitivity lifecylcle transition
Khi chuyển từ một activity sang một activity khác, phương thức `onPause()` sẽ được gọi và sẽ gọi các phương thức `onCreate()` , `onStart()` , `onResume()`  và một số hoạt động cần thiết khác của Activity sẽ được chạy.
```java
public class TargetActivity extends AppCompatActivity {
  
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_target);

        // Get data from the Intent
        String data = getIntent().getStringExtra("key");
    }

// Other lifecycle methods, like onStart(), onResume(), onPause(), onStop(), onDestroy()
}
```


### Hành động quay lại của user
Khi người dùng muốn quay lại Activity cũ, Activity hiện tại sẽ bị loại bỏ khỏi stack và các phương thức vòng đời **onPause(), onStop()**, và **onDestroy()** của nó được gọi. Activity trước đó trong stack sẽ được trở lại trạng thái hoạt động, tiếp tục các vòng đời **onRestart(), onStart()**, và **onResume()**
. Vì vậy trước khi quay lại, nếu có thông tin gì cần thiết để dùng thì ta phải lưu vào 1 Intent.
```java
// Set result and finish the Activity
Intent resultIntent = new Intent();
resultIntent.putExtra("result_key", "result_value");
setResult(RESULT_OK, resultIntent);
finish();
```

### Trả về kết quả (Tùy chọn)
Nếu Activity được khởi chạy bằng `startActivityForResult()`, nó sẽ trả về kết quả cho Activity đã gọi nó và sẽ nhận được trong phương thức `onActivityResult()` của Activity đó. Phương thức đó sẽ trông như sau:
```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

// Mỗi request code tương ứng cho một lời gọi activity khác nhau
    if (requestCode == 1) { 
	    // Nếu kết quả được trả về bình thường
        if (resultCode == RESULT_OK && data != null) {
            String resultData = data.getStringExtra("result_key");
            // Xử lý result data
        }
    }
}
```

Các bước trên được thể hiện qua sơ đồ sau :
![[Pasted image 20250711151421.png]]
Ngoài việc khởi động một activity bằng cách chạm vào icon hoặc thông qua lời gọi của các ứng dụng khác, điều này có thể thực hiện bằng cách sử dụng **ADB(Android Debug Bridge)**. ADB là một công cụ dòng lệnh cho phép người dùng có thể giao tiếp với một thiết bị Android. Nó thường sử dụng cho mục đích gỡ lỗi, phát triển và kiểm thử. 

### Khai báo Activity
Để sử dụng được một Activity, ta phải khai báo nó trong tệp manifest của app. Trong Android thì nó là tệp `AndroidManifest.xml`. Tệp này sẽ chứa các `component`, quyền và các metadata khác. Các thẻ `<activity>` sẽ nằm trong thẻ `<application>`. 
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">

        <!-- Declare your Activity here -->
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!-- Declare other Activities if needed -->
        <!-- <activity android:name=".AnotherActivity" /> -->

    </application>

</manifest>
```

Trong đoạn mã trên, `android:name="android.intent.action.MAIN"` cho biết rằng Activity này là điểm khởi đầu của ứng dụng. Việc xác định điểm khởi đầu của một ứng dụng rất quan trọng trong quá trình pentest vì nó giúp ta hiểu rõ hơn về luồng, chức năng và cấu trúc tổng thể của ứng dụng, phát hiện các attack surface tiềm năng và các lỗ hổng tiềm ẩn. 
`category android:name="android.intent.category.LAUNCHER"` cho biết rằng Activity này được liệt kê trong quá trình khởi chạy ứng dụng của hệ thống và do đó, khi người dụng chạm vào icon của ứng dụng thì Activity này sẽ được khởi động.

Một số activity có thể bao gồm cả thuộc tính `android:exported` có giá trị true/false để chỉ định xem component đó có cho phép ứng dụng khác gọi tới hay không. Nó có thể đặt trong các component như `Activity` ,`Service`, `BroadcastReceiver`. Nên cẩn thận với việc đặt thuộc tính này vì nó có thể dẫn tới một số lỗi bảo mật.
Ví dụ: 
```java
<manifest ...>
    <application ...>
        <activity
            android:name=".MyCustomActivity"
            android:exported="true">
            </activity>
    </application>
</manifest>
```



## Services

Service là một component thực hiện các hoạt động chạy nền (**long-running operations in the background**) mà không cung cấp giao diện người dùng. Service có thể được sử dụng cho các tác vụ như tải xuống tệp, phát nhạc hoặc giao tiếp với một máy chủ từ xa (remote server) và có thể tiếp tục hoạt động ngay cả sau khi người dùng rời khỏi áp. Ví dụ như bạn nghe nhạc trên Zing MP3 chẳng hạn, kể cả khi bạn tắt điện thoại đi thì ứng dụng vẫn chạy, đó là vì ứng dụng đã gọi tới một Service để phát nhạc.
Có 3 loại service trong Android :
+ Foreground Service
+ Background Service
+ Bound Service
### Foreground Service (Dịch vụ tiền cảnh)
Foreground Service thực hiện các hoạt động yêu cầu sự chú ý của người dùng. Nó sẽ gửi cho người dùng thông báo rằng dịch vụ này đang được chạy. Ví dụ về một số service như vậy bao gồm media player như các trình phát nhạc. Một foreground service có thể được bắt đầu bằng cách gọi phương thức `startService()`
### Background Service (Dịch vụ nền)
Background Service thực hiện các hoạt động không yêu cầu tương tác với người dùng(không. Bắt đầu từ **Android API level 26 (Android 8.0 Oreo)**, các **background services** không còn được phép chạy trừ khi ứng dụng ở chế độ tiền cảnh (**foreground**). Điều này giúp tối ưu tài nguyên hệ thống và tối ưu hóa thời lượng pin.

### Bound Service (Dịch vụ liên kết)
Bound services cho phép các component khác liên kết với chúng bằng cách gọi phương thức `bindService()`. Chúng cung cấp một giao diện client-server cho phép các component, ngay cả trên các tiến trình khác nhau tương tác với Service này bằng cách sử dụng **Interprocess Communication (IPC)**.

### Tính chất của Service
Tất cả các Service sẽ được kế thừa từ lớp `Service`

```java
public class ExampleService extends Service {
    int startMode;       // chỉ ra cách xử lý nếu service bị dừng
    IBinder binder;      // giao diện cho các client liên kết
    boolean allowRebind; // chỉ ra liệu onRebind có nên được sử dụng hay không
    ...
}
```
Tương tự như Activity, các Service có các phương thức lifecycle callback phải được triển khai để giám sát các thay đổi trong trạng thái của chúng. Sơ đồ dưới đây cho thấy các phương thức lifecycle callback của service. Ở bên trái, service được tạo bằng cách sử dụng `startService()`, trong khi ở bên phải, bằng cách sử dụng `bindService()`.
![[Pasted image 20250713091054.png]]
Ta cũng cần phải liệt kê tất cả các Service trong file `AndroidManifest.xml`
```xml
<manifest ...>
    <application ...>
        <service android:name=".MyForegroundService"/>
        <service android:name=".MyBackgroundService"/>
    </application>
</manifest>
```

## Broadcast Receiver

**Lưu ý** :
+ Broadcast là một tín hiệu được gửi từ một ứng dụng hoặc từ hệ thống về một trạng thái nào đó của nó. Nó giống như 1 cái loa phát thanh để truyền tín hiệu thông báo của hệ thống/ ứng dụng với.
+ Trong đoạn dưới có thể ngầm hiểu `Receiver` chính là `Broadcast Receiver`

`BroadcastReceiver` là một component không có giao diện người dùng, được sử dụng để lắng nghe các broadcast từ hệ thống hoặc các ứng dụng khác. Nó được coi là một cơ chế **Interprocess Communication (IPC)** (cơ chế cho phép các ứng dụng giao tiếp với nhau).
Ví dụ: Khi pin yếu, khi có tin nhắn đến, khi kết nối mạng thay đổi,... thì hệ thống sẽ gửi một broadcast và nếu ứng dụng của bạn có đăng ký `BroadcastReceiver` để lắng nghe broadcast đó thì nó sẽ được kích hoạt.
**Broadcast Receivers** thừa kế lớp **BroadcastReceiver** và ghi đè phương thức `onReceive()` để xử lý các sự kiện khớp với một **Intent Filter** đã được khai báo trong `AndroidManifest.xml`. Ví dụ sau đây cho thấy một Broadcast Receiver xử lý một sự kiện khi thiết bị đang sạc.
```java
public class MyBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
	    // Xử lý khi nhận được broadcast
        String action = intent.getAction();

        if (action != null) {
            switch (action) {
                case Intent.ACTION_POWER_CONNECTED:
                    // Handle the power connected event
                    break;
                case Intent.ACTION_POWER_DISCONNECTED:
                    // Handle the power disconnected event
                    break;
                default:
                    // Handle other actions as needed
                    break;
            }
        }
    }
}
```

Broadcast Receiver cũng cần được khai báo trong tệp `AndroidManifest.xml`

```xml
<manifest ...>
    <application ...>
        <receiver android:name=".MyBroadcastReceiver">
            <intent-filter>
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
                <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
            </intent-filter>
        </receiver>
    </application>
</manifest>
```

Các phương thức sau đây được sử dụng để gửi các Broadcast đến các nơi khác nhau:

| Phương thức                                 | Mô tả                                                                                                                                               |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| sendOrderedBroadcast(Intent, String)        | Gửi broadcast đến từng Receiver một theo thứ tự.                                                                                                    |
| sendBroadcast(Intent)                       | Gửi broadcast đến tất cả các Receiver theo một thứ tự không xác định.                                                                               |
| localBroadcastManager.sendBroadcast(intent) | Gửi các Intent broadcasts đến các đối tượng cục bộ trong tiến trình. Phương thức này đã bị loại bỏ từ API 28, và LiveData được sử dụng để thay thế. |

## Content Provider

**ContentProvider** là một lớp trung gian sử dụng cơ chế **IPC** cho phép ứng dụng cung cấp dữ liệu của mình cho các ứng dụng khác (hoặc dùng nội bộ), thông qua một giao diện thống nhất. Nó đóng vai trò giống như một “cổng” truy cập dữ liệu.
Ví dụ: Danh bạ, tin nhắn, hình ảnh,... đều được Android lưu trữ và chia sẻ thông qua Content Provider. Ví dụ khi ta chọn ảnh để up lên face hoặc chọn một tệp để gửi qua tin nhắn thì Content Provider sẽ được sựng dụng.
Content Providers sử dụng một API tiêu chuẩn hóa dựa trên các hoạt động CRUD (Create, Read, Update, Delete) để tương tác với dữ liệu. Dữ liệu được xử lý bởi một Content Provider có thể được lưu trữ trong nhiều cấu trúc, bao gồm cơ sở dữ liệu SQLite cục bộ, bộ nhớ trong hoặc ngoài của thiết bị, hoặc thậm chí trên một máy chủ từ xa .

![[Pasted image 20250713094217.png]]

Việc truy cập một ContentProvider thường được chạy nền và xử lý bất đồng bộ bằng cách sử dụng **CursorLoader** để thực thi các truy vấn. Các component khởi tạo một yêu cầu tới **CursorLoader** và **CursorLoader**  sẽ thực hiện truy vấn để lấy dữ liệu bằng cách truy cập **ContentProvider** thông qua **ContentResolver**.
![[Pasted image 20250713094816.png]]
Giải thích :
 1. **Activity ofFragment**
	- Là nơi hiển thị dữ liệu trên giao diện người dùng (UI).
	- Gọi `LoaderManager` để khởi tạo hoặc quản lý `CursorLoader`.
 2. **CursorLoader**
	- Là một lớp dùng để tải dữ liệu bất đồng bộ (asynchronously) từ ContentProvider.
	- Trả về một đối tượng `Cursor` (bảng dữ liệu).
	- Tránh chặn main thread (giao diện) khi truy vấn dữ liệu lớn.

 3. **ContentResolver**
	- Là lớp trung gian để tương tác với ContentProvider.
	- Không truy cập trực tiếp vào dữ liệu mà sẽ **gửi yêu cầu truy vấn đến ContentProvider** qua `URI`.
	- Cung cấp các hàm: `query()`, `insert()`, `update()`, `delete()`...

4. **ContentProvider**
	- Là nơi xử lý yêu cầu dữ liệu (query, insert, update, delete) đến từ ContentResolver.
	- Truy cập vào nguồn dữ liệu thật như SQLite, file, bộ nhớ nội bộ,...
	- Trả kết quả về lại cho ContentResolve

Đoạn code sau đây truy xuất các từ và vị trí của chúng từ **User Dictionary Provider**. Một **User Dictionary Provider** là một **ContentProvider** trong Android quản lý từ điển tùy chỉnh của người dùng. Để đạt được điều này, nó gọi **ContentResolver.query()**, tiếp theo nó sẽ gọi phương thức **ContentProvider.query()** được triển khai bởi **User Dictionary Provider**.
```java
// Queries the user dictionary and returns results
cursor = getContentResolver().query(
    UserDictionary.Words.CONTENT_URI,  // The content URI of the words table
    projection,                        // The columns to return for each row
    selectionClause,                   // Selection criteria
    selectionArgs,                     // Selection criteria
    sortOrder);                        // The sort order for the returned rows
```
Lớp `ContentProvider`:
```java
public class MyContentProvider extends ContentProvider {
    // Implement required CRUD methods and other logic here
    // Thao tác với cơ sở dữ liệu và xử lý các logic để trả về dữ liệu
}
```
Content Provider cũng cần cấp các quyền cần thiết để có thể truy cập dữ liệu từ cơ sở dữ liệu nên nó cần được khai báo cùng các quyền trong `AndroidManifest.xml`
```xml
<manifest ...>
    <application ...>
        <provider
            android:name=".MyContentProvider"
            android:authorities="com.example.myapp.provider"
            android:exported="false" />
    </application>
</manifest>
```
Tương tự như Activities và Broadcast Receivers, Content Providers có thể được truy cập bằng Android Debug Bridge (ADB) thông qua terminal.

## Intent
Intent là đối tượng được ứng dụng hoặc hệ thống sử dụng để yêu cầu các hành động từ các component khác như Activity, Service, Broadcast Receiver. Mặc dù không được thiết kế theo IPC, nó vẫn có thể sử dụng nếu ứng dụng muốn tương tác với một component nằm trong một tiến trình khác. 
Ta có thể coi Intent như một gói thư được gửi tới các Component khác.
Intent có thể lưu trữ dữ liệu để sử dụng ở nhiều Component khác nhau bằng cách sử dụng các cặp `key-value`, được gọi là `extra`
```java
Intent intent = new Intent(this, TargetActivity.class);
intent.putExtra("key", "value");
startActivity(intent);
```
Cũng giống như Application Components, Intents có thể được tạo bằng Android Debug Bridge (ADB) thông qua terminal. Việc hiểu và phân tích Intents trong khi đánh giá một application là rất quan trọng—không chỉ để hiểu rõ hơn về luồng (flow) của app mà còn để xác định các khả năng bỏ qua bảo mật (security bypasses) tiềm ẩn.
### Các trường hợp sử dụng Intent
Có 3 trường hợp thường sử dụng Intent :
+ Khởi động một Activity
+ Khởi động một Service
+ Phát một broadcast
#### Khởi động một Activity
Intent thường sử được sử dụng để khởi chạy các Activity mới và truyền dữ liệu giữa các Activity với nhau.
```java
/* Navigating from a list of contacts to a detailed view of the selected contact. 
   In the source Activity (ContactListActivity.java), an explicit Intent tells 
   Android to launch the target Activity (ContactDetailActivity.java) and passes 
   the selected contact's ID as extra data. This allows the target activity to 
   retrieve and display the correct contact details. */

Intent intent = new Intent(this, ContactDetailActivity.class);
intent.putExtra("contact_id", selectedContactId);
startActivity(intent);
```
#### Khởi động một Service
Intent có thể được sử dụng để khởi động hoặc liên kết với các dịch vụ chạy nền
``` java
/* Tải xuống một tệp trong nền. Đoạn code này khởi động một background Service
   (DownloadService) để xử lý việc tải xuống tệp. Một Intent chỉ định
   lớp target Service và đính kèm URL tệp làm extra data. Service sau đó có thể
   truy xuất URL từ Intent và bắt đầu hoạt động tải xuống trong nền. */
Intent intent = new Intent(this, DownloadService.class);
intent.putExtra("file_url", fileUrl);
startService(intent);
```
#### Phát một Broadcast
Broadcasts cho phép các ứng dụng gửi hoặc lắng nghe các sự kiện trên toàn hệ thống hoặc sự kiện cụ thể của ứng dụng.
```java
/* Thông báo cho các component khác rằng pin yếu. Mã này gửi một custom
   broadcast với chuỗi action `com.example.ACTION_BATTERY_LOW`. Bất kỳ component
   nào (trong cùng app hoặc giữa các app) đã đăng ký một BroadcastReceiver với
   một Intent filter phù hợp sẽ được thông báo khi broadcast này được gửi. */
Intent intent = new Intent("com.example.ACTION_BATTERY_LOW");
sendBroadcast(intent);
```

### Phân loại Intent
Intent bao gồm 2 loại **Explicit Intent** và **Implicit Intent**
#### Explicit Intent (Intent rõ ràng)
Explicit Intent thường được sử dụng để điều hướng giữa các Activity trong cùng một ứng dụng hoặc khởi động Service. Component đích (Activity, Service, hoặc Broadcast Receiver) phải được biết và có thể được tạo bằng cách chỉ định tên lớp của Component đích trong hàm tạo Intent.
```java
Intent intent = new Intent(this, TargetActivity.class);
startActivity(intent);
```

#### Implicit Intent (Intent ngầm định)
Implicit Intent được sử dụng khi chúng ta không biết chính xác Component đích, nhưng biết hành động chúng ta muốn thực hiện và muốn hệ thống tìm một Component phù hợp để xử lý yêu cầu. Để tạo một implicit Intent, chúng ta phải chỉ định hành động và dữ liệu (URI).
``` java
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://www.example.com"));
startActivity(intent);
```

Hình ảnh sau đây cho thấy cách một implicit intent được gửi qua hệ thống để bắt đầu một activity khác.
![[Pasted image 20250713110139.png]]

## Binder

Binder là cơ chế **Interprocess Communication (IPC)** cốt lõi của Android, cho phép giao tiếp hiệu quả và an toàn giữa các tiến trình khác nhau. Nó được xây dựng trên mô hình **Remote Procedure Call (RPC)**, cho phép một tiến trình  gọi các phương thức trên một đối tượng từ xa nằm trong một tiến trình khác như thể đối tượng đó ở cục bộ.

Theo ý hiểu của mình, Binder như một đối tượng cung cấp một giao diện giúp cho 1 service đóng vài trò như 1 server và có thể xử lý các yêu cầu từ các đối tượng từ xa (client). Đối tượng từ xa này có thể là 1 service hoặc component khác. 

Từ giờ ta sẽ coi các service từ xa (remote service) là một service đang chạy trong cùng một ứng dụng nhưng trong một tiến trình khác.  Binder thường được sử dụng thông qua một Service triển khai một interface được định nghĩa trong tệp AIDL, chỉ định các phương thức, tham số và giá trị trả về cho IPC. Service cung cấp chức năng được yêu cầu, trong khi Binder tạo điều kiện giao tiếp giữa client và service. Dưới đây là 1 số file code minh họa cách một Service sử dụng Blinder để giao tiếp với một đối tượng từ xa.


### ICalculator.aidl
File này là 1 interface để khai báo các phương thức
``` java
interface ICalculator {
	int add(int a, int b);
}
```

Tiếp theo, chúng ta có một đoạn mã của tệp `CalculatorService.java`, tệp này tạo một service và triển khai interface đã được định nghĩa trong tệp AIDL trước đó.

```java
public class CalculatorService extends Service {
    private final ICalculator.Stub binder = new ICalculator.Stub() {
        @Override
        public int add(int a, int b) {
            return a + b;
        }
    };

    @Override
    public IBinder onBind(Intent intent) {
        return binder;
    }
}
```

Đoạn code trên tạo một `Service` tên là `CalculatorService`, cung cấp phương thức `add(int a, int b)` thông qua AIDL, cho phép client truy cập vào service và gọi `add()` từ xa.

`ICalculator` là giao diện AIDL đã được Android tự động sinh ra từ file `ICalculator.aidl`.
`Stub` là lớp `server-side` dùng để nhận các lời gọi từ client.
Phương thức add() được ghi đè và cung cấp logic cộng hai số.

Phương thức `public IBinder onBind(Intent intent)` được gọi khi client gọi tới phương thức `bindService()`. Nó sẽ trả về 1 đối tượng có kiểu `IBinder` để hệ thống dùng làm cầu nối giữa client và server.

### MainActivity.java

Tệp `MainActivity.java` sẽ  kết nối (connecting) và liên kết (binding) với remote service `CalculatorService`, và sau đó gọi các phương thức của nó. Kết nối (connecting) với một Service bao gồm việc thiết lập một liên kết với Service để giao tiếp và tương tác với nó, trong khi liên kết (binding) với một Service thiết lập một kết nối lâu dài giữa một client (chẳng hạn như một Activity) và một Service. Điều này cho phép client tương tác với Service, gọi các phương thức của nó và nhận kết quả một cách đồng bộ.
```java
// Kết nối với remote service
private ServiceConnection serviceConnection = new ServiceConnection() {
    @Override
    public void onServiceConnected(ComponentName name, IBinder service) {
        calculatorService = ICalculator.Stub.asInterface(service);
        performCalculations();
    }
    // ...
};

// ...

// Liên kết với remote service
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    Intent intent = new Intent();
    intent.setComponent(new ComponentName("com.example.calculatorservice", "com.example.calculatorservice.CalculatorService"));
    bindService(intent, serviceConnection, Context.BIND_AUTO_CREATE);
}

// ...

// Gọi các phương thức
private void performCalculations() {
    if (calculatorService == null) {
        return;
    }

    try {
        int additionResult = calculatorService.add(10, 5);
        
        // Sử dụng kết quả nếu cần, ví dụ: hiển thị chúng trong UI
        // ...

    } catch (RemoteException e) {
        e.printStackTrace();
    }
}
```

Binders không được khai báo trực tiếp trong tệp manifest, vì chúng là một phần của việc triển khai Service. Tuy nhiên, nếu Service chạy trong một tiến trình khác, thuộc tính `android:process` nên được chỉ định trong tệp `AndroidManifest.xml`.
```xml
<manifest ...>
    <application ...>
        <service
            android:name=".MyService"
            android:process=":remote" />
    </application>
</manifest>
```

## Deep Link

Deep Link là một cơ chế Interprocess Communication (IPC) cho phép người dùng điều hướng trực tiếp đến nội dung cụ thể trong một app bằng cách chạm vào một URL tìm thấy trên một trang web, email hoặc bất kỳ vị trí nào khác có thể đặt liên kết.

Ví dụ, một người dùng có thể nhận được một email quảng cáo về một đợt giảm giá chớp nhoáng cho một sản phẩm cụ thể. Thay vì đưa người dùng đến trang web, liên kết sẽ mở app tương ứng để hiển thị sản phẩm đó. Trong một số trường hợp, nếu app chưa được cài đặt, người dùng sẽ được chuyển hướng đến cửa hàng app store để tải xuống và cài đặt. Có hai loại Deep Link, đó là Standard Deep Link và Android App Link.
### Standard Deep Link
Ví dụ dưới đây minh họa một trang web cung cấp các Deep link để liệt kê các sản phẩm máy tính của nó thông qua mobile app. Mã nguồn của trang web trông như sau:
```html
<div>
	<p>Buy our latest PC parts.</p>
	<a href="app://myapp/products/cpu"> </a>
</div>
```
Để URL trên mở được ứng dụng , chúng ta phải thiết lập một intent filter trong tệp `Androidmanifest.xml` cho Activity tương ứng.
```xml
<activity android:name=".ProductsActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="app"
              android:host="myapp"
              android:pathPrefix="/products/" />
    </intent-filter>
</activity>
```
Bảng dưới đây cung cấp mô tả về các yếu tố quan trọng nhất của đoạn mã trên :

| Phần tử                                       | Mô tả                                                                                                                                      |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `<activity android:name=".ProductsActivity">` | Định nghĩa activity sẽ được khởi chạy khi liên kết được nhấn.                                                                              |
| `android:scheme="app"`                        | Thiết lập giao thức (protocol). Nó định nghĩa app (có thể là bất cứ thứ gì) của URL `app://myapp/products/cpu` được nhúng trong trang web. |
| `android:host="myapp"`                        | Thiết lập host. Nó định nghĩa phần myapp (có thể là bất cứ thứ gì) của URL `app://myapp/products/cpu` được nhúng trong trang web.          |
| `android:pathPrefix="/products/" />`          | Đặt tiền tố đường dẫn (path prefix). Nó định nghĩa phần /products/ của URL `app://myapp/products/cpu` được nhúng trong trang web.          |
Đoạn mã Java sau xử lý các Intent mà Service được nhận
```java
public class ProductActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_planet);

        Intent intent = getIntent();
        String action = intent.getAction();
        Uri data = intent.getData();
		// Nếu action là xem 
        if (Intent.ACTION_VIEW.equals(action) && data != null) {
            String ProductName = data.getLastPathSegment();
          
          	if (ProductName.equals("cpu")) {
            	// Thực hiện một số hành động. Ví dụ, truy vấn cơ sở dữ liệu để lấy thông tin về sản phẩm này.
            }
        }
    }
}
```

Trong đoạn mã Java trên, câu lệnh `if()` kiểm tra xem giá trị trả về từ phương thức `data.getLastPathSegment()` có bằng `cpu` hay không. Giá trị trả về từ phương thức `data.getLastPathSegment()` thực chất là phần `cpu` của URL `app://myapp/products/cpu`.

Đây là cách Android xử lý một Standard Deep Link. Mặc dù deep link là một cơ chế mạnh mẽ, các rủi ro bảo mật có thể phát sinh từ việc triển khai không đúng cách. Trong ví dụ trên, thuộc tính `android:scheme` được đặt thành `app`, và `android:host` được đặt thành `myapp`. Tuy nhiên, Android không bắt buộc xác minh quyền sở hữu cho các custom schemes, có nghĩa là bất kỳ app độc hại nào cũng có thể tự khai báo  cho scheme đó, có khả năng dẫn đến các lỗ hổng bảo mật. Để giảm thiểu rủi ro này, ta nên sử dụng **Android App Links**.

### Android App Link
Giả sử rằng URL `https://www.myapp.com/` dẫn đến một trang web hiện có, deep link trong đó sẽ trông như sau:
```html
<div>
	<p>Buy our latest PC parts.</p>
	<a href="https://www.myapp.com/products/cpu"> </a>
</div>
```
Tệp `AndroidManifest.xml` :
```xml
<activity android:name=".ProductsActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="https"
              android:host="www.myapp.com"
              android:pathPrefix="/products/" />
    </intent-filter>
</activity>
```

Chúng ta nhận thấy rằng thuộc tính `android:scheme` được đặt thành https, và `android:host` được đặt thành `www.myapp.com`. Trong trường hợp này, nếu app xử lý deep link không được cài đặt, liên kết sẽ mở trong trình duyệt web liệt kê các sản phẩm. Đây là một tính năng được thêm vào trên Android 6.0 trở lên, đảm bảo rằng chỉ chủ sở hữu miền được xác minh mới có thể xử lý các liên kết đến miền đó trong app của họ, và các app độc hại tiềm năng khác sẽ không thể xử lý liên kết này.

Mặt khác, lập trình kém vẫn có thể dẫn đến các vấn đề bảo mật. Hãy tưởng tượng một app xử lý URL `https://www.myapp.com/home?uid=50&token=RLsB?19oYMAL6M5v`. Nếu app không xác minh các tham số uid và token được truyền qua deep link, một kẻ tấn công độc hại có thể tạo liên kết của riêng họ với các giá trị tham số khác, dẫn đến truy cập trái phép vào dữ liệu của người dùng khác. 
### Kết luận
Để tăng cường bảo mật khi sử dụng Deep Links, chúng ta nên sử dụng Android App Link (đảm bảo các liên kết được xác minh và xử lý an toàn) thay vì Generic Deep Link. Ngoài ra, cần xác thực đầu vào của các tham số và tránh truyền dữ liệu nhạy cảm qua URL.

-------------------------------------------------- 
# Setting Up The Testing Environment

Cái này các bạn tự đọc tại tài liệu gốc và làm theo hướng dẫn của họ.

-----------------

# Skills Assessments

Các bạn tự đọc và làm bài tập ở tài liệu gốc.