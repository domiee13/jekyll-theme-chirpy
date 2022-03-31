---
title: UMassCTF'21 - Web - heim Writeup
date: 2021-03-29 6:00:00 +0700
categories: [Writeup, UMassCTF'21]
tags: [web, writeup]     # TAG names should always be lowercase
---
# UMassCTF'21 - Web - heim

![](/assets/img/UMassCTF'21/15.jpg)

Giao diện của trang web

![](/assets/img/UMassCTF'21/16.jpg)

Mình thử nhập 1 cái tên bất kì và ấn enter

![](/assets/img/UMassCTF'21/17.jpg)

Okay, mình được cấp 1 access token, nhưng để làm gì thì không ai nói :^(

Mình thử fuzz trang web để tìm các thư mục con/file trong trang web bằng [ffuf](https://github.com/ffuf/ffuf#installation). Chi tiết như nào các bạn có thể tìm hiểu thêm tại đây [Fuzzing web với FFUF](https://viblo.asia/p/fuzzing-web-voi-ffuf-LzD5dekwKjY). Thực ra có nhiều cách để làm việc này như dirbuster, dirsearch, . . . nhưng mình vừa học trên [hackthebox academy](https://academy.hackthebox.eu/course/preview/attacking-web-applications-with-ffuf/web-fuzzing) cách này nên muốn thử :^.

```
ffuf -u http://104.197.195.221:8081/FUZZ -w directory-list-2.3-medium.txt
```

Ngon lành :^

![](/assets/img/UMassCTF'21/18.jpg)

Truy cập đường link nhưng . . .

![](/assets/img/UMassCTF'21/19.jpg)

Có lẽ đây là lúc mình dùng access token được cấp :^ Loay hoay 1 hồi cuối cùng mình dùng curl

![](/assets/img/UMassCTF'21/20.jpg)

Và nó báo token hết hạn =)) Chắc tại mình google hơi lâu

Lấy 1 access token mới và thử lại thì mình nhận được

![](/assets/img/UMassCTF'21/21.jpg)

Oke, mình không xứng đáng, chỉ có Odin mới có thể xem flag xD

Và nhân danh bộ râu của Odin, mình gõ tên Odin để lấy access token :^

![](/assets/img/UMassCTF'21/22.jpg)

Doneeeeee, flag là gì thì mình vẫn không nói nhé (¬‿¬)
