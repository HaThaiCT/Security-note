## Basic
### Keywords

+ Plaintext : the original, readable message or data before it's encrypted.
+ Ciphertext : phiên bản của tin nhắn sau khi được mã hóa
+ Cipher : thuật toán mã hóa
+ Key
+ Encryption : Mã hóa
+ Decryption : Giải mã
+ authentication : sự xác thực => authenticity : tính xác thực : chắc chắn đang giao tiếp với đúng người
+ integrity : tính toàn vẹn : đảm bảo không ai khác có thể làm thay đổi dữ liệu
+ confidentiality : tính bí mật : không bị nghe lén

### Symmetric Encryption (Mã hóa đối xứng)

+ only 1 key
+ DES
+ 3DES
+ AES

### Asymmetruc Encryption

+ use public key to encrypt and private key to decrypt
+ RSA, Diffie-Hellman

### Math Basic

+ XOR : encrypt C = P(parameter) ^ K(key) => decrypt : C ^ K = (P ^ K) ^ K = P
+ Modulo : Phép toán không thể đảo ngược

## Public Key Cryptography Basic

+ Sử dụng mã hóa bất đối xứng để gửi đi khóa đối xứng

| Analogy     | Cryptographic System                                |
| ----------- | --------------------------------------------------- |
| Secret Code | Symmetric Encryption Cipher and Key (khóa đối xứng) |
| Lock        | Public Key                                          |
| Lock’s Key  | Private Key                                         |

### RSA
![[Pasted image 20250218232430.png]]

+ Bob chon 2 số nguyên tố p = 157 và q = 199. Anh ấy tính ra n = p x q = 31243
+ Ta có hàm _ϕ_(_n_) = n - p - q + 1 = (p - 1) x (q- 1) = 30888, Bob sẽ chọn e = 163 là 1 số nguyên tố cùng nhau với _ϕ_(_n_). 
+ Bob sẽ chọn được 1 số d = 379 sao cho (e x d) mod _ϕ_(_n_) = 1 (có thể sử dụng nghịch đảo modulo)
+ Public key sẽ là (n,e) = (31243,163)
+ Private key sẽ là (n,d) = (31243,379)
+ Giả sử Alice muốn mã hóa giá trị x = 13 cho Bob, ta sẽ mã hóa y = $x^e$ mod n = 13^163 mod 31243 = 16341.
+ Bob sẽ giải mã giá trị nhận được bằng cách tính x = $y^d$ mod n = 16341^379 mod 31243 = 13.

=> tóm lại
+ p,q là các số nguyên tố lớn
+ n = p x q
+ public key : (n,e)
+ private key : (n,d)
+ m : plaintext = $c^e$ % n
+ c : ciphertext = $m^e$ % n
+ Sử dụng để có thể truyền thông điệp là 1 key chung để có thể áp dụng mã hóa đối xứng

### Diffie-Hellman Key Exchange

+ Alice và Bob đồng ý 2 biến công khai : p là 1 số nguyên tố lớn và 1 số g thuộc phần tử sinh của p(g^1,g^2,...,g^(p-1) lần lượt mod p sẽ sinh ra hoán vị gồm các số từ 1->p-1) sao cho 0 < g < p. Giả sử cả 2 sẽ chọn p = 29, g = 3.
+ Mỗi bên chọn 1 private key. Giả sử Alice chọn private key a = 13, Bob chọn private key b = 15
+ Mỗi bên sẽ lần lượt tính ra public key của mình theo công thức  public_key = $g^{private-key}$  mod p . Như ví dụ trên public key của Alice A = $3^{13}$ mod 29 = 19, public key của Bob B = $3^{15}$ mod 29 = 26.
+ Alice và Bob gửi public key của họ cho nhau (key exchange)
+ Alice và Bob sẽ sử dụng private key của mình và public key của đối phương để tính ra **shared secret key** theo công thức secret key = ${public-key}^{private-key}$  mod p. Như ví dụ trên, Alice sẽ tính K = $B^{a}$ mod p = $26^{13}$ mod 29 = 10. Bob sẽ tính K = $A^b$ mod p = $19^{15}$ mod 29 = 10. Ở đây K = 10 sẽ là secret key.
+ 2 bên sẽ sử dụng secret key này để trao đổi thông tin qua Symmetric Encryption(Mã hóa đối xứng)
+ Chứng minh : Vì public key = $g^{PrivateKeyOfMe}$ mod p => K = $PublicKeyOfOther^{PrivateKeyOfMe}$%p=${(g^{PrivateKeyOfOther}})^{PrivateKeyOfMe}$%p=$g^{PrivateKeyOfMe*PrivateKeyOfOther}$%p
+ Dù biết p,g,public key của cả 2 bên nhưng khó có thể tìm được secret key nếu không có private key nếu p đủ lớn. Nhưng nếu kẻ tấn công biết private key của 1 bên, hắn sẽ sử dụng public key của bên còn lại và áp dụng công thức và tính ra được K.
+ Để tìm được private key, hacker cần giải bài toán tìm a trong phương trình A = $g^a$ mod p với A là public key, p là 1 số nguyên tố lớn, g là 1 phần tử sinh của p. Vì g là phần tử sinh của p nên tương ứng với mỗi kết quả của phép tính $g^a$ mod p thì tương ứng với 1 phần tử a khác nhau. Để đoán được chỉ còn cách brute-force thử từng a một.

### SSH

#### Authenticating the Server
+  Khi sử dụng SSH để kết nối với một máy chủ, bạn sẽ thấy một thông báo xác nhận hỏi liệu bạn có tin tưởng vào máy chủ đó hay không.
- Điều này xảy ra vì SSH không nhận ra khóa công khai của máy chủ và muốn bạn xác nhận danh tính của nó.
- **Ví dụ**: Khi nhập lệnh `ssh 10.10.244.173`, bạn sẽ thấy
    `The authenticity of host '10.10.244.173' can't be established. ED25519 key fingerprint is SHA256:... Are you sure you want to continue connecting (yes/no/[fingerprint])?`
    
- Nếu bạn chọn **"yes"**, khóa công khai của máy chủ sẽ được lưu vào tệp `known_hosts`, giúp bạn không cần xác nhận lại trong tương lai.
- Cảnh báo này giúp ngăn chặn **tấn công man-in-the-middle (MITM)**, trong đó kẻ tấn công có thể giả mạo máy chủ mục tiêu.

#### Authenticating the Client

+ Sau khi xác thực máy chủ, client cần chứng minh danh tính của mình đối với máy chủ
+ Cách sử dụng tài khoản và mật khẩu không an toàn cho lắm vì có thể brute-force
+ Có thể sử dụng SSH Key, gồm
	+ Public key : Lưu trên máy chủ từ trước
	+ Private key : Lưu trên máy client, dùng để xác minh danh tính
+ Lệnh `ssh-keygen` giúp tạo khóa SSH
+ 1 số thuật toán tạo khóa SSH : 
	+ DSA : Cũ, ít dùng
	+ RSA : phổ biến nhưng cần khóa dài
	+ ECDSA 
	+ Ed25519 : Tối ưu, được khuyến khích sử dụng
	+ 

### Digital Signature

+ Là phương thức xác định tính xác thực và tính toàn vẹn của 1 thông điệp hoặc tài liệu số. Sử dụng asymmetric crpytography, có thể tạo ra 1 chữ ký bằng private key, chữ ký này có thể xác minh thông qua public key.
+ Cách đơn giản nhất để tạo digital signature là mã hóa tài liệu bằng private key. Nếu ai muốn xác minh chữ ký này thì họ cần dùng public key để giải mã và kiểm tra nội dung có khớp hay không. Trong lúc truyền mã nếu có ai thay đổi nội dung tài liệu thì khi giải mã bằng public key, nó sẽ ra văn bản khác bản gốc
+ Bản gốc -> Mã hash -> Private key mã hóa -> gửi đi -> public key ra giải mã hash -> so 2 mã hash với nhau. 
+ Việc sử dụng mã hash sẽ đảm bảo tính bí mật, việc so 2 mã hash với nhau bảo đảm tính toàn vẹn và tính
+ Certificate : Máy chủ web sẽ lưu các certificate cho mỗi domain để chứng thực rằng nó uy tín ba

## PGP và GPG

+ `gpg --import <tên file key>` : nhập key
+ `gpg --decrypt <tên file cần giải mã>` :Giải mã file với key đã được import trước đó
+ 

## Hashing

### Hash Funtion

+ Là hàm mã hóa không thể giải mã được hoặc để giải mã cần rất nhiều thời gian
+ `<tên thuật toán>sum tên file` : in ra nội dung file khi đã được băm bằng thuật toán chỉ định
### Hash Collision
+ Là thuật ngữ chỉ khi 2 đầu vào khác nhau cho ra cùng 1 đầu ra nếu lượng đầu vào quá lớn so với đầu ra.
+ MD5 và SHA1 xử lí va chạm không tốt lắm
### Lưu trữ mật khẩu an toàn

+ Sẽ có 1 thuật toán hash mật khẩu của người dùng và lưu giá trị hash ở máy chủ
+ Nếu nhiều mật khẩu giống nhau thì mã hash giống nhau=> nếu hacker tìm được mật khẩu của 1 tkhoan thì sẽ kiểm soát được các tài khoản khác bằng cách tạo ra 1 rainbow table là 1 map để tra cứu với mỗi mã hash thì mật khẩu nếu đã từng được tìm thấy sẽ là gì
+ Tool rainbow table(tra cứu password dựa theo mã băm) : [CrackStation.](https://crackstation.net/) [Decrypt](https://hashes.com/en/decrypt/hash)

### Mật khẩu trong linux

+ Trong linux mật khẩu đc lưu trong tệp /etc/shadow và chỉ tài khoản root mới có quyền đọc. 
+ Tệp này gồm 9 fields, cách bởi dấu `:`. 2 fields đầu tiên là username và password đã được mã hóa(tìm hiểu các fields còn lại dùng lệnh `man 5 shadow`)
+ Fields mật khẩu đã mã hóa chứa 4 thành phần cách nhau bởi $ có dạng : `$prefix$options$salt$hash` 
	+ prefix : giúp nhận dạng thuật toán băm được dùng
	+ options : tham số
	+ salt : mã salt được trộn vào mật khẩu trước khi hash
	+ hash : mật khẩu sau khi đc hash

### Crack Password

`hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`
- `-m <hash_type>` specifies the hash-type in numeric format. For example, `-m 1000` is for NTLM. Check the official documentation (`man hashcat`) and [example page](https://hashcat.net/wiki/doku.php?id=example_hashes) to find the hash type code to use.
- `-a <attack_mode>` specifies the attack-mode. For example, `-a 0` is for straight, i.e., trying one password from the wordlist after the other.
- `hashfile` is the file containing the hash you want to crack.
- `wordlist` is the security word list you want to use in your attack.

### Kiểm tra tính toàn vẹn

+ **HMAC** (Keyed-Hash Message Authentication Code) là một dạng mã xác thực thông điệp (MAC) sử dụng hàm băm mật mã kết hợp với một khóa bí mật để xác minh tính xác thực và tính toàn vẹn của dữ liệu.

+ Một HMAC giúp đảm bảo rằng người tạo ra HMAC chính là người họ khẳng định (tức là tính xác thực được xác nhận) và chứng minh rằng thông điệp không bị chỉnh sửa hoặc hỏng hóc (tức là tính toàn vẹn được duy trì). Điều này được thực hiện thông qua việc sử dụng khóa bí mật để chứng minh tính xác thực và một thuật toán băm để tạo ra giá trị băm nhằm chứng minh tính toàn vẹn.
Các bước dưới đây sẽ cho bạn một ý tưởng cơ bản về cách HMAC hoạt động:

1. **Đệm khóa bí mật:** Khóa bí mật được đệm (pad) đến kích thước khối của hàm băm.
2. **XOR khóa đệm với hằng số:** Khóa đã đệm được thực hiện phép XOR với một hằng số (thường là một khối các số 0 hoặc số 1).
3. **Băm thông điệp:** Thông điệp được băm bằng cách sử dụng hàm băm cùng với khóa đã được XOR.
4. **Băm lại kết quả:** Kết quả từ bước 3 được băm lại bằng cùng một hàm băm, nhưng lần này sử dụng khóa đã đệm được XOR với một hằng số khác.
5. **Giá trị HMAC cuối cùng:** Kết quả cuối cùng là giá trị HMAC, thường là một chuỗi có kích thước cố định.

![[Pasted image 20250220182505.png]]
+ HMAC(K,M) = H((K xor opad) || H(K xor ipad) || M)
	+ K : key
	+ M : Message