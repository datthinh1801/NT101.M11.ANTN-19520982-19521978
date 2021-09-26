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

Với option `-l` để liệt kê các ports mà máy đang lắng nghe, `-u` để liệt kệ các UDP sockets và `-t` để liệt kê các `TCP sockets. Cuối cùng, `-n` để show địa chỉ IP mà không cần phân giải tên miền. Việc này sẽ giúp giảm thời gian thực thi của câu lệnh.

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
- Vì lịch sử câu lệnh được lưu trên file, nên ta có thể xóa hoặc làm rỗng file này sau mỗi lần sử dụng. Một cách nhanh gọn là sử dụng option `-c` của chính câu lệnh `history`:` history -c`.
- Cấu hình shell. Để cấu hình shell, ta mở file cấu hình (file cấu hình thường có tên là `.<shell>rc` nằm tại thư mục  home của người dùng, ví dụ trên Kali sẽ là `/home/kali/.zshrc`) và set giá trị cho `HISTSIZE=n` với `n` là số câu lệnh ta muốn lưu. Để không lưu lịch sử thì ta set `HISTSIZE=0`.

## Câu 9
### Question
Ngoài cách sử dụng tiện ích history expansion, còn cách nào để thực hiện lại các lệnh đã nhập một cách nhanh chóng hay không? Nếu có, hãy mô tả cách làm.

### Answer

## Câu 10
### Question
Như đã biết, khi sử dụng toán tử `>` để xuất kết quả vô tập tin, nếu tập tin đã tồn tại, nội dung trong tập tin sẽ bị thay thế bằng nội dung mới. Vậy, có cách nào để hoàn tác lại quá trình này hay không? Nếu có, hãy mô tả cách làm.

### Solution

## Câu 11
### Description
Sử dụng lệnh `cat` cùng với lệnh `sort` để sắp xếp lại nội dung của tập tin `/etc/passwd`, sau đó lưu kết quả vào một tập tin mới có tên `passwd_new` và thực hiện đến số lượng dòng có trong tập tin mới.

### Solution
Đầu tiên, ta đọc file `/etc/passwd`, sau đó pipeline sang lệnh `sort` để sắp xếp lại nội dung. Sau đó, ta redirect nội dung đã sắp xếp vào file `passwd_new` với redirection operator `>`. Cuối cùng, ta pipeline nội dung đã sắp xếp vào lệnh `wc` với option `-l` để đêm số dòng.
```
└─$ cat /etc/passwd | sort > password_new | wc -l
```
