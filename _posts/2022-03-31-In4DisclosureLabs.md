---
title: Information Disclosure Labs
date: 2022-03-31 20:00:00 +0700
categories: [Writeup, PortSwigger]
tags: [information_disclosure]     # TAG names should always be lowercase
---

# Information Disclosure Labs

## **Lab: Information disclosure in error messages**

---

![Untitled](/assets/img/In4DisclosureLabs/Untitled.png)

Giao diện trang web

![Untitled](/assets/img/In4DisclosureLabs/Untitled%201.png)

Ta thấy trang web sử dụng GET request với parameter productId=2 để truy xuất thông tin chi tiết của một sản phẩm

Thử thay thế giá trị hợp lệ thành một giá trị với kiểu dữ liệu khác

![Untitled](/assets/img/In4DisclosureLabs/Untitled%202.png)

Ta thấy trang web trả lại thông báo lỗi kèm cả vesion của apache cho chắc chắn :^

![Untitled](/assets/img/In4DisclosureLabs/Untitled%203.png)

![Untitled](/assets/img/In4DisclosureLabs/Untitled%204.png)

---

## **Lab: Information disclosure on debug page**

![Untitled](/assets/img/In4DisclosureLabs/Untitled%205.png)

Lần này, chúng ta cần lấy được SECRET_KEY

Check qua source code của trang web, ta thấy 1 comment, hàng về hàng về

![Untitled](/assets/img/In4DisclosureLabs/Untitled%206.png)

Truy cập url và tìm được SECRET_KEY

![Untitled](/assets/img/In4DisclosureLabs/Untitled%207.png)

![Untitled](/assets/img/In4DisclosureLabs/Untitled%208.png)

---

## **Lab: Source code disclosure via backup files**

![Untitled](/assets/img/In4DisclosureLabs/Untitled%209.png)

Check file robots.txt

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2010.png)

Truy cập /backup

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2011.png)

Ta có file backup [ProductTemplate.java](http://ProductTemplate.java)

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2012.png)

Pass của db được hard code trong file

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2013.png)

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2014.png)

---

## **Lab: Authentication bypass via information disclosure**

![Untitled](/assets/img/In4DisclosureLabs/Untitled%2015.png)

Đang cập nhật. . .
