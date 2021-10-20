# Vulnerability Scanning
## Câu 1
### Question
Thực hiện lại các bước trên để quét máy Metasploitable 2 không sử dụng tài khoản chứng thực.  

### Answer
![image](https://user-images.githubusercontent.com/44528004/138049697-e0f2f58c-0dbc-465b-a8bf-88999f830e42.png)


## Câu 2
### Question
Bật Wireshark sau đó tiến hành quét và xác định các bước mà Nessus đã thực hiện để hoàn tất quá trình quét.

### Answer
Khi sử dụng wireshark và quan sát port `80` (port này đã được mở) thì ta thấy rằng:  
- Máy scanner `10.1.1.128` sẽ gửi 1 gói tin TCP SYN để yêu cầu mở kết nối TCP tới máy victim `10.1.1.130`. Đây cũng là bước đầu tiên trong quy trình bắt tay 3 bước của TCP.  
- Tiếp theo, máy victim sẽ phản hồi lại bằng một gói tin SYN ACK. Điều này chứng tỏ port này hiện đang mở trên máy victim và chấp nhận mở kết nối TCP.  
- Cuối cùng, máy scanner sẽ gửi 1 gói tin TCP RST để đóng kết nối.   

![image](https://user-images.githubusercontent.com/44528004/138048338-412d1dcb-a091-4418-bfbc-404a5ec7bf27.png)

Trong một trường hợp khác ở port `90`:  

![image](https://user-images.githubusercontent.com/44528004/138049008-4cc354ef-a39b-408e-b611-7d0adbe736ad.png)  

- Đầu tiên, máy scanner gửi gói tin TCP SYN đến máy victim.  
- Lúc này, victim phản hồi với gói tin RST ACK để acknowlege cho gói SYN nhưng yêu cầu đóng kết nối với flag RST. Điều này đồng nghĩa với việc máy victim không mở port `90`.

## Câu 4
### Question
Thực hiện lại các bước trên để quét máy Metasploitable 2 có sử dụng tài khoản chứng thực.  

### Answer
![image](https://user-images.githubusercontent.com/44528004/138052817-dc73d885-d058-4233-8e16-8c0f42d6be1d.png)

## Câu 7
### Question
Thực hiện lại các bước trên để quét máy Metasploitable 2 sử dụng plugin NFS Exported Share Information Disclosure.

### Answer
![image](https://user-images.githubusercontent.com/44528004/138053428-e5ad689d-a826-495e-902a-3083598c5353.png)


![image](https://user-images.githubusercontent.com/44528004/138053394-b3c7a085-58e7-4c91-9cdb-6b3dd8784176.png)

