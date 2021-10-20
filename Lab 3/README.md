# Vulnerability Scanning
## Câu 1

## Câu 2
Khi sử dụng wireshark và quan sát port `80` (port này đã được mở) thì ta thấy rằng:  
- Máy scanner `10.1.1.128` sẽ gửi 1 gói tin TCP SYN để yêu cầu mở kết nối TCP tới máy victim `10.1.1.130`. Đây cũng là bước đầu tiên trong quy trình bắt tay 3 bước của TCP.  
- Tiếp theo, máy victim sẽ phản hồi lại bằng một gói tin SYN ACK. Điều này chứng tỏ port này hiện đang mở trên máy victim và chấp nhận mở kết nối TCP.  
- Cuối cùng, máy scanner sẽ gửi 1 gói tin TCP RST để đóng kết nối.   

![image](https://user-images.githubusercontent.com/44528004/138048338-412d1dcb-a091-4418-bfbc-404a5ec7bf27.png)

Trong một trường hợp khác ở port `90`:  

![image](https://user-images.githubusercontent.com/44528004/138049008-4cc354ef-a39b-408e-b611-7d0adbe736ad.png)  

- Đầu tiên, máy scanner gửi gói tin TCP SYN đến máy victim.  
- Lúc này, victim phản hồi với gói tin RST ACK để acknowlege cho gói SYN nhưng yêu cầu đóng kết nối với flag RST. Điều này đồng nghĩa với việc máy victim không mở port `90`.
