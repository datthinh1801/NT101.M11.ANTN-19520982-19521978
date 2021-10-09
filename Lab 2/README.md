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


## Câu 22
### Question
Sử dụng lệnh `host` để tìm kiếm các bản ghi TXT, MX cho tên miền `uit.edu.vn`.

### Answer
```
└─$ host -t txt uit.edu.vn     
uit.edu.vn descriptive text "v=spf1 include:_spf.google.com ~all"
uit.edu.vn descriptive text "google-site-verification=wjArKGa37oHK083XqT2C91tPny8NLttGS0aU5pJjKiY"
uit.edu.vn descriptive text "MS=E431E3CA3EFF5A6431E2378C924984A8A0334ABC"
```

```
└─$ host -t mx uit.edu.vn
uit.edu.vn mail is handled by 20 alt2.aspmx.l.google.com.
uit.edu.vn mail is handled by 40 aspmx3.googlemail.com.
uit.edu.vn mail is handled by 20 alt1.aspmx.l.google.com.
uit.edu.vn mail is handled by 40 aspmx2.googlemail.com.
uit.edu.vn mail is handled by 10 aspmx.l.google.com.
```                                                        

## Câu 23
### Question
Sử dụng lệnh `host` cho các hostname không tồn tại trong tên miền `uit.edu.vn` (idontexist, noexist, baithuchanhso2). Có nhận xét gì về kết quả trả về hay không? Giải thích?

### Answer
![image](https://user-images.githubusercontent.com/44528004/136663473-ab44524e-0cfa-4a6b-9d77-ad408ad8ba88.png)

Từ kết quả trên, ta thấy răng các địa chỉ IP trả về đều giống nhau. Lí dó là vì cấu hình DNS của `uit.edu.vn` có sử dụng wildcard `*` nên nếu 1 DNS query nào đó không có hostname tương ứng thì sẽ được match với wildcard `*` và trả về cùng 1 địa chỉ IP.

## Câu 24
### Question
Sử dụng wordlist thông dụng khác (rockyou, seclists) để tìm kiếm các hostname hợp lệ khác của megacorpone.com.

### Answer
```
└─$ for name in $(cat /usr/share/seclists/Discovery/DNS/namelist.txt ); do host $name.megacorpone.com;done | grep -v "not found"
admin.megacorpone.com has address 51.222.169.208
beta.megacorpone.com has address 51.222.169.209
intranet.megacorpone.com has address 51.222.169.211
mail.megacorpone.com has address 51.222.169.212
mail2.megacorpone.com has address 51.222.169.213
ns1.megacorpone.com has address 51.79.37.18
ns2.megacorpone.com has address 51.222.39.63
ns3.megacorpone.com has address 66.70.207.180
router.megacorpone.com has address 51.222.169.214
snmp.megacorpone.com has address 51.222.169.216
support.megacorpone.com has address 51.222.169.218
syslog.megacorpone.com has address 51.222.169.217
test.megacorpone.com has address 51.222.169.219
vpn.megacorpone.com has address 51.222.169.220
www.megacorpone.com has address 149.56.244.87
www2.megacorpone.com has address 149.56.244.87
```

## Câu 25
### Question
Viết một chương trình Bash script để liệt kê danh sách các nameserver của các đơn vị thành viên thuộc Đại học Quốc Gia TP.HCM (hcmus.edu.vn, hcmussh.edu.vn, uit.edu.vn, hcmut.edu.vn, hcmiu.edu.vn, uel.edu.vn, hcmier.edu.vn, vnuhcm.edu.vn) và thực hiện zone transfer ứng với các nameserver đã tìm được.

### Answer
Script:
```bash
#! /bin/bash
domains=("hcmus.edu.vn" "hcmussh.edu.vn" "uit.edu.vn" "hcmut.edu.vn" "uel.edu.vn" "hcmier.edu.vn" "vnuhcm.edu.vn" "agu.edu.vn")

for domain in ${domains[@]}; do
        echo "# Domain: $domain"
        for nameServer in `host -t ns $domain 2> /dev/null | cut -d " " -f 4`; do
                echo "## Nameserver: $nameServer"
                echo "### Transferring zone..."
                host -l $domain $nameServer 2> /dev/null
                echo
                echo "---------------------------------------------------------"
        done
        echo
        echo "################################################################"
        echo
done
```

Kết quả chạy:
```
└─$ ./dns_digger.sh  
# Domain: hcmus.edu.vn
## Nameserver: server.hcmus.edu.vn.
### Transferring zone...
Using domain server:
Name: server.hcmus.edu.vn.
Address: 171.244.202.180#53
Aliases: 

Host hcmus.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: dns2.hcmus.edu.vn.
### Transferring zone...
;; Connection to 115.73.217.121#53(115.73.217.121) for hcmus.edu.vn failed: timed out.
;; connection timed out; no servers could be reached

;; Connection to 115.73.217.121#53(115.73.217.121) for hcmus.edu.vn failed: timed out.

---------------------------------------------------------
## Nameserver: dns1.hcmus.edu.vn.
### Transferring zone...
;; Connection to 14.241.254.131#53(14.241.254.131) for hcmus.edu.vn failed: timed out.
;; connection timed out; no servers could be reached

;; Connection to 14.241.254.131#53(14.241.254.131) for hcmus.edu.vn failed: timed out.

---------------------------------------------------------

################################################################

# Domain: hcmussh.edu.vn
## Nameserver: server.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: server.vnuhcm.edu.vn.
Address: 103.88.121.201#53
Aliases: 

Host hcmussh.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: vnuserv.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: vnuserv.vnuhcm.edu.vn.
Address: 103.88.121.200#53
Aliases: 

Host hcmussh.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------

################################################################

# Domain: uit.edu.vn
## Nameserver: nsbak.pavietnam.net.
### Transferring zone...
Using domain server:
Name: nsbak.pavietnam.net.
Address: 112.213.89.22#53
Aliases: 

Host uit.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: ns1.pavietnam.vn.
### Transferring zone...
Using domain server:
Name: ns1.pavietnam.vn.
Address: 112.213.89.3#53
Aliases: 

Host uit.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: ns2.pavietnam.vn.
### Transferring zone...
Using domain server:
Name: ns2.pavietnam.vn.
Address: 222.255.121.247#53
Aliases: 

Host uit.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------

################################################################

# Domain: hcmut.edu.vn
## Nameserver: dns4.hcmut.edu.vn.
### Transferring zone...
Using domain server:
Name: dns4.hcmut.edu.vn.
Address: 203.205.32.236#53
Aliases: 

hcmut.edu.vn name server dns1.hcmut.edu.vn.
hcmut.edu.vn name server dns2.hcmut.edu.vn.
hcmut.edu.vn name server dns3.hcmut.edu.vn.
hcmut.edu.vn name server dns4.hcmut.edu.vn.
hcmut.edu.vn has address 221.133.13.114
60.hcmut.edu.vn has address 112.213.89.2
aao.hcmut.edu.vn has address 221.133.13.122
apps.aao.hcmut.edu.vn has address 221.133.13.124
server.aao.hcmut.edu.vn has address 221.133.13.122
actbk.hcmut.edu.vn has address 221.133.13.127
alumni.hcmut.edu.vn has address 221.133.13.109
amis.hcmut.edu.vn has address 221.133.13.106
bkiot.hcmut.edu.vn has address 210.211.113.130
bkpay.hcmut.edu.vn has address 221.133.13.124
bksi.hcmut.edu.vn has address 221.133.13.118
bkyst.hcmut.edu.vn has address 45.119.83.20
bridge.hcmut.edu.vn has address 113.176.61.107
bridge2.hcmut.edu.vn has address 123.30.157.251
carerescif.hcmut.edu.vn has address 112.213.89.145
www.carerescif.hcmut.edu.vn has address 112.213.89.145
casdev-master.hcmut.edu.vn has address 221.133.13.105
cc.hcmut.edu.vn has address 112.78.1.105
cce.hcmut.edu.vn has address 112.78.1.105
conferences.hcmut.edu.vn has address 221.133.13.111
www.conferences.hcmut.edu.vn has address 221.133.13.111
cse.hcmut.edu.vn has address 221.133.13.113
60.cse.hcmut.edu.vn has address 61.28.227.157
doanhoi.cse.hcmut.edu.vn has address 45.119.83.33
elearning.cse.hcmut.edu.vn has address 221.133.13.110
internship.cse.hcmut.edu.vn has address 221.133.13.108
server.cse.hcmut.edu.vn has address 221.133.13.113
vre.cse.hcmut.edu.vn has address 103.88.121.151
ctct.hcmut.edu.vn has address 125.212.245.195
dcselab.hcmut.edu.vn has address 221.132.37.37
demo.hcmut.edu.vn has address 221.133.13.105
diemthi.hcmut.edu.vn has address 221.133.13.122
diemthi.hcmut.edu.vn has address 103.88.121.145
diemthi.hcmut.edu.vn has address 115.78.0.48
dkmh.hcmut.edu.vn has address 221.133.13.124
dls.hcmut.edu.vn has address 103.88.121.156
dns1.hcmut.edu.vn has address 221.133.13.114
dns2.hcmut.edu.vn has address 221.133.13.115
dns3.hcmut.edu.vn has address 203.205.32.235
dns4.hcmut.edu.vn has address 203.205.32.236
dae.dte.hcmut.edu.vn has address 171.244.43.27
www.dae.dte.hcmut.edu.vn has address 171.244.43.27
e-learning.hcmut.edu.vn has address 221.133.13.123
elearning-cse.hcmut.edu.vn has address 221.133.13.107
fdse2017.hcmut.edu.vn has address 61.28.227.157
fe.hcmut.edu.vn has address 52.74.151.191
fenr.hcmut.edu.vn has address 112.213.89.145
www.fenr.hcmut.edu.vn has address 112.213.89.145
hre.fme.hcmut.edu.vn has address 125.212.209.56
ise.fme.hcmut.edu.vn has address 103.48.81.8
gateway01.hcmut.edu.vn has address 14.241.245.110
gateway02.hcmut.edu.vn has address 221.133.12.6
gateway2.hcmut.edu.vn has address 113.161.83.117
gpu02.hcmut.edu.vn has address 103.88.121.152
gpu11.hcmut.edu.vn has address 103.88.121.150
grad.hcmut.edu.vn has address 221.133.13.127
graylog.hcmut.edu.vn has address 221.133.13.115
gtsw2019.hcmut.edu.vn has address 166.62.28.82
www.gtsw2019.hcmut.edu.vn has address 166.62.28.82
hnkhcn2013.hcmut.edu.vn has address 112.213.89.149
hpcc.hcmut.edu.vn has address 203.205.33.134
hpccbk.hcmut.edu.vn has address 116.118.106.108
hpccportal.hcmut.edu.vn has address 203.205.33.134
hpclab.hcmut.edu.vn has address 103.88.121.154
icse.hcmut.edu.vn has address 103.18.6.44
www.icse.hcmut.edu.vn has address 103.18.6.44
imp.hcmut.edu.vn has address 103.221.220.25
www.imp.hcmut.edu.vn has address 103.221.220.25
impactmap.hcmut.edu.vn has address 61.28.227.157
iot.hcmut.edu.vn has address 61.28.227.157
iotlab.hcmut.edu.vn has address 210.211.113.130
iro.hcmut.edu.vn has address 112.213.89.46
www.iro.hcmut.edu.vn has address 112.213.89.46
it.hcmut.edu.vn has address 103.88.121.162
tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
www.tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
ktx.hcmut.edu.vn has address 203.205.32.235
opac.lib.hcmut.edu.vn has address 103.88.121.159
portal.lib.hcmut.edu.vn has address 221.133.13.104
server.lib.hcmut.edu.vn has address 112.213.85.46
lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
www.lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
log.hcmut.edu.vn has address 221.133.13.108
logserver.hcmut.edu.vn has address 221.133.13.108
meet.hcmut.edu.vn has address 14.241.245.187
meganet.hcmut.edu.vn has address 10.128.0.1
meganet-gateway.hcmut.edu.vn has address 14.169.141.126
meganet-gateway2.hcmut.edu.vn has address 14.169.17.32
meganet02.hcmut.edu.vn has address 10.130.0.1
meganet2.hcmut.edu.vn has address 10.228.0.1
membrane2014.hcmut.edu.vn has address 112.213.89.144
mining.hcmut.edu.vn has address 103.88.121.145
mybk.hcmut.edu.vn has address 221.133.13.124
netdata.hcmut.edu.vn has address 221.133.13.116
ntop.hcmut.edu.vn has address 221.133.13.115
oisp.hcmut.edu.vn has address 103.90.220.204
sinhvien.oisp.hcmut.edu.vn has address 221.132.17.180
personel.hcmut.edu.vn has address 221.133.13.127
pgs.hcmut.edu.vn has address 221.133.13.112
portal.hcmut.edu.vn has address 221.133.13.108
private01.hcmut.edu.vn has address 10.130.0.1
private6.hcmut.edu.vn has address 10.228.0.1
pssp.hcmut.edu.vn has address 221.133.13.105
public.hcmut.edu.vn has address 172.28.232.1
public2.hcmut.edu.vn has address 10.28.232.1
qlns.hcmut.edu.vn has address 221.133.13.108
radius01.hcmut.edu.vn has address 221.133.12.6
radius1.hcmut.edu.vn has address 221.133.12.6
recsys.hcmut.edu.vn has address 221.133.13.106
rsce2016.hcmut.edu.vn has address 103.227.177.226
sc.hcmut.edu.vn has address 221.133.13.121
scc.hcmut.edu.vn has address 61.28.227.157
server02.hcmut.edu.vn has address 221.133.13.115
server03.hcmut.edu.vn has address 203.205.32.236
server04.hcmut.edu.vn has address 221.133.13.114
server05.hcmut.edu.vn has address 221.133.13.116
server06.hcmut.edu.vn has address 203.205.32.235
server07.hcmut.edu.vn has address 221.133.13.117
server09.hcmut.edu.vn has address 203.205.32.235
server11.hcmut.edu.vn has address 221.133.13.117
server12.hcmut.edu.vn has address 221.133.13.118
server14.hcmut.edu.vn has address 221.133.13.108
server15.hcmut.edu.vn has address 221.133.13.115
server236.hcmut.edu.vn has address 221.133.13.110
server30.hcmut.edu.vn has address 221.133.13.121
server80.hcmut.edu.vn has address 221.133.13.119
server89.hcmut.edu.vn has address 221.133.13.120
shms.hcmut.edu.vn has address 221.133.13.111
sso.hcmut.edu.vn has address 221.133.13.120
sso-net.hcmut.edu.vn has address 221.133.13.111
sso-net2.hcmut.edu.vn has address 221.133.13.111
test.hcmut.edu.vn has address 221.133.13.108
traffic.hcmut.edu.vn has address 103.88.121.161
tris.hcmut.edu.vn has address 14.161.5.98
tuyensinh.hcmut.edu.vn has address 221.133.13.124
tv-cam01.hcmut.edu.vn has address 221.133.13.114
tv-cam02.hcmut.edu.vn has address 221.133.13.115
tv-cam03.hcmut.edu.vn has address 113.161.83.117
uiseminar2017.hcmut.edu.vn has address 198.252.111.243
www.uiseminar2017.hcmut.edu.vn has address 198.252.111.243
vre.hcmut.edu.vn has address 103.88.121.151
wifi-controller.hcmut.edu.vn has address 221.133.13.110
wifi-cse.hcmut.edu.vn has address 172.28.211.1
wiki.hcmut.edu.vn has address 221.133.13.124

---------------------------------------------------------
## Nameserver: dns2.hcmut.edu.vn.
### Transferring zone...
Using domain server:
Name: dns2.hcmut.edu.vn.
Address: 221.133.13.115#53
Aliases: 

hcmut.edu.vn name server dns1.hcmut.edu.vn.
hcmut.edu.vn name server dns2.hcmut.edu.vn.
hcmut.edu.vn name server dns3.hcmut.edu.vn.
hcmut.edu.vn name server dns4.hcmut.edu.vn.
hcmut.edu.vn has address 221.133.13.114
60.hcmut.edu.vn has address 112.213.89.2
aao.hcmut.edu.vn has address 221.133.13.122
apps.aao.hcmut.edu.vn has address 221.133.13.124
server.aao.hcmut.edu.vn has address 221.133.13.122
actbk.hcmut.edu.vn has address 221.133.13.127
alumni.hcmut.edu.vn has address 221.133.13.109
amis.hcmut.edu.vn has address 221.133.13.106
bkiot.hcmut.edu.vn has address 210.211.113.130
bkpay.hcmut.edu.vn has address 221.133.13.124
bksi.hcmut.edu.vn has address 221.133.13.118
bkyst.hcmut.edu.vn has address 45.119.83.20
bridge.hcmut.edu.vn has address 113.176.61.107
bridge2.hcmut.edu.vn has address 123.30.157.251
carerescif.hcmut.edu.vn has address 112.213.89.145
www.carerescif.hcmut.edu.vn has address 112.213.89.145
casdev-master.hcmut.edu.vn has address 221.133.13.105
cc.hcmut.edu.vn has address 112.78.1.105
cce.hcmut.edu.vn has address 112.78.1.105
conferences.hcmut.edu.vn has address 221.133.13.111
www.conferences.hcmut.edu.vn has address 221.133.13.111
cse.hcmut.edu.vn has address 221.133.13.113
60.cse.hcmut.edu.vn has address 61.28.227.157
doanhoi.cse.hcmut.edu.vn has address 45.119.83.33
elearning.cse.hcmut.edu.vn has address 221.133.13.110
internship.cse.hcmut.edu.vn has address 221.133.13.108
server.cse.hcmut.edu.vn has address 221.133.13.113
vre.cse.hcmut.edu.vn has address 103.88.121.151
ctct.hcmut.edu.vn has address 125.212.245.195
dcselab.hcmut.edu.vn has address 221.132.37.37
demo.hcmut.edu.vn has address 221.133.13.105
diemthi.hcmut.edu.vn has address 221.133.13.122
diemthi.hcmut.edu.vn has address 103.88.121.145
diemthi.hcmut.edu.vn has address 115.78.0.48
dkmh.hcmut.edu.vn has address 221.133.13.124
dls.hcmut.edu.vn has address 103.88.121.156
dns1.hcmut.edu.vn has address 221.133.13.114
dns2.hcmut.edu.vn has address 221.133.13.115
dns3.hcmut.edu.vn has address 203.205.32.235
dns4.hcmut.edu.vn has address 203.205.32.236
dae.dte.hcmut.edu.vn has address 171.244.43.27
www.dae.dte.hcmut.edu.vn has address 171.244.43.27
e-learning.hcmut.edu.vn has address 221.133.13.123
elearning-cse.hcmut.edu.vn has address 221.133.13.107
fdse2017.hcmut.edu.vn has address 61.28.227.157
fe.hcmut.edu.vn has address 52.74.151.191
fenr.hcmut.edu.vn has address 112.213.89.145
www.fenr.hcmut.edu.vn has address 112.213.89.145
hre.fme.hcmut.edu.vn has address 125.212.209.56
ise.fme.hcmut.edu.vn has address 103.48.81.8
gateway01.hcmut.edu.vn has address 14.241.245.110
gateway02.hcmut.edu.vn has address 221.133.12.6
gateway2.hcmut.edu.vn has address 113.161.83.117
gpu02.hcmut.edu.vn has address 103.88.121.152
gpu11.hcmut.edu.vn has address 103.88.121.150
grad.hcmut.edu.vn has address 221.133.13.127
graylog.hcmut.edu.vn has address 221.133.13.115
gtsw2019.hcmut.edu.vn has address 166.62.28.82
www.gtsw2019.hcmut.edu.vn has address 166.62.28.82
hnkhcn2013.hcmut.edu.vn has address 112.213.89.149
hpcc.hcmut.edu.vn has address 203.205.33.134
hpccbk.hcmut.edu.vn has address 116.118.106.108
hpccportal.hcmut.edu.vn has address 203.205.33.134
hpclab.hcmut.edu.vn has address 103.88.121.154
icse.hcmut.edu.vn has address 103.18.6.44
www.icse.hcmut.edu.vn has address 103.18.6.44
imp.hcmut.edu.vn has address 103.221.220.25
www.imp.hcmut.edu.vn has address 103.221.220.25
impactmap.hcmut.edu.vn has address 61.28.227.157
iot.hcmut.edu.vn has address 61.28.227.157
iotlab.hcmut.edu.vn has address 210.211.113.130
iro.hcmut.edu.vn has address 112.213.89.46
www.iro.hcmut.edu.vn has address 112.213.89.46
it.hcmut.edu.vn has address 103.88.121.162
tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
www.tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
ktx.hcmut.edu.vn has address 203.205.32.235
opac.lib.hcmut.edu.vn has address 103.88.121.159
portal.lib.hcmut.edu.vn has address 221.133.13.104
server.lib.hcmut.edu.vn has address 112.213.85.46
lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
www.lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
log.hcmut.edu.vn has address 221.133.13.108
logserver.hcmut.edu.vn has address 221.133.13.108
meet.hcmut.edu.vn has address 14.241.245.187
meganet.hcmut.edu.vn has address 10.128.0.1
meganet-gateway.hcmut.edu.vn has address 14.169.141.126
meganet-gateway2.hcmut.edu.vn has address 14.169.17.32
meganet02.hcmut.edu.vn has address 10.130.0.1
meganet2.hcmut.edu.vn has address 10.228.0.1
membrane2014.hcmut.edu.vn has address 112.213.89.144
mining.hcmut.edu.vn has address 103.88.121.145
mybk.hcmut.edu.vn has address 221.133.13.124
netdata.hcmut.edu.vn has address 221.133.13.116
ntop.hcmut.edu.vn has address 221.133.13.115
oisp.hcmut.edu.vn has address 103.90.220.204
sinhvien.oisp.hcmut.edu.vn has address 221.132.17.180
personel.hcmut.edu.vn has address 221.133.13.127
pgs.hcmut.edu.vn has address 221.133.13.112
portal.hcmut.edu.vn has address 221.133.13.108
private01.hcmut.edu.vn has address 10.130.0.1
private6.hcmut.edu.vn has address 10.228.0.1
pssp.hcmut.edu.vn has address 221.133.13.105
public.hcmut.edu.vn has address 172.28.232.1
public2.hcmut.edu.vn has address 10.28.232.1
qlns.hcmut.edu.vn has address 221.133.13.108
radius01.hcmut.edu.vn has address 221.133.12.6
radius1.hcmut.edu.vn has address 221.133.12.6
recsys.hcmut.edu.vn has address 221.133.13.106
rsce2016.hcmut.edu.vn has address 103.227.177.226
sc.hcmut.edu.vn has address 221.133.13.121
scc.hcmut.edu.vn has address 61.28.227.157
server02.hcmut.edu.vn has address 221.133.13.115
server03.hcmut.edu.vn has address 203.205.32.236
server04.hcmut.edu.vn has address 221.133.13.114
server05.hcmut.edu.vn has address 221.133.13.116
server06.hcmut.edu.vn has address 203.205.32.235
server07.hcmut.edu.vn has address 221.133.13.117
server09.hcmut.edu.vn has address 203.205.32.235
server11.hcmut.edu.vn has address 221.133.13.117
server12.hcmut.edu.vn has address 221.133.13.118
server14.hcmut.edu.vn has address 221.133.13.108
server15.hcmut.edu.vn has address 221.133.13.115
server236.hcmut.edu.vn has address 221.133.13.110
server30.hcmut.edu.vn has address 221.133.13.121
server80.hcmut.edu.vn has address 221.133.13.119
server89.hcmut.edu.vn has address 221.133.13.120
shms.hcmut.edu.vn has address 221.133.13.111
sso.hcmut.edu.vn has address 221.133.13.120
sso-net.hcmut.edu.vn has address 221.133.13.111
sso-net2.hcmut.edu.vn has address 221.133.13.111
test.hcmut.edu.vn has address 221.133.13.108
traffic.hcmut.edu.vn has address 103.88.121.161
tris.hcmut.edu.vn has address 14.161.5.98
tuyensinh.hcmut.edu.vn has address 221.133.13.124
tv-cam01.hcmut.edu.vn has address 221.133.13.114
tv-cam02.hcmut.edu.vn has address 221.133.13.115
tv-cam03.hcmut.edu.vn has address 113.161.83.117
uiseminar2017.hcmut.edu.vn has address 198.252.111.243
www.uiseminar2017.hcmut.edu.vn has address 198.252.111.243
vre.hcmut.edu.vn has address 103.88.121.151
wifi-controller.hcmut.edu.vn has address 221.133.13.110
wifi-cse.hcmut.edu.vn has address 172.28.211.1
wiki.hcmut.edu.vn has address 221.133.13.124

---------------------------------------------------------
## Nameserver: dns1.hcmut.edu.vn.
### Transferring zone...
Using domain server:
Name: dns1.hcmut.edu.vn.
Address: 221.133.13.114#53
Aliases: 

Host hcmut.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: dns3.hcmut.edu.vn.
### Transferring zone...
Using domain server:
Name: dns3.hcmut.edu.vn.
Address: 203.205.32.235#53
Aliases: 

hcmut.edu.vn name server dns1.hcmut.edu.vn.
hcmut.edu.vn name server dns2.hcmut.edu.vn.
hcmut.edu.vn name server dns3.hcmut.edu.vn.
hcmut.edu.vn name server dns4.hcmut.edu.vn.
hcmut.edu.vn has address 221.133.13.114
60.hcmut.edu.vn has address 112.213.89.2
aao.hcmut.edu.vn has address 221.133.13.122
apps.aao.hcmut.edu.vn has address 221.133.13.124
server.aao.hcmut.edu.vn has address 221.133.13.122
actbk.hcmut.edu.vn has address 221.133.13.127
alumni.hcmut.edu.vn has address 221.133.13.109
amis.hcmut.edu.vn has address 221.133.13.106
bkiot.hcmut.edu.vn has address 210.211.113.130
bkpay.hcmut.edu.vn has address 221.133.13.124
bksi.hcmut.edu.vn has address 221.133.13.118
bkyst.hcmut.edu.vn has address 45.119.83.20
bridge.hcmut.edu.vn has address 113.176.61.107
bridge2.hcmut.edu.vn has address 123.30.157.251
carerescif.hcmut.edu.vn has address 112.213.89.145
www.carerescif.hcmut.edu.vn has address 112.213.89.145
casdev-master.hcmut.edu.vn has address 221.133.13.105
cc.hcmut.edu.vn has address 112.78.1.105
cce.hcmut.edu.vn has address 112.78.1.105
conferences.hcmut.edu.vn has address 221.133.13.111
www.conferences.hcmut.edu.vn has address 221.133.13.111
cse.hcmut.edu.vn has address 221.133.13.113
60.cse.hcmut.edu.vn has address 61.28.227.157
doanhoi.cse.hcmut.edu.vn has address 45.119.83.33
elearning.cse.hcmut.edu.vn has address 221.133.13.110
internship.cse.hcmut.edu.vn has address 221.133.13.108
server.cse.hcmut.edu.vn has address 221.133.13.113
vre.cse.hcmut.edu.vn has address 103.88.121.151
ctct.hcmut.edu.vn has address 125.212.245.195
dcselab.hcmut.edu.vn has address 221.132.37.37
demo.hcmut.edu.vn has address 221.133.13.105
diemthi.hcmut.edu.vn has address 221.133.13.122
diemthi.hcmut.edu.vn has address 103.88.121.145
diemthi.hcmut.edu.vn has address 115.78.0.48
dkmh.hcmut.edu.vn has address 221.133.13.124
dls.hcmut.edu.vn has address 103.88.121.156
dns1.hcmut.edu.vn has address 221.133.13.114
dns2.hcmut.edu.vn has address 221.133.13.115
dns3.hcmut.edu.vn has address 203.205.32.235
dns4.hcmut.edu.vn has address 203.205.32.236
dae.dte.hcmut.edu.vn has address 171.244.43.27
www.dae.dte.hcmut.edu.vn has address 171.244.43.27
e-learning.hcmut.edu.vn has address 221.133.13.123
elearning-cse.hcmut.edu.vn has address 221.133.13.107
fdse2017.hcmut.edu.vn has address 61.28.227.157
fe.hcmut.edu.vn has address 52.74.151.191
fenr.hcmut.edu.vn has address 112.213.89.145
www.fenr.hcmut.edu.vn has address 112.213.89.145
hre.fme.hcmut.edu.vn has address 125.212.209.56
ise.fme.hcmut.edu.vn has address 103.48.81.8
gateway01.hcmut.edu.vn has address 14.241.245.110
gateway02.hcmut.edu.vn has address 221.133.12.6
gateway2.hcmut.edu.vn has address 113.161.83.117
gpu02.hcmut.edu.vn has address 103.88.121.152
gpu11.hcmut.edu.vn has address 103.88.121.150
grad.hcmut.edu.vn has address 221.133.13.127
graylog.hcmut.edu.vn has address 221.133.13.115
gtsw2019.hcmut.edu.vn has address 166.62.28.82
www.gtsw2019.hcmut.edu.vn has address 166.62.28.82
hnkhcn2013.hcmut.edu.vn has address 112.213.89.149
hpcc.hcmut.edu.vn has address 203.205.33.134
hpccbk.hcmut.edu.vn has address 116.118.106.108
hpccportal.hcmut.edu.vn has address 203.205.33.134
hpclab.hcmut.edu.vn has address 103.88.121.154
icse.hcmut.edu.vn has address 103.18.6.44
www.icse.hcmut.edu.vn has address 103.18.6.44
imp.hcmut.edu.vn has address 103.221.220.25
www.imp.hcmut.edu.vn has address 103.221.220.25
impactmap.hcmut.edu.vn has address 61.28.227.157
iot.hcmut.edu.vn has address 61.28.227.157
iotlab.hcmut.edu.vn has address 210.211.113.130
iro.hcmut.edu.vn has address 112.213.89.46
www.iro.hcmut.edu.vn has address 112.213.89.46
it.hcmut.edu.vn has address 103.88.121.162
tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
www.tracuuhoadon.khtc.hcmut.edu.vn has address 103.145.62.137
ktx.hcmut.edu.vn has address 203.205.32.235
opac.lib.hcmut.edu.vn has address 103.88.121.159
portal.lib.hcmut.edu.vn has address 221.133.13.104
server.lib.hcmut.edu.vn has address 112.213.85.46
lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
www.lmpi-erasmus.hcmut.edu.vn has address 221.133.13.113
log.hcmut.edu.vn has address 221.133.13.108
logserver.hcmut.edu.vn has address 221.133.13.108
meet.hcmut.edu.vn has address 14.241.245.187
meganet.hcmut.edu.vn has address 10.128.0.1
meganet-gateway.hcmut.edu.vn has address 14.169.141.126
meganet-gateway2.hcmut.edu.vn has address 14.169.17.32
meganet02.hcmut.edu.vn has address 10.130.0.1
meganet2.hcmut.edu.vn has address 10.228.0.1
membrane2014.hcmut.edu.vn has address 112.213.89.144
mining.hcmut.edu.vn has address 103.88.121.145
mybk.hcmut.edu.vn has address 221.133.13.124
netdata.hcmut.edu.vn has address 221.133.13.116
ntop.hcmut.edu.vn has address 221.133.13.115
oisp.hcmut.edu.vn has address 103.90.220.204
sinhvien.oisp.hcmut.edu.vn has address 221.132.17.180
personel.hcmut.edu.vn has address 221.133.13.127
pgs.hcmut.edu.vn has address 221.133.13.112
portal.hcmut.edu.vn has address 221.133.13.108
private01.hcmut.edu.vn has address 10.130.0.1
private6.hcmut.edu.vn has address 10.228.0.1
pssp.hcmut.edu.vn has address 221.133.13.105
public.hcmut.edu.vn has address 172.28.232.1
public2.hcmut.edu.vn has address 10.28.232.1
qlns.hcmut.edu.vn has address 221.133.13.108
radius01.hcmut.edu.vn has address 221.133.12.6
radius1.hcmut.edu.vn has address 221.133.12.6
recsys.hcmut.edu.vn has address 221.133.13.106
rsce2016.hcmut.edu.vn has address 103.227.177.226
sc.hcmut.edu.vn has address 221.133.13.121
scc.hcmut.edu.vn has address 61.28.227.157
server02.hcmut.edu.vn has address 221.133.13.115
server03.hcmut.edu.vn has address 203.205.32.236
server04.hcmut.edu.vn has address 221.133.13.114
server05.hcmut.edu.vn has address 221.133.13.116
server06.hcmut.edu.vn has address 203.205.32.235
server07.hcmut.edu.vn has address 221.133.13.117
server09.hcmut.edu.vn has address 203.205.32.235
server11.hcmut.edu.vn has address 221.133.13.117
server12.hcmut.edu.vn has address 221.133.13.118
server14.hcmut.edu.vn has address 221.133.13.108
server15.hcmut.edu.vn has address 221.133.13.115
server236.hcmut.edu.vn has address 221.133.13.110
server30.hcmut.edu.vn has address 221.133.13.121
server80.hcmut.edu.vn has address 221.133.13.119
server89.hcmut.edu.vn has address 221.133.13.120
shms.hcmut.edu.vn has address 221.133.13.111
sso.hcmut.edu.vn has address 221.133.13.120
sso-net.hcmut.edu.vn has address 221.133.13.111
sso-net2.hcmut.edu.vn has address 221.133.13.111
test.hcmut.edu.vn has address 221.133.13.108
traffic.hcmut.edu.vn has address 103.88.121.161
tris.hcmut.edu.vn has address 14.161.5.98
tuyensinh.hcmut.edu.vn has address 221.133.13.124
tv-cam01.hcmut.edu.vn has address 221.133.13.114
tv-cam02.hcmut.edu.vn has address 221.133.13.115
tv-cam03.hcmut.edu.vn has address 113.161.83.117
uiseminar2017.hcmut.edu.vn has address 198.252.111.243
www.uiseminar2017.hcmut.edu.vn has address 198.252.111.243
vre.hcmut.edu.vn has address 103.88.121.151
wifi-controller.hcmut.edu.vn has address 221.133.13.110
wifi-cse.hcmut.edu.vn has address 172.28.211.1
wiki.hcmut.edu.vn has address 221.133.13.124

---------------------------------------------------------

################################################################

# Domain: uel.edu.vn
## Nameserver: ns2.dns.net.vn.
### Transferring zone...
Using domain server:
Name: ns2.dns.net.vn.
Address: 103.45.229.100#53
Aliases: 

Host uel.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: ns1.dns.net.vn.
### Transferring zone...
Using domain server:
Name: ns1.dns.net.vn.
Address: 210.211.108.160#53
Aliases: 

Host uel.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------

################################################################

# Domain: hcmier.edu.vn
## Nameserver: server.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: server.vnuhcm.edu.vn.
Address: 103.88.121.201#53
Aliases: 

Host hcmier.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: vnuserv.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: vnuserv.vnuhcm.edu.vn.
Address: 103.88.121.200#53
Aliases: 

Host hcmier.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------

################################################################

# Domain: vnuhcm.edu.vn
## Nameserver: ns1.vdc2.vn.
### Transferring zone...
Using domain server:
Name: ns1.vdc2.vn.
Address: 14.225.232.186#53
Aliases: 

Host vnuhcm.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: ns2.vdc2.vn.
### Transferring zone...
Using domain server:
Name: ns2.vdc2.vn.
Address: 14.225.232.23#53
Aliases: 

vnuhcm.edu.vn has address 103.88.121.29
vnuhcm.edu.vn name server vnuserv.vnuhcm.edu.vn.
vnuhcm.edu.vn name server server.vnuhcm.edu.vn.
www.4s.vnuhcm.edu.vn has address 118.69.204.199
aaa.vnuhcm.edu.vn has address 103.88.123.21
aaa1.vnuhcm.edu.vn has address 103.88.123.22
aad.vnuhcm.edu.vn has address 203.162.44.60
ab.vnuhcm.edu.vn has address 203.162.147.252
aun.vnuhcm.edu.vn has address 203.162.147.168
baixektx.vnuhcm.edu.vn has address 123.30.236.140
baocaoaad.vnuhcm.edu.vn has address 203.162.44.60
mssql.baocaoaad.vnuhcm.edu.vn has address 203.162.44.60
betaaad.vnuhcm.edu.vn has address 222.255.69.252
cdio2015.vnuhcm.edu.vn has address 221.133.13.127
cea.vnuhcm.edu.vn has address 103.88.123.7
csgd.cea.vnuhcm.edu.vn has address 103.88.123.7
database.cea.vnuhcm.edu.vn has address 103.88.123.7
dkht.cea.vnuhcm.edu.vn has address 103.88.123.7
cete.vnuhcm.edu.vn has address 103.88.123.2
chrd.vnuhcm.edu.vn has address 203.162.147.149
club.vnuhcm.edu.vn has address 203.162.147.185
www.cntttt.vnuhcm.edu.vn has address 203.162.44.72
congdoan.vnuhcm.edu.vn has address 118.69.123.142
cpmu-demo.vnuhcm.edu.vn has address 103.88.121.59
cpmu-demo1.vnuhcm.edu.vn has address 112.78.11.146
cps.vnuhcm.edu.vn has address 112.78.11.146
ct.vnuhcm.edu.vn has address 203.162.147.252
data.vnuhcm.edu.vn has address 203.162.147.185
dataonline.vnuhcm.edu.vn has address 203.162.44.60
demo.vnuhcm.edu.vn has address 103.88.121.29
demo-cloud.vnuhcm.edu.vn has address 103.88.121.64
demo-khcn.vnuhcm.edu.vn has address 203.162.147.185
demo-lms.vnuhcm.edu.vn has address 103.88.121.142
demo-portal.vnuhcm.edu.vn has address 203.128.241.215
demo-portal-admin.vnuhcm.edu.vn has address 203.128.241.215
demo-portal-static.vnuhcm.edu.vn has address 203.128.241.21
demo1.vnuhcm.edu.vn has address 203.162.147.185
demotuyensinh.vnuhcm.edu.vn has address 203.162.147.186
doancoquan.vnuhcm.edu.vn has address 203.162.147.186
doancoquan.vnuhcm.edu.vn has address 103.74.123.10
doantn.vnuhcm.edu.vn has address 203.162.44.83
email-reply.vnuhcm.edu.vn has address 103.88.121.53
gddhhoinhapquocte.vnuhcm.edu.vn has address 123.30.191.189
greeting-card.vnuhcm.edu.vn has address 203.162.147.185
hoidong.vnuhcm.edu.vn has address 203.162.147.185
hoithaocokhi.vnuhcm.edu.vn has address 165.22.97.200
hoithaogiaothong.vnuhcm.edu.vn has address 206.189.35.164
hosting.vnuhcm.edu.vn has address 203.162.147.185
hotrokythuat.vnuhcm.edu.vn has address 112.78.11.146
idm.vnuhcm.edu.vn has address 103.88.123.51
it-support.vnuhcm.edu.vn has address 112.78.11.146
jobs.vnuhcm.edu.vn has address 103.88.123.54
khaosat.vnuhcm.edu.vn has address 203.162.147.185
khcn.vnuhcm.edu.vn has address 203.162.147.185
quanly.khcn.vnuhcm.edu.vn has address 118.69.123.142
khcn2018.vnuhcm.edu.vn has address 103.88.121.35
khoanhkhacdothidaihoc.vnuhcm.edu.vn has address 123.30.78.232
kitucxa.vnuhcm.edu.vn has address 45.117.77.102
ksknsvtn.vnuhcm.edu.vn has address 203.162.44.60
ktx.vnuhcm.edu.vn has address 45.117.77.103
mail.ktx.vnuhcm.edu.vn has address 203.162.44.60
ktxdhqg.vnuhcm.edu.vn has address 45.117.77.102
ktxdhqghcm.vnuhcm.edu.vn has address 123.30.236.140
lichtuan.vnuhcm.edu.vn has address 203.162.147.195
live.vnuhcm.edu.vn has address 42.116.11.16
manage-01.vnuhcm.edu.vn has address 103.88.123.64
manage-02.vnuhcm.edu.vn has address 103.88.121.41
meeting.vnuhcm.edu.vn has address 203.162.147.247
noc.vnuhcm.edu.vn has address 112.78.10.40
ns.vnuhcm.edu.vn has address 10.159.136.186
ns1.vnuhcm.edu.vn has address 10.159.136.186
ns2.vnuhcm.edu.vn has address 10.159.136.186
ntb.vnuhcm.edu.vn has address 103.88.88.88
phapluat.vnuhcm.edu.vn has address 74.86.148.43
portal-st.vnuhcm.edu.vn has address 103.88.121.38
qlcb.vnuhcm.edu.vn has address 118.69.123.137
qlda-vp.vnuhcm.edu.vn has address 103.88.121.138
qlda-xd.vnuhcm.edu.vn has address 103.88.121.137
qldt.vnuhcm.edu.vn has address 103.88.121.38
qtmvp.vnuhcm.edu.vn has address 203.163.1.150
quanlydetai.vnuhcm.edu.vn has address 115.78.164.32
rankingdata.vnuhcm.edu.vn has address 103.88.121.33
rk.vnuhcm.edu.vn has address 103.88.121.33
rkd.vnuhcm.edu.vn has address 103.88.121.33
rm.vnuhcm.edu.vn has address 103.88.121.37
rnm.vnuhcm.edu.vn has address 103.88.121.37
server.vnuhcm.edu.vn has address 103.88.121.201
server.vnuhcm.edu.vn has address 10.159.136.186
server3.vnuhcm.edu.vn has address 203.162.147.149
sm-vnu.vnuhcm.edu.vn has address 203.162.44.47
static.vnuhcm.edu.vn has address 103.88.121.29
svktx.vnuhcm.edu.vn has address 45.117.77.102
tapchikhoahoc.vnuhcm.edu.vn has address 203.162.147.185
tchc.vnuhcm.edu.vn has address 203.162.147.241
test.vnuhcm.edu.vn has address 203.162.147.186
testbed.vnuhcm.edu.vn has address 203.162.44.55
testing.vnuhcm.edu.vn has address 203.162.147.179
testweb.vnuhcm.edu.vn has address 123.30.78.233
thinangluc.vnuhcm.edu.vn has address 118.69.123.136
thinangluc.vnuhcm.edu.vn has address 45.122.249.72
thinangluc-test.vnuhcm.edu.vn has address 221.133.13.124
thumoi.vnuhcm.edu.vn has address 125.253.116.180
thuongnien.vnuhcm.edu.vn has address 203.162.147.252
tspl.vnuhcm.edu.vn has address 203.162.44.60
ttgdqp.vnuhcm.edu.vn has address 222.255.69.250
ttqlptkdt.vnuhcm.edu.vn has address 203.162.44.60
ttqlptkdt-beta.vnuhcm.edu.vn has address 203.162.44.60
tttdtt.vnuhcm.edu.vn has address 103.88.123.130
tuoitre.vnuhcm.edu.vn has address 210.211.118.168
tuvantuyensinh.vnuhcm.edu.vn has address 203.162.147.185
dangky.tuyensinh.vnuhcm.edu.vn has address 203.162.147.196
vc.vnuhcm.edu.vn has address 171.244.28.100
vnu-f.vnuhcm.edu.vn has address 103.88.121.141
www.vnu-f.vnuhcm.edu.vn has address 103.88.121.141
vnu-f2.vnuhcm.edu.vn has address 103.88.123.5
vnu20.vnuhcm.edu.vn has address 203.162.147.185
vnuc.vnuhcm.edu.vn has address 112.78.11.146
vnuserv.vnuhcm.edu.vn has address 103.88.121.200
vnuserv.vnuhcm.edu.vn has address 10.159.136.186
voice.vnuhcm.edu.vn has address 203.162.147.187
wifi.vnuhcm.edu.vn has address 10.238.239.1
www.vnuhcm.edu.vn has address 103.88.121.29

---------------------------------------------------------
## Nameserver: server.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: server.vnuhcm.edu.vn.
Address: 103.88.121.201#53
Aliases: 

Host vnuhcm.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------
## Nameserver: vnuserv.vnuhcm.edu.vn.
### Transferring zone...
Using domain server:
Name: vnuserv.vnuhcm.edu.vn.
Address: 103.88.121.200#53
Aliases: 

Host vnuhcm.edu.vn not found: 5(REFUSED)
; Transfer failed.

---------------------------------------------------------

################################################################

# Domain: agu.edu.vn
## Nameserver: out;
### Transferring zone...

---------------------------------------------------------

################################################################
```

## Câu 35
### Question
Sử dụng thêm 2 NSE script (tự chọn) để quét máy mục tiêu (Metasploitable 2).

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
