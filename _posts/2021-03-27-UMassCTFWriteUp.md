---
title: UMassCTF'21 - Web - Hermit-Part 1 Writeup
date: 2021-03-29 6:00:00 +0700
categories: [Writeup, UMassCTF'21]
tags: [web, writeup]     # TAG names should always be lowercase
---
# UMassCTF'21 - Web - Hermit-Part 1

![](/assets/img/UMassCTF'21/1.jpg)

Truy cập vào trang web bằng 1 trong 2 link, đây là giao diện của trang web:

![](/assets/img/UMassCTF'21/2.jpg)

Nhìn qua thì mình khá chắc đây là File Upload Attacks, chúng ta sẽ phải upload file reverse shell lên webserver. Theo kết quả của Wappalyzer mình biết được rằng hệ thống của web được code bằng PHP

![](/assets/img/UMassCTF'21/3.jpg)

Vậy nếu chúng ta có thể upload 1 file reverse shell được viết bằng PHP lên, tìm nơi chứa file đó và chạy được file, chúng ta sẽ có reverse shell. Bạn có thể tìm hiểu thêm về reverse shell ở [đây](https://viblo.asia/p/hieu-ro-ve-reverse-shells-LzD5ddE45jY). Mình chỉ giới thiệu bài viết bằng tiếng Việt vì tiếng Anh google cái ra rất nhiều xD. Tất nhiên mình vẫn khuyến khích các bạn đọc tài liệu tiếng Anh.

Okay, quay lại chủ đề chính, mình sử dụng reverse shell php ở [đây](https://github.com/pentestmonkey/php-reverse-shell)

Đây là lúc mình nhận ra thực tế và những bài mình làm trên Tryhackme hay hackthebox khác hoàn toàn. Ở Tryhackme hay hackthebox máy bạn và máy cần tần công nằm trong cùng 1 mạng, việc tấn công có thể dễ dàng hơn xD. Còn ở đây thì khác hoàn toàn. Mình loay hoay 1 hồi rồi nhớ ra [ngrok](https://ngrok.com/). Ngrok là công cụ tạo đường hầm (tunnel) giữa localhost của bạn và internet, giúp người khác có thể truy cập được localhost thông qua custom domain của ngrok.

Cài đặt ngrok và mở 1 cổng với giao thức TCP

```
./ngrok tcp 666
```
Mở cổng 666 với giao thức TCP, mở thành công sẽ hiển thị như sau\
![](/assets/img/UMassCTF'21/5.jpg)

Sau đó mở port 666 để "nghe" với netcat

```
nc -lvnp 666
```

Xong xuôi hết, việc cuối cùng là chỉnh sửa file php reverse shell

Có 2 giá trị ở đây cần thay đổi, đó là ip và port
![](/assets/img/UMassCTF'21/6.jpg)

Port là cổng mình đã mở ở trên, còn ip là 2.tcp.ngrok.io (Giá trị của trường Forwarding trong thông báo của ngrok ở trên)

Chỉnh sửa xong xuôi, việc tiếp theo là upload file lên, và oops :^(

![](/assets/img/UMassCTF'21/7.jpg)

Có thể thấy webserver đã chặn không cho mình upload file đuôi php lên, nicetry :^. Mình thử bypass filter đấy bằng cách thêm đuôi .jpg vào và trông nó sẽ như thế này xD

![](/assets/img/UMassCTF'21/8.jpg)

Okay, thử upload lại và mình đã upload thành công

![](/assets/img/UMassCTF'21/9.jpg)

Click vào See Image và mình lấy được reverse shell

![](/assets/img/UMassCTF'21/11.jpg)

Okay, theo kinh nghiệm chơi mấy room trên tryhackme, mình tìm thử trong thư mục home đầu tiên

![](/assets/img/UMassCTF'21/12.jpg)

Bước cuối :))

![](/assets/img/UMassCTF'21/13.jpg)

Ngoài lề tý, mình có để lại lời nhắn và có 1 ông nào đó đáp lại, khá vui =)))) Niềm vui nho nhỏ trong niềm vui to :^. Chall này giúp mình học thêm được khá nhiều thứ xD.

![](/assets/img/UMassCTF'21/14.jpg)
