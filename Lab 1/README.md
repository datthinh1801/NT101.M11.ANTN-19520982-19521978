# Lab 1: Tổng quan Kali Linux
## Câu 1
### Description
Sử dụng lệnh `which` để xác định ví trị lưu trữ của lệnh `pwd`.

### Solution
```
└─$ which pwd   
pwd: shell built-in command
```

Vấn đè ở đây là `pwd` là shell built-in command nên `which` sẽ không trả về `pathname`. Nhưng khi xem manual page của `which`, ta có duy nhất 1 option và option này được dùng để in ra tòan bộ pathname của 1 command:
```
OPTIONS
       -a     print all matching pathnames of each argument
```

Sử dụng `which` với `-a` option:
```
└─$ which -a pwd
pwd: shell built-in command
/usr/bin/pwd
/bin/pwd
```

## Câu 2
### Description
Sử dụng lệnh `locate` để xác định ví trí lưu trữ `wce32.exe`.

### Solution
```
└─$ locate wce32.exe
/usr/share/windows-resources/wce/wce32.exe
```

## Câu 3
### Description
Sử dụng lệnh `find` để xác định bất kỳ tập tin (không phải thư mục) đã được sửa đổi vào ngày trước đó, **KHÔNG** thuộc sở hữu của user `root` và thực thi lệnh `ls -l` trên chúng. **KHÔNG** được sử dụng các lệnh **pipeline/chaining**.

### Solution
Ở câu này, ta có các yêu cầu sau:
- Tập tin (không phải thư mục)
- Được sửa đỏi vào ngày trước đó
- Không thuộc sơ hữu của user `root`

Đầu tiên, để tìm tập tin mà không phải thư mục, ta dùng option `-type f`.  
Tiếp theo, để tìm file được sửa đổi 1 ngày trước đó, ta dùng option `-ctime n`. Theo manual page của `find` thì option `-ctime` được dùng như sau:
```
-ctime n
              File's status was last changed less than, more than or exactly n*24 hours ago.
```

Ở đây, `n` của chúng ta sẽ bằng `1` vì chúng ta muốn tìm file đã được sửa đôi 1 ngày (24 giờ) trước đó. Nếu ta muốn tìm các file đã được sửa đổi **trong vòng 24 giờ qua** thì `n` sẽ là `-1`.  

Để tìm file không thuộc quyền sở hữu của user `root` ta dùng option `! -user root`. Ở đây, `-user root` sẽ cho ra các file thuộc sỡ hưu của `root và `!` sẽ phủ định lại điều kiện.

Vậy câu lệnh để tìm các file thỏa mãn yêu cầu là:
```
find / -type f -ctime 1 ! -user root
```
Để `ls -l` các file này, ta sẽ sử dụng `-exec` trong command `find`:
```
sudo find / -type f -ctime 1 ! -user root -exec ls -l {} +
```
> Vì điểm bắt dầu tìm là `/` nên ta cần quyền admin với `sudo`.


## Câu 4
### Description
Liệt kê các port đang được mở trên Kali Linux.

### Solution
Để liệt kê tất cả các port đang được mở, ta dùng command sau:
```
└─$ sudo ss -lutn                                                                                            
Netid     State      Recv-Q      Send-Q           Local Address:Port           Peer Address:Port     Process     
tcp       LISTEN     0           128                    0.0.0.0:22                  0.0.0.0:*                    
tcp       LISTEN     0           128                       [::]:22                     [::]:*                    
tcp       LISTEN     0           511                          *:80                        *:*                    
```

Với option `-l` để liệt kê các ports mà máy đang lắng nghe, `-u` để liệt kệ các UDP sockets và `-t` để liệt kê các `TCP` sockets. Cuối cùng, `-n` để show địa chỉ IP mà không cần phân giải tên miền. Việc này sẽ giúp giảm thời gian thực thi của câu lệnh.

## Câu 5
### Question
Tại sao khi kiểm tra dịch vụ SSH có đang chạy hay không, kết quả hiển thị 2 dòng, trong khi dịch vụ HTTP, kết quả chỉ có 1 dòng.
```
└─$ sudo ss -utln
Netid     State      Recv-Q      Send-Q           Local Address:Port           Peer Address:Port     Process     
tcp       LISTEN     0           128                    0.0.0.0:22                  0.0.0.0:*                    
tcp       LISTEN     0           128                       [::]:22                     [::]:*                    
tcp       LISTEN     0           511                          *:80                        *:*                    
```

### Answer
Việc dịch vụ SSH có 2 dòng hiển thị là vì dịch vụ này hoạt động trên IPv4 và IPv6 (`0.0.0.0` là địa chỉ IPv4 và `[::]` là địa chỉ IPv6). Trong khi đó, dịch vụ HTTP chỉ hoạt động trên IPv4 nên chỉ có 1 dòng hiển thị.

## Câu 6
### Description
Ngăn dịch vụ SSH chạy cùng với hệ thống lúc khởi động.

### Solution
Như ta đã biết, câu lệnh `systemctl enable <service-name>` sẽ tự động khởi động 1 dịch vụ cùng hệ thống khi khởi động. Vậy ta có thể đoán được là `systemctl disable <service-name>` sẽ làm điều ngược lại.  

Vậy để ngăn dịch vụ SSH chạy cùng hệ thống, ta dùng câu lệnh sau:
```
└─$ sudo systemctl disable ssh  
Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable ssh
```

## Câu 7
### Question
Lịch sử các lệnh thực ra được lưu trữ ở đâu? Liệt kê các ưu, nhược điểm khi thực hiện lưu trữ lại các lệnh đã nhập?

### Answer
- Lịch sử các lệnh được lưu tại file `/home/user/.<shell>_history`. Nếu ta sử dụng `bash` thì lịch sử sẽ được lưu tại `/home/user/.bash_history`. Kali Linux sử `zsh` nên lịch sử sẽ được lưu tại `/home/user/.zsh_history`.
- Ưu điểm của việc lưu lịch sử các câu lệnh là ta có thể dễ dàng xem lại, sử dụng lại các câu lệnh cũ nhằm tránh gõ đi gõ lại một câu lệnh nhiều lần.
- Nhược điểm là nếu có 1 người khác sử dụng máy tính của chúng ta, với `user` của chúng ta và họ xem được command history thì sẽ biết được các hoạt động của chúng ta trên máy.

## Câu 8
### Question
Có cách nào để ngăn chặn việc lưu trữ lịch sử lệnh hay không? Nếu có, hãy mô tả cách làm.

### Answer
Có 2 cách:
- Vì lịch sử câu lệnh được lưu trên file, nên ta có thể xóa hoặc làm rỗng file này sau mỗi lần sử dụng. Một cách nhanh gọn là sử dụng option `-c` của chính câu lệnh `history`:` history -c`. Tuy nhiên có 1 số shell không hỗ trợ option này (ví dụ `zsh`).
- Cấu hình shell. Để cấu hình shell, ta mở file cấu hình (file cấu hình thường có tên là `.<shell>rc` nằm tại thư mục  home của người dùng, ví dụ trên Kali sẽ là `/home/kali/.zshrc`) và set giá trị cho `HISTSIZE=n` với `n` là số câu lệnh ta muốn lưu. Để không lưu lịch sử thì ta set `HISTSIZE=0`.

## Câu 9
### Question
Ngoài cách sử dụng tiện ích history expansion, còn cách nào để thực hiện lại các lệnh đã nhập một cách nhanh chóng hay không? Nếu có, hãy mô tả cách làm.

### Answer
Ngoài cách sử dụng tiện ích history expansion như lệnh `history`, mũi tên lên xuống để chọn nhanh câu lệnh trước đó, các shortcut như `!!`, `!n`, ta còn một cách khác để có thể thực hiện lại các lệnh đã nhập là ta đọc file `.<shell>_history`. Như đã đề cập ở câu 7, file này sẽ lưu lại lịch sử lệnh của shell tương ứng, kể cả khi ta thay đổi `HISTSIZE=0` thì file này vẫn không bị xóa.

## Câu 10
### Question
Như đã biết, khi sử dụng toán tử `>` để xuất kết quả vô tập tin, nếu tập tin đã tồn tại, nội dung trong tập tin sẽ bị thay thế bằng nội dung mới. Vậy, có cách nào để hoàn tác lại quá trình này hay không? Nếu có, hãy mô tả cách làm.

### Solution
Nếu ta có sử dụng các VCS như `git` và nội dung cũ của tập tin đã được staged thì ta có thể recover thông qua các VCS này. Nếu ta sử dụng git, ta có 2 subcommand là `reset` và `revert`. Với `git reset`, ta sẽ rollback trạng thái và nội dung của file về lại 1 checkpoint nào đó và các checkpoint phía sau sẽ bị ẩn/xóa (tùy ta chọn). Còn đối với `git revert` ta cũng sẽ rollback trạng thái và nội dung của file về lại 1 checkpoint nhưng sẽ không có checkpoint nào bị xóa mà sẽ có thêm 1 commit nữa được tạo để đánh dấu việc revert này.

## Câu 11
### Description
Sử dụng lệnh `cat` cùng với lệnh `sort` để sắp xếp lại nội dung của tập tin `/etc/passwd`, sau đó lưu kết quả vào một tập tin mới có tên `passwd_new` và thực hiện đến số lượng dòng có trong tập tin mới.

### Solution
Đầu tiên, ta đọc file `/etc/passwd`, sau đó pipeline sang lệnh `sort` để sắp xếp lại nội dung. Sau đó, ta redirect nội dung đã sắp xếp vào file `passwd_new` với redirection operator `>`. Cuối cùng, ta pipeline nội dung đã sắp xếp vào lệnh `wc` với option `-l` để đêm số dòng.
```
└─$ cat /etc/passwd | sort > password_new | wc -l
```

## Câu 12
### Description
Sử dụng tập tin `/etc/passwd`, trích xuất tên `user` và home directory cho tất cả user có shell được thiết lập là `/usr/sbin/nologin`. Lưu ý, chỉ sử dụng 1 dòng lệnh duy nhất. Kết quả xuất ra màn hình như hình dưới.

### Solution
Khi xem qua cấu trúc của file `/etc/passwd`, ta có thể thấy là các trường được cách nhau bởi dấu 2 chấm `:`. Vậy ta có thể tận dụng `awk` để truy xuất các trường này 1 cách dễ dàng.
```
└─$ awk -F ':' '{if($7 == "/usr/sbin/nologin") print "The user", $1, "directory is", $7}' /etc/passwd
The user daemon directory is /usr/sbin/nologin
The user bin directory is /usr/sbin/nologin
The user sys directory is /usr/sbin/nologin
The user games directory is /usr/sbin/nologin
# ...
```

Với `awk`, ta dùng option `-F` để chỉ ra dấu ngăn cách giữa các trường, ở đây là `:`. Tiếp theo, ta chỉ quan tâm các user có thiết lập shell là `/usr/sbin/nologin` nên ta sẽ trực tiếp dùng `if` trong `awk`. Trong if statement này, ta muốn rằng nếu trường thứ 7 bằng với `/usr/sbin/nologin`, thì sẽ thực thi việc in dòng text mà ta chọn. Trong trường này là `The user $1 directory is $7` với `$1` là trường thứ nhất tương ứng với tên user và `$7` là trường thứ 7 tương ứng với thiết lập shell.

## Câu 13
### Description
Tải tập tin [access_log.txt.gz](https://github.com/blakduk/ahihi/raw/master/access_log.txt.gz), sau đó thực hiện liệt kê danh sách các địa chỉ IP và số lượng tương ứng, thực hiện sắp xếp giảm dần.

### Solution
Đầu tiên, để tải tập tin trên, ta có thể dùng `wget`:
```
└─$ wget "https://github.com/blakduk/ahihi/raw/master/access_log.txt.gz"
--2021-09-26 23:22:54--  https://github.com/blakduk/ahihi/raw/master/access_log.txt.gz
Resolving github.com (github.com)... 52.74.223.119
Connecting to github.com (github.com)|52.74.223.119|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/blakduk/ahihi/master/access_log.txt.gz [following]
--2021-09-26 23:22:54--  https://raw.githubusercontent.com/blakduk/ahihi/master/access_log.txt.gz
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3783 (3.7K) [application/octet-stream]
Saving to: ‘access_log.txt.gz’

access_log.txt.gz            100%[===========================================>]   3.69K  --.-KB/s    in 0s      

2021-09-26 23:22:54 (20.2 MB/s) - ‘access_log.txt.gz’ saved [3783/3783]
```

Sau đó, ta sẽ có được file `access_log.txt.gz`:
```
└─$ ls
access_log.txt.gz
```

Tiếp theo, ta decompress file bằng `gunzip` vì file này đang được nén ở dạng `gzip`. Sau đó ta sẽ được file `.txt`.
```
└─$ gunzip ./access_log.txt.gz
└─$ ls
access_log.txt
```

Khi xem qua file log này, ta thấy địa chỉ IP thuộc trường đầu tiên, sau đó là 1 delimiter `-`.
```
└─$ head access_log.txt 
201.21.152.44 - - [25/Apr/2013:14:05:35 -0700] "GET /favicon.ico HTTP/1.1" 404 89 "-" "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.31 (KHTML, like Gecko) Chrome/26.0.1410.64 Safari/537.31" "random-site.com"
70.194.129.34 - - [25/Apr/2013:14:10:48 -0700] "GET /include/jquery.jshowoff.min.js HTTP/1.1" 200 2553 "http://www.random-site.com/" "Mozilla/5.0 (Linux; U; Android 4.1.2; en-us; SCH-I535 Build/JZO54K) AppleWebKit/534.30 (KHTML, like Gecko) Version/4.0 Mobile Safari/534.30" "www.random-site.com"
# ...
```

Vậy ta có thể dùng `awk` với `-F '-'` để extract IP.
```
└─$ awk -F '- -' '{print $1}' ./access_log.txt
201.21.152.44 
70.194.129.34 
70.194.129.34 
70.194.129.34 
70.194.129.34 
70.194.129.34 
# ...
```

Tiếp theo, ta cần đếm số lần xuất hiện của mỗi IP. Ta có thể dùng lệnh `uniq`. Lênh `uniq` đươc dùng trích xuất các dòng **liền kề và trùng nhau**. Chẳng hạn ta có 3 dòng liền kề có IP là `10.0.0.1` thì lệnh `uniq` sẽ chỉ show ra 1 dòng duy nhất. Với option `-c` ta có thể đếm số dòng liền kề đó.  

Vậy, trước khi dùng `uniq`, ta cần `sort` các IP để các IP trùng nhau sẽ nằm kề nhau, sau đó dùng `uniq -c` để đếm. Số lần xuất hiện của mỗi IP sẽ được đặt ở trường đầu tiên và IP sẽ là trường thứ 2.
```
└─$ awk -F '-' '{print $1}' ./access_log.txt | sort | uniq -c   
      1 201.21.152.44 
     59 208.115.113.91 
     22 208.54.80.244 
   1038 208.68.234.99 
      8 70.194.129.34 
      8 72.133.47.242 
      8 88.112.192.2 
      8 98.238.13.253 
     21 99.127.177.95
```

Tiếp theo, ta sẽ sort số lần xuất hiện tăng dần với lệnh `sort` sử dụng option `-nr` để sort theo giá trị số và theo thứ tự giảm dần.
```
└─$ awk -F '-' '{print $1}' ./access_log.txt | sort | uniq -c | sort -nr 
   1038 208.68.234.99 
     59 208.115.113.91 
     22 208.54.80.244 
     21 99.127.177.95 
      8 98.238.13.253 
      8 88.112.192.2 
      8 72.133.47.242 
      8 70.194.129.34 
      1 201.21.152.44 
```

Cuối cùng, ta dùng `awk` để show nội dung theo yêu cầu:
```
└─$ awk -F '-' '{print $1}' ./access_log.txt | sort | uniq -c | sort -nr | awk -F ' ' '{print "The IP Address", $2, "has hit", $1}'
The IP Address 208.68.234.99 has hit 1038
The IP Address 208.115.113.91 has hit 59
The IP Address 208.54.80.244 has hit 22
The IP Address 99.127.177.95 has hit 21
The IP Address 98.238.13.253 has hit 8
The IP Address 88.112.192.2 has hit 8
The IP Address 72.133.47.242 has hit 8
The IP Address 70.194.129.34 has hit 8
The IP Address 201.21.152.44 has hit 1
```

## Câu 14
### Description
Hãy cho biết đường đẫn thực thi của 2 lệnh `wget` và `curl`?

### Solution
```
└─$ which wget                                                          
/usr/bin/wget

└─$ which curl
/usr/bin/curl
```

## Câu 15
### Question
Theo bạn, trong 2 lệnh tải về `wget` và `curl`, lệnh nào ưu việt hơn? Giải thích?

### Answer
| | `wget` | `curl` |
|---|---|---|
| Công dụng chính | Tải tài nguyên, thường là file. | Tải tài nguyên và có thể thực hiện 1 số tác vụ khác của 1 web browser. |
| Đặc điểm | Là 1 chương trình độc lập, không phụ thuộc vào thư viện bên ngoài. | Phụ thuộc vào thư viện `libcurl`. |
| | Xử lý việc tỉ file, đặc biệt là trên mạng yếu, bất ổn định tốt. Nhưng chỉ hỗ trợ HTTP, HTTPS và FTP. | Tải file tốt tuy không tối ưu bằng `wget`. Nhưng `curl` hỗ trợ hầu như mội giao thức internet từ FTP, FTPS, HTTP, HTTPS đến IMAP, IMAPS, LDAPS, MQTT, POP3, SMTP,... |
| | Có thể resume aborted downloads. | Không thấy đề cập trong [document](https://everything.curl.dev/). |
| | Không thấy đề cập. | Hỗ trợ URL globbing nên có thể tải nhiều file cùng lúc chỉ với 1 câu lệnh. |

Vậy nếu ta cần tải file 1 cách nhanh chóng, ta nên dùng `wget`. Trong trường hợp giao thức ta sử dụng không được hỗ trợ bởi `wget` hoặc tác vụ cần thực hiện phức tạp hơn, ta nên dùng `curl`.

## Câu 16
### Question
Có thể sử dụng lệnh `curl` để thay đổi các HTTP header được hay không? Nếu được, cho ví dụ?

### Answer
`curl` hỗ trợ thay đổi HTTP header.  

Để thay đổi header ta dùng option `-H` hoặc `--header`, theo sau là 1 chuỗi ở dạng `"Header name: value"`. Nếu ta sử dụng `-H` với 1 header đã được set trước đó thì header này sẽ được cập nhật theo giá trị của chúng ta. Nếu ta sử dụng `-H` với 1 header chưa được set thì `curl` sẽ thêm header này vào request. Ví dụ:
```
curl -H "User-Agent: Edge" -H "X-Forwarded-For: 1.1.1.1" www.site.com
```
## Câu 17-22 : Triển khai ứng dụng chat cơ bản trên hai máy Kali và Windows.
## Câu 17
### Question
Máy nào đóng vai trò là server?

![image](https://user-images.githubusercontent.com/31529599/135111634-3e0ab1e1-6ead-429c-8591-b1598c8e9268.png)

### Answer

Linux listen ở port 4444, đóng vai trò là server.


## Câu 18
### Question
Máy nào đóng vai trò là client?

![image](https://user-images.githubusercontent.com/31529599/135111634-3e0ab1e1-6ead-429c-8591-b1598c8e9268.png)

### Answer

Windows đóng vai trò là client.

## Câu 19
### Question
Nếu khai báo lệnh `nc -lvnp 4444` thì thật chất, port 4444 được mở ở máy nào? 

### Answer
Nếu khai báo lệnh trên thì port 4444 được mở ở máy server (Kali) vì option `-l` là chỉ định netcat listening ở port 4444.

## Câu 20
### Question
Thực hiện chuyển tập tin `wget.exe` trên máy Kali sang máy Windows 10.

### Answer
![image](https://user-images.githubusercontent.com/31529599/135114439-9c1e726a-1052-4815-8a13-20d08f1ce54b.png)

Ở máy Windows, tiến hành listening port 4444 và chuyển tiếp kết quả vào tập tin `incomming.exe`.  
Ở máy Kali, sẽ gởi tập tin `wget.exe` tới máy windows thông qua port 4444.  
Cuối cùng, test thử file đã nhận.

## Câu 21
### Question
Thực hiện lại chi tiết kịch bản Reverse Shell và Bind Shell sử dụng netcat.

### Answer
#### Bind Shell
![image](https://user-images.githubusercontent.com/31529599/135115790-2bb8c7e0-5cc2-4bf9-be41-0c013eb905b2.png)

Ở máy Windows thực hiện lắng nghe tại port 4444 và sử dụng option `-e` để thực thi lệnh `cmd.exe` (mở command prompt) ngay khi có kết nối tới.  
Ở máy Kali, kết nối tới máy windows ở port 4444 và có thể thực thi lệnh từ `cmd` của máy windows.

#### Reverse Shell
![image](https://user-images.githubusercontent.com/31529599/135116634-cf0c7256-4988-4d76-baf6-0af0d303ea4b.png)

Ở máy Kali thực hiện lắng nghe tại port 4444.  
Ở máy Windows thực hiện kết nối tới máy Kali với option `-e` để thực thi lệnh `cmd.exe` (mở command prompt) ngay khi kết nối thành công tới máy Kali.

## Câu 22
### Question
So sánh ưu và nhược điểm khi sử dụng Reverse Shell và Bind Shell? Khi nào nên sử dụng Bind Shell? Khi nào nên sử dụng Reverse Shell?

### Answer
| Bind shell | Reverse shell |
|---|---|
| Victim lắng nghe và attacker sẽ kết nối tới. | Attacker sẽ lắng nghe và victim sẽ kết nối tới. |
| Với cách thiết lập shell này, máy victim luôn up và listening nên ta có thể *ra vào* bất cứ lúc nào. | Ngay khi kết thúc kết nối, victim sẽ thoát khỏi netcat. Nếu ta muốn có lại kết nối, ta phải chạy lại lệnh netcat trên máy victim để kết nối tới máy attacker. |
| Vì bind shell luôn up and listening nên có thể 1 attacker khác nhanh tay hơn và connect tới vicim trước. | Chúng ta sẽ không gặp trường hợp này với reverse shell. |
| Trong 1 số môi trường, inbound traffic sẽ bị block bởi firewall nếu port đích *lạ*. | Vì victim chủ động initiate connection và kết nối ra ngoài nên ít có khả năng bị block bởi firewall hơn. |

Vậy chúng ta nên sử dụng reverse shell trong hầu hết các trường hợp, trừ khi chúng ta có 1 mục đích gì đó cụ thể và cần bind shell thì ta sử dụng bind shell.

## Câu 23
### Question
Thực hiện trao đổi tập tin, bind shell và reverse shell sử dụng PowerShell 

### Answer

![image](https://user-images.githubusercontent.com/31529599/135124226-801918a0-f790-4c74-9650-4174b0011aa3.png)

#### Bind Shell

![image](https://user-images.githubusercontent.com/31529599/135124372-e4211462-9991-4f50-8bf0-795c46c9e8fc.png)

#### Reverse Shell

![image](https://user-images.githubusercontent.com/31529599/135124650-10c5e588-f41a-4940-978d-0bee14a0dec0.png)


