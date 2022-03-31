---
title: W3Challs - Web - Authentication Writeup
date: 2021-03-24 19:45:00 +0700
categories: [Writeup, W3Challs]
tags: [web, writeup]     # TAG names should always be lowercase
---

# W3Challs - Web - Authentication

*Link: https://w3challs.com/challenges/web/authentication*

![problem](/assets/img/screenImg/1.png)

Truy cập [link](http://authentication.hax.w3challs.com/)

![Administration page](/assets/img/screenImg/2.png)

Mình click thử vào [Administration](http://authentication.hax.w3challs.com/index.php?page=admin) và trang web báo lỗi "Forbidden Access! This part of the site is reserved to the admin!" 

![Administration page error](/assets/img/screenImg/3.png)

Check cookie của trang web và mình thấy 1 cookie với tên name và giá trị "b14361404c078ffd549c03db443c3fede2f3e534d73f78f77301ed97d4a436a9fd9db05ee8b325c0ad36438b43fec8510c204fc1c1edb21d0941c00e9e2c1ce2"

![Cookie](/assets/img/screenImg/4.png)


Sử dụng hash-identifier để xác định định dạng của chuỗi giá trị kia:

![hash-identifier](/assets/img/screenImg/5.png)

Và mình được kết quả:
![hash-identifier result](/assets/img/screenImg/6.png)

Okay, thử crack trên [CrackStation](https://crackstation.net/) được kết quả là chuỗi "user" :

![CrackStation result](/assets/img/screenImg/7.png)

Mã hóa SHA-512 cho chuỗi "admin":

```
Sha512(admin) = c7ad44cbad762a5da0a452f9e854fdc1e0e7a52a38015f23f3eab1d80b931dd472634dfac71cd34ebc35d16ab7fb8a90c81f975113d6c7538dc69dd8de9077ec
```

Sử dụng chuỗi đã mã hóa SHA-512 của "admin" thay cho chuỗi giá trị có sẵn và tải lại trang và lấy được flag xD