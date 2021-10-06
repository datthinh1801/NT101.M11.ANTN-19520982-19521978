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



## Câu 11
### Question
Sử dụng Netcraft để xác định máy chủ ứng dụng (application server) đang chạy trên www.megacorpone.com.

### Answer
![image](https://user-images.githubusercontent.com/44528004/136158113-227712a9-61a0-4af3-b016-bb615ba9a1ed.png)


## Câu 17
### Question
Sử dụng công cụ theHarvester để lấy tìm kiếm các địa chỉ email của UIT.

### Answer
![image](https://user-images.githubusercontent.com/44528004/136160112-8cc3f728-b626-4582-83d3-303b85fd6666.png)  


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

![image](https://user-images.githubusercontent.com/31529599/136163234-20cd4839-8fdc-40bf-a677-a19096b1f030.png)



