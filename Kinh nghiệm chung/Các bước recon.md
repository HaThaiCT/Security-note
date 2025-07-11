
# Recon flow

Domain -> Subdomain -> IP -> 
+ OS
+ Port/ Service -> Web -> 
	+ Tech stack
	+ Directories scan
	+ Parameters scan


# Domain/Subdomain
## Amass 
Link: https://github.com/OWASP/Amass
Để sửdụng Amass, ta dùng lệnh: `amass enum -d <hostname>`

# Tìm IP/ dãy IP

Bước tiếp theo khi ta đã recon được subdomain của target, ta cần tìm thêm IP/Dãy đểcó thêm nhiều attack surface.
- Đểt ìm IP của ứng dụng thì có nhiều cách và 1 cách đơn giản nhất là sử dụng một lệnh có sẵn trên Windows/Linux đó là lệnh nslookup
- Cách sử dụng lệnh này rất đơn giản: `nslookup <domain name>`

# Tìm OS/Port/Service

## Nmap

Các option
+ Scan speed: `-T0 -> -T5`
+ Port range: `-p1-65635`
+ Service version detection: `-sV`
+ OS detection: `-O`
+ Service version detection, OS detection, script scanning, and traceroute: `-A`
Nên sử dụng nmap dưới quyền root để công cụ hoạt động hiệu quả nhất

# Tech stack

Sử dụng Extension Wappalyzer để biết Tech stack của web

# Directories scan

Có 3 cách thu thập endpoints
+ Manual : bằng tay
+ Find: Tìm trong source code của web
+ Discovery: Brute force

## Katana 
Link: [projectdiscovery/katana: A next-generation crawling and spidering framework.](https://github.com/projectdiscovery/katana)
Chức năng: crawl website để tìm ra các endpoints
`katana -u <URL>` : quét URL
## fuff
Link : [ffuf/ffuf: Fast web fuzzer written in Go](https://github.com/ffuf/ffuf)
Dùng để fuzzing hoặc brute force
`-ac` : chế độ auto calibration sẽ tự động điều chỉnh việc filter các request
`-H` : có thể thêm các header tùy chỉnh vào request
`Filter (-fc, -fs)` : filter các kết quả trả về (fs là lọc bỏ, mc là lọc lấy)
Ví dụ ```ffuf -w /path/to/wordlist -u https://target/FUZZ```
=> Sẽ trả về tất cả các response => có thể dùng filter lọc ra các response hợp lệ

## Parameter scan

## Arjun
Dùng để brute force các parameter trong GET,POST
Có sẵn wordlist thông dụng
Link : [s0md3v/Arjun: HTTP parameter discovery suite.](https://github.com/s0md3v/Arjun)
Cách tải: `pipx install arjun`
Cách dùng `arjun -u <target_url>`



# Một số nguồn khác

Recon qua certificate
+ [crt.sh | Certificate Search](https://crt.sh/)
Wayback machine để xem các phiên bản của domain
+ [Wayback Machine](https://web.archive.org/)
Word list thông dụng
+ https://github.com/danielmiessler/SecLists
Một số công cụ khác
+ jaeles : https://github.com/jaeles-project/jaeles
+ git-dumper : https://github.com/arthaud/git-dumper
+ 