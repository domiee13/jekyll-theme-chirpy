---
title: hackthebox- misc - misDIRection Writeup
date: 2021-03-25 20:30:00 +0700
categories: [Writeup, hackthebox]
tags: [misc, writeup]     # TAG names should always be lowercase
---

# hackthebox - Misc - misDIRection

*Link: https://app.hackthebox.eu/challenges/55*

Sau khi download và giải nén ta nhận được 1 folder .secret như sau

![](/assets/img/hackthebox/miscDIR1.png)
Mình check thử 1 vài thư mục con

![](/assets/img/hackthebox/miscDIR2.png)

Dùng lệnh tree để xem tổng quan cấu trúc thư mục:
![](/assets/img/hackthebox/miscDIR3.png)

Ban đầu mình viết 1 script python dùng thư viện [glob](https://docs.python.org/3/library/glob.html) để liệt kê hết tên thư mục ra và đây là kết quả:
```
./0/6
./1/22
./1/30
./2/34
./5/16
./9/36
./B/23
./C/4
./D/26
./E/14
./F/19
./F/2
./F/27
./J/8
./N/11
./N/25
./N/31
./N/33
./R/3
./R/7
./S/1
./U/9
./V/35
./X/17
./X/21
./X/29
./d/13
./e/5
./j/10
./j/12
./p/32
./s/24
./u/20
./u/28
./x/15
./z/18
```
Sau đó mình thử ghép các chữ số ở cuối thành 1 dãy số:
```
6 22 30 34 16 36 23 4 26 14 19 2 27 8 11 25 31 33 3 7 1 9 35 17 21 29 13 5 10 12 32 24 20 28 15 18
```
Và sau đó là betak =)))\
Okay quay xe, mình xem xét chuỗi kia và quyết định làm ngược lại, nghĩa là mình sẽ thử sắp xếp tên thư mục ở đầu theo thứ tự tăng dần của tên file trong thư mục (dãy số ở cuối).
```
import glob

path = './*/*'
files = glob.glob(path)

l = []
for name in files:
    l.append(name[2:])
dct ={}
for s in l:
    dct[int(s.split("/")[1])]=s.split("/")[0]
sorted_key = sorted(dct.keys())

for i in sorted_key:
    print(dct[i],end="")
```
Sau khi chạy script sẽ được 1 chuỗi:
```
SFRCe0RJUjNjdEx5XzFuX1BsNDFuX1NpN2V9
```
Một thói quen của mình là khi thấy 1 chuỗi như vậy việc đầu check thử chiều dài của chuỗi xem có chia hết cho 4 không, nếu có khả năng cao nó là base64 xDD

![](/assets/img/hackthebox/miscDIR4.png)

Okay, mình dùng [CyberChef](https://gchq.github.io/CyberChef/) giả mã và nhận được flag, flag là gì thì mình không nói :^)
```
Flag: HTB{DIR3ctLy_*************}
```
