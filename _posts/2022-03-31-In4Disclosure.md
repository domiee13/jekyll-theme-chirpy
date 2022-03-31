---
title: Information disclosure vulnerabilities
date: 2022-03-31 11:00:00 +0700
categories: [Blog, PortSwigger]
tags: [portswigger, information_disclosure]     # TAG names should always be lowercase
---

# Information disclosure vulnerabilities

## Infromation disclosure là gì

- Thông tin bị tiết lộ hay rò rỉ khi website vô tình tiết lộ thông tin nhạy cảm cho người dùng
- Tùy vào hoàn cảnh, trang web có thể để lộ nhiều loại thông tin, bao gồm
    - Dữ liệu về các người dùng khác (username, thông tin tài chính,. . .)
    - Dữ liệu kinh doanh hoặc thương mại
    - Chi tiết về công nghệ, kĩ thuật được sử dụng trên trang web và cơ sở hạ tầng của nó

## Một vài ví dụ về Information Disclosure

- Tiết lộ tên của các thư mục ẩn, cấu trúc và nội dung của chúng từ file robots.txt hoặc danh sách thư mục
- Cung cấp quyền truy cập vào source code thông qua các bản sao lưu tạm thời (temporary backups)
- Đề cập đến tên bảng hoặc tên cột trong databases trong thông báo lỗi
- Hard code API keys, địa chỉ IP, thông tin đăng nhập databases trong source code
- Gợi ý về sự tồn tại hoặc không của tài nguyên, tên người dùng, v.v. thông qua sự khác biệt nhỏ trong thông báo, phản hồi của ứng dụng. Ví dụ thực tế ở dưới =)))

![Untitled](/assets/img/In4Disclosure/Untitled.png)

## Cách mà lỗ hổng chít tịt này phát sinh ?

- Quên xóa nội dung nội bộ khỏi nội dung công khai. Ví dụ: Comment của dev có thể hiển thị cho người dùng
- Cấu hình thiếu hoặc cấu hình sai trang web và các công nghệ liên quan. Ví dụ: Không tắt tính năng debug : D
- Lỗ hổng trong thiết kế và phát triển phần mềm: Ví dụ: Trả về thông báo lỗi khác nhau cho chức năng đăng nhập: “Sai tên đăng nhập” và “Sai mật khẩu” thay vì “Tên đăng nhập HOẶC mật khẩu sai”

## Ảnh hưởng của lỗ hổng này ?

- Lỗ hổng có thể tác động trực tiếp và gián tiếp đến trang web tùy thuộc vào mục đích của trang web, kẻ tấn công có thể thu thập được thông tin nào đó
- Trong một số trường hợp, chỉ riêng việc tiết lộ thông tin nhạy cảm cũng gây ảnh hưởng nghiêm trọng. Ví dụ: Một trang web thương mại điện tử làm lộ dữ liệu thẻ tín dụng của khách hàng, ...
- Mặt khác, thông tin kĩ thuật bị rò rỉ như cấu trúc thư mục, thông tin về các công nghệ, framework đang được sử dụng có thể là thông tin quan trọng, một “mảnh ghép còn thiếu” để kẻ tấn công tận dụng, hoàn thiện kịch bản tấn công hoặc mở ra nhiều attack vector (hướng tấn công) khác. Trong trường hợp này, mức độ nghiêm trọng của lỗ hổng phụ thuộc vào những gì mà kẻ tấn công có thể làm với thông tin bị rò rỉ ( với mình thì chắc vô dụng =))) )

## Cách khai thác lỗ hổng Information Disclosure

Phần này khá dài nên có lẽ mình sẽ viết trong bài tiếp theo

## Ngăn chặn/khắc phục lỗ hổng này?

Việc ngăn chặn hoàn toàn lỗ hổng này là một việc khó khăn do có nó có thể phát sinh theo nhiều cách khác nhau. Dù vậy, chúng ta hoàn toàn có thể sử dụng những cách sau đây để hạn chế được lỗ hổng Information Disclosure:

- Đầu tiên là con người ( Lỗ hổng lớn nhất của bất kì hệ thống nào :^ ). Đảm bảo rằng tất cả mọi người tham gia vào phát triển trang web đều nhận thức được thông tin nào là thông tin nhạy cảm. Đôi khi những thông tin tưởng chừng rất đơn giản nhưng lại cực kì hữu ích cho kẻ tấn công :^
- Sử dụng những thông báo chung càng nhiều càng tốt, không cung cấp bất kì “hint” nào cho kẻ tấn công
- Kiểm tra kỹ để đảm bảo rằng mọi tính năng gỡ lỗi, chẩn đoán đã được tắt
- Đảm bảo  hiểu đầy đủ cách cấu hình và ý nghĩa bảo mật của bất kỳ công nghệ bên thứ ba nào mà bạn triển khai. Dành thời gian để tìm hiểu và tắt bất kỳ tính năng và cài đặt nào mà bạn không thực sự cần.
