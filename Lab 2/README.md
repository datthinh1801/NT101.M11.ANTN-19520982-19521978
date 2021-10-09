# Lab 2: Information Gathering
## Câu 1
### Question
Từ trang web của MegaCorp One, hãy mô tả một chút về lĩnh vực hoạt động của công ty?

### Answer
Nanotechnology và các tiêu chuẩn trong các lĩnh vực dược học, điện tử, thương mại.  
![image](https://user-images.githubusercontent.com/44528004/136151242-da157a61-b180-499c-b85e-30e03008fd03.png)

## Câu 2
### Question
Hãy liệt kê những thành viên đang làm việc cho MegaCorp One và một vài thông tin về những thành viên đó (địa chỉ email, chức vụ, tài khoản mạng xã hội)?

### Answer
![image](https://user-images.githubusercontent.com/44528004/136160316-3a552c62-31c4-45ee-ad74-210976bba7cf.png)

## Câu 3
### Question
Khi có được địa chỉ Email của các thành viên thuộc tổ chức, bạn có phát hiện ra được điều gì?

### Answer
Từ các email trên ta thấy chúng đều có điểm chung là `<name>@<company-mail-domain>`. Vậy giả sử ta biết có 1 nhân viên của Megacorp One tên là Tim, ta có thể đoán được email của anh ấy là `tim@megacorpone.com`.

## Câu 4
### Question
Sử dụng công cụ whois để xác định các name server của MegaCorp One.

### Answer
![image](https://user-images.githubusercontent.com/44528004/136161707-19b4896d-3ecc-4064-8c6b-b6df21e16bf3.png)


## Câu 5
### Question
Sử dụng công cụ whois để tìm kiếm các thông tin của trường Đại học Công nghệ Thông tin (`uit.edu.vn`) có được không? Giải thích?

### Answer
Khi chạy thử `whois` thì ta có kết quả sau:
```
┌──(kali㉿kali)-[~]
└─$ whois uit.edu.vn     
This TLD has no whois server, but you can access the whois database at
http://www.vnnic.vn/en
```

Từ kết quả trên cũng như [issue](https://github.com/weppos/whois/issues/346) của tool `whois` trên github, ta biết được là VN TLD không có whois server. Do đó ta không thể trích xuất thông tin từ `whois` được.  

Vậy để trích xuất được thông tin của `uit.edu.vn`, ta có thể vào trang web www.vnnic.vn để tra cứu.  
![image](https://user-images.githubusercontent.com/44528004/136162610-82afa2c9-32cd-4548-a26b-45a68460d62b.png)

## Câu 6
### Question
Thu thập thông tin về tên miền uit.edu.vn và hãy cho biết các thông tin như:  
 a. Ngày đăng ký tên miền  
 b. Ngày hết hạn tên miền  
 c. Chủ sở hữu tên miền  
 d. Các name server của tên miền
 
### Answer
Từ kết quả tra cứu ở câu trên:  
a. Ngày đăng ký tên miền (Creation date): 02/10/2006  
b. Ngày hết hạn tên miền (Expiration date): 02/10/2022  
c. Chủ sở hữu tên miền: Công ty TNHH PA Việt Nam  
d. Các name server: `ns1.pavietnam.vn`, `ns2.pavietnam.vn`, `nsbak.pavietnam.net`.

## Câu 7
### Question
Ai là Phó chủ tịch Pháp lý (Vice President of Legal) của MegaCorp One và địa chỉ email của họ là gì?

### Answer
![image](https://user-images.githubusercontent.com/44528004/136157199-bb9b82c6-e3a4-4519-9277-d681d9dfa749.png)  

![image](https://user-images.githubusercontent.com/44528004/136157219-cf7f4205-b9ee-4e0c-b20c-41fabe5d7ffd.png)

## Câu 8
### Question
Bạn có thể tìm kiếm thêm các nhân viên khác của MegaCorp One mà không được liệt kê trên trang web www.megacorpone.com?

### Answer
Khi ta sử dụng dork `intext:name`, ta sẽ search các trang của `www.megacorpone.com` có name, bao gồm cả trang contact.  
![image](https://user-images.githubusercontent.com/44528004/136164482-e9292dea-4233-47ed-bb7f-63b3183176c2.png)  

Bên cạnh đó, nếu 1 trang web nào đó có đăng hình nhân viên thì ta cũng có thể thấy được mặt của họ.  
![image](https://user-images.githubusercontent.com/44528004/136164765-bceae327-2362-40f3-a6cd-5faccd9aba01.png)

## Câu 9
### Question
Liệt kê một vài từ khóa thường gặp trên Google và cho ví dụ? (Yêu cầu: ít nhất 5 từ khóa)

### Answer
| Keyword | Example |
|---|---|
| `site` | `site:megacorpone.com` |
| `inurl` | `inurl:uit` |
| `intitle` | `intitle:contact` |
| `filetype` | `filetype:pdf` |
| `intext` | `intext:passwd` |

## Câu 10
### Question
Thực hiện tìm kiếm các tài liệu thú vị của Trường Đại học Công nghệ Thông tin mà được công bố trên Internet mà theo bạn là không nên được công bố?

### Answer


## Câu 11
### Question
Sử dụng Netcraft để xác định máy chủ ứng dụng (application server) đang chạy trên www.megacorpone.com.

### Answer
![image](https://user-images.githubusercontent.com/44528004/136158113-227712a9-61a0-4af3-b016-bb615ba9a1ed.png)

## Câu 12
### Question
Thực hiện sử dụng module có thể giúp phân giải tên miền từ `show hosts` thành địa chỉ IP tương ứng.

### Answer
Từ các `hosts` sau khi chạy `netcraft` module sau:  

![image](https://user-images.githubusercontent.com/44528004/136660937-fbfce59f-3510-4880-b73c-1f9378bd94f8.png)


![image](https://user-images.githubusercontent.com/44528004/136660873-dbe741c4-e13b-4f20-99de-006a79b3bceb.png)

Ta có thể phân giải tên miền bằng cách sử dụng module `recon/hosts-hosts/resolve`.  

![image](https://user-images.githubusercontent.com/44528004/136660945-4d26d4da-91e1-4818-bf4c-34a81633764c.png)
> Để có thể sử dụng module này, từ module `netcraft`, ta dùng lệnh `back` và sau đó load module `resolve` và `run` như thông thường.

## Câu 15
### Question
Thực hiện tìm kiếm các lệnh khác trên Shodan mà có thể tiết lộ thêm nhiều thông tin thú vị về một đối tượng bất kỳ.

### Answer
Sử dụng filters:
| Filter | Ý nghĩa |
|---|---|
| city | Dùng để tìm thiết bị tại một thành phố nào đó |
| country | Dùng để tìm thiết bị tại một quốc gia nào đó |
| geo | Dùng cho tọa độ |
| hostname | Tìm theo hostname |
| net | Tìm theo địa chỉ IP |
| os | Tìm theo hệ điều hành |
| `+` hoặc `-` | `AND` hoặc `NOT` một filter nào đó |
| port | Tìm theo port được mở |
| before/after | Tìm theo thời gian |

## Câu 16
### Question
So sánh kết quả tìm kiếm trên Shodan so với các search engine khác như Google, Bing, ...

### Answer
| | Shodan | Các search engine khác |
|---|---|---|
| Kết quả tìm kiếm thông thường | Thiết bị (camera, router, webcames, servers, printers ...) | Nội dung (file, đoạn text, url, ...) |
| Về tìm kiếm dịch vụ | Kết quả là các dịch vụ (như VPN, VNC, ...) bị rò rỉ kèm theo các thông tin có liên quan đế dịch vụ mà ta có thể truy cập được. | Kết quả là các sản phẩm liên quan đên dịch vụ (ứng dụng để chạy dịch vụ, document, ...). |
| So sánh với Google Dorks | Mặc định là tìm kiếm thiết bị và dịch vụ bị rò rỉ. | Ta có thể tận dụng google dork để đạt được kết quả tương tự nhưng đòi hỏi sử dụng các keywords như `intitle`, `allintext`, ... .|


## Câu 17
### Question
Sử dụng công cụ theHarvester để lấy tìm kiếm các địa chỉ email của UIT.

### Answer
![image](https://user-images.githubusercontent.com/44528004/136160112-8cc3f728-b626-4582-83d3-303b85fd6666.png)  

## Câu 18
### Question
Sử dụng với nguồn tìm kiếm khác (-b). Theo bạn, kết quả của nguồn nào tốt hơn?

### Answer
#### Bing
![image](https://user-images.githubusercontent.com/44528004/136662925-cb9dc1ae-04a4-4418-ae57-2328acd85963.png)


#### Google
![image](https://user-images.githubusercontent.com/44528004/136662950-ac022547-dffd-4a4f-bccf-6fd076dbf6e7.png)

#### Baidu
![image](https://user-images.githubusercontent.com/44528004/136662971-6155af1c-08f5-4a7e-87ae-26892edd93b1.png)

#### DuckDuckGo
![image](https://user-images.githubusercontent.com/44528004/136663005-e9a24dda-001c-43b5-8564-56334b71d77d.png)

> Từ một số ví dụ trên, ta có thể thấy là Google tốt hơn.

## Câu 19
### Question
Thực hiện tìm kiếm các địa chỉ Email của MegaCorp One sử dụng Maltego.

### Answer

## Câu 20
### Question
Sử dụng công cụ Maltego cho UIT (tên miền: `uit.edu.vn`) và trả lời các câu hỏi sau:
a. Các bản ghi DNS.
b. Các website và địa chỉ IP tương ứng.

### Answer

câu a: Các bản ghi dns (ns,nx,soa,spf...):

![image](https://user-images.githubusercontent.com/31529599/136162461-af90926d-2b9e-4f6c-b76b-d423079fef00.png)


câu b: Các website và địa chỉ IP tương ứng: 

![image](https://user-images.githubusercontent.com/31529599/136167270-fa4fcfd0-6643-42b7-b43e-adb1764ac1cc.png)

## Câu 21
### Question
Ngoài các bản ghi kể trên, hãy liệt kê các bản ghi khác của DNS.

### Answer
Ngoài NS, A, MX, PTR, CNAME, TXT, còn có các bản ghi khác như AAAA, SOA, SRV, AFSDB, APL, CAA, DNSKEY, CDNSKEY, CERT, DCHID, DNAME, HIP, IPSECKEY, LOC, NAPTR, NSEC, RRSIG, RP, và SSHFP.
> https://www.cloudflare.com/learning/dns/dns-records/

## Câu 35: Sử dụng thêm 2 NSE script (tự chọn) để quét máy mục tiêu (Metasploitable 2)

### Anwser

Script: `qscan`

```bash
└─$ sudo nmap 192.168.21.137 --script=qscan
[sudo] password for kali: 
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-06 04:35 EDT
Nmap scan report for 192.168.21.137
Host is up (0.0018s latency).
Not shown: 977 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 00:0C:29:FA:DD:2A (VMware)

Host script results:
| qscan: 
| PORT  FAMILY  MEAN (us)  STDDEV  LOSS (%)
| 1     0       748.70     303.84  0.0%
| 21    1       528.10     67.39   0.0%
| 22    0       723.30     476.66  0.0%
| 23    0       775.50     408.16  0.0%
| 25    0       794.50     538.23  0.0%
| 53    0       586.90     146.47  0.0%
| 80    0       758.70     244.58  0.0%
| 111   0       665.90     404.18  0.0%
|_139   0       711.70     199.32  0.0%

Nmap done: 1 IP address (1 host up) scanned in 33.75 seconds

```

Script: `ssl-cert`

```bash
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-06 04:38 EDT
Nmap scan report for 192.168.21.137
Host is up (0.0018s latency).
Not shown: 977 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  domain
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2049/tcp open  nfs
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 00:0C:29:FA:DD:2A (VMware)

Nmap done: 1 IP address (1 host up) scanned in 90.24 seconds

```
