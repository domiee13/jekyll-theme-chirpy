---
title: Đừng chơi Bug bounty, chạy, chạy ngay đi!!
date: 2022-08-11 12:00:00 +0700
categories: [Blog]
tags: [bug_bounty]     # TAG names should always be lowercase
---

## Bug bounty là gì?

## Mindset

*Mindset, hay cách giữ cho tình thần của bạn ổn định sau khi bị duplicate và tiếp tục gõ các program*

Nếu bạn mới bắt đầu CHƠI bug bounty, nên xác định tinh thần trước rằng sẽ mất ( rất nhiều ) thời gian để có thể CHƠI được bug bounty hoặc là bug bounty sẽ CHƠI bạn mỗi ngày. Bạn sẽ cần có kiên nhẫn, quyết tâm và đam mê, đam mê, rất nhiều đam mê ( Điều quan trọng nhắc lại 3 lần ). Đây là một lĩnh vực cực kỳ cạnh tranh, đòi hỏi đam mê, chăm chỉ, tư duy tốt để có thể duy trì và phát triển được. 

> Đối với một số người, quá trình tìm bug bounty có thể bắt đầu rất chậm và cũng có những người tìm ra lỗi ngay sau khi bắt đầu. Một điều quan trọng cần nhớ khi tìm bug bounty là đừng chán nản, khó chịu nếu bạn mất nhiều thời gian hơn để tìm thấy lỗi hợp lệ. Không phải ai cũng tìm thấy lỗi mỗi khi họ ngồi xuống và hack. Việc tìm ra lỗi rất phổ biến trong nhiều ngày, vài tuần hoặc thậm chí vài tháng. Đừng so sánh thành công hay thất bại của chính bạn với người khác. Bởi vì cũng như bất cứ điều gì khác, sẽ luôn có người tốt hơn bạn và người khác kém hơn bạn. Vì vậy, đặt ra các mục tiêu của riêng bạn và làm việc để đạt được chúng có thể rất quan trọng. ( Tommy “dawgyg” DeVoss )
> 

Ngoài làm suy sụp tinh thần của một số người thì bài học và kiến thức là phần thưởng duy nhất mà bạn sẽ luôn nhận được và nằm trong tầm kiểm soát của bạn. Vì vậy, nếu bạn là người mới bắt đầu, bạn nên đặt mục tiêu tìm hiểu về các lỗ hổng và kỹ thuật khai thác chúng hơn là kiếm được bao nhiêu tiền.

## Học gì để CHƠI

Nói chung là rất nhiều thứ cần học, và việc học là việc cả đời vì đặc thù của ngành: Mọi thứ đang thay đổi từng giây, ngủ dậy cái cũng có thể thành người tối cổ ngay, đi tù hay bị băt cóc chục năm thì mình không biết ¯\_(ツ)_/¯. Bài này mình chỉ tập trung vào học gì để săn bug bounty trên các web application.

**Kiến thức ứng dụng web cơ bản**

- Cách request hoạt động
- HTTP headers
- JSON requests
- Cách browser hoạt động
- Cách ứng dụng giao tiếp và gửi dữ liệu với server

**Những lỗ hổng phổ biến ( Top 10 OWASP)**

Bạn sẽ cần hiểu rõ về nguyên nhân tồn tại (do sai sót gì, trong các chức năng nào), cách khai thác, ngăn chặn/giảm thiểu [**biết cách ngăn chặn sẽ nghĩ ra cách bypass ( ͠° ͟ʖ ͡°)** ] những lỗ hổng phổ biến như Remote Code Execution (RCE), Cross Site Request Forgery (CSRF), Cross Site Scripting (XSS), Injeciton (SQL injeciton, Command injection, … ), …. Bản thân mình khuyên tìm hiểu từng lỗ hổng, tái hiện lại lỗ hổng và cách khai thác lỗ hổng. 

**Read blogs.** Learn new techniques from other bug bounty hunters so that you can test it out during your testing.

> If you are new to Bug Bounty program, you might not feel confident that you can find something a public program. This is something that a lot of hackers are struggling with. If you haven’t found a lot of security vulnerabilities yet, it might payoff to practice on Capture The Flag (CTF). Exploiting something for the first time is difficult and eye-opening. Apply the same structure if you would apply when looking in real targets as this help you a build a solid foundation and will help you to become an amazing hacker. Use bug bounty as a way to expand your knowledge and not as a race. Write simple scripts and use available tools to expand the process of expanding attack surface [...] Understand the web application and figure out what assets the web application are trying to protect. Think like an engineer of the web application. (Jobert Abma, Hackerone Cofounder)
> 

**Đọc blog:** Học những công nghệ mới từ những bug bounty huntrer khác, từ đó có thể áp dụng vào chính chương trình, dự án của mình. Bản thân mình đọc bounty writeup của người khác rất nhiều, cố gắng suy nghĩ và sao chép mindset của họ ( ͠° ͟ʖ ͡°), nghĩ xem tại sao họ tìm thấy lỗi đấy mà mình không tìm được :(. Mỗi khi thấy 1 lỗi thú vị, mình thường thử áp dụng vào các target hiện tại của mình.

> Nếu bạn là một người mới, mình khuyên bạn nên chơi CTF ( tất nhiên là đừng để CTF chơi bạn ). Chơi CTF có thể giúp bạn luyện tập phản xạ, nâng “sense” của mình lên ( cách tiếp cận target, tính năng nào thường bị lỗ hổng nào )
> 

**Học cách tạo ra một trang web/ứng dụng:** Bạn cần biết cách mà một ứng dụng web được tạo ra trước, sau khi đã hiểu cách mà mọi thứ được tạo ra và hoạt động, bạn sẽ tìm ra cách để khai thác cũng như cách phòng chống, từ cách phòng chống lại nghĩ ra cách bypass ( ͠° ͟ʖ ͡°).

## Phương pháp CHƠI

### Pick target

Tìm một target ngon sẽ phụ thuộc vào những yếu tố sau:

**Ngày công bố chương trình**

Nên tập trung vào những chương trình mới được công bố, thay vì những chương trình cũ đã được các bounty hunter khác vọc nát rồi :^. Thỉnh thoảng mình vẫn chọn program cũ vì ai cũng nghĩ nó cũ nên không đụng vào =))) vì một số yếu tố nữa mà mình sẽ đề cập ngay dưới

**Phản hồi**

Thời gian phản hồi và cách phản hồi cũng là một tiêu chí để mình đánh giá chương trình có thơm hay không =)). Nếu một chương trình phản hồi chậm hay thiếu chuyên nghiệp, “lươn lẹo” giảm impact vô lý thì mình sẽ skip. Thường thì mình sẽ “thử lửa” bằng cách submit 1 lỗi P5 để xem thời gian phản hồi và cách họ phản hồi ra sao để quyết định có nên theo và đào sâu target hơn không.

**Scope (Phạm vi của chương trình)**

Phạm vi của chương trình càng lớn càng tăng khả năng lỗi không bị duplicate

**Bạn có cảm thấy hứng thú với program đó không?**

Với mình, đây là cái quan trọng nhất. Việc bạn hứng thú hay không sẽ ảnh hưởng rất lớn đến năng suất làm việc của bạn, khi hứng thú thì bạn sẽ đầu tư thời gian và tâm huyết với nó. Vậy nên đừng cố gắng ôm một cái program mà bạn không yêu, đau khổ lắm 💔 

**Tiền thưởng**

Cái này thì tùy mỗi người, ai làm vì đam mê thì skip nhé =)))))). Tiền thưởng lỗi cũng nên là một tiêu chí để bạn quyết định gõ nó hay không. Không ai muốn tìm sml ra 1 cái P1 được trả tiền bằng cái P3 ở program khác, factos ( ͠° ͟ʖ ͡°)

### Cách tiếp cận một target

Cách mà mình tiếp cận và recon một em hàng ngọt nước. Cái này chỉ để tham khảo thôi (và mình cũng muốn chia sẻ nữa :3 ), vì có n+1 cách ( n thuộc N*) khác

Mình sẽ lấy một program làm ví dụ để dễ hình dung cách mình recon hơn. Đây cũng là dạng program mà mình thích ( nhiều nước, lộn, nhiều subdomain )

![Untitled](/assets/img/bugbounty/Untitled.png)

Sau khi đọc qua phần Chính sách, Out-of-scope thì mình sẽ ngó qua Scope, Scope nhiều thế này thì phải vụt. ( program này là VDP, nôm na là sẽ không có tiền, nhưng nếu bạn mới tham gia bug bounty thì cứ thử và tận hưởng cảm giác duplicate đi )

Không lòng vòng nữa, đầu tiên khi thấy một đống subdomain thế này, mình sẽ dùng `amass` để liệt kê toàn bộ subdomain, và dùng `httpx` để check xem subdomain nào còn sống

```jsx
amass enum -d domain | httpx -title -status-code
```

Kí tự “|” để mình chain 2 câu lệnh với nhau, đại khái nó sẽ lấy đầu ra câu lệnh trước làm đầu vào cho câu lệnh 
tiếp theo, muốn hiểu rõ hơn thì bạn nên làm 1 khóa linux cơ bản :^ 

Sau khi có list các subdomain còn sống, mình sẽ đi sâu vào từng subdomain 1:

- Xem qua các công nghệ mà trang web đang sử dụng
- Google dorking
- Dirsearch/ffuf
- Sử dụng `JSFinder` để kiểm tra xem có thông tin nhạy cảm bị lộ không
- Rà quét trang web sử dụng `Nuclei`
- Liệt kê các endpoint, chức năng của trang web, hiểu rõ nghiệp vụ của từng chức năng. Dạo gần đây mình hay sử dụng `gau` (get all url) để list ra các url của trang web.

Well, sơ sơ cũng chỉ vậy thôi, còn đi sâu vào từng chức năng thì test theo check list, hoặc làm nhiều bạn sẽ tự biết chức năng nào thường hay dính lỗi nào 

¯\_( ͡° ͜ʖ ͡°)_/¯

### Focus vào cái gì ?

Cái này cần câu cơm nên mình không share đâu 🐧

## Tips

**Gitlab**

- Ưu tiên những lỗi nghiêm trọng (P1)
    - Không ai muốn dành nhiều thời gian để phân tích những lỗi Low
- Lắng nghe, xem xét phản hồi của các bên liên quan, đôi lúc nó có thể giúp ích
    - Mình từng tìm được 1 lỗi P5, và ông verify đã rep lại khá nhiệt tình, gợi ý cho mình các attack vector để có thể nâng impact của lỗ hổng lên
        
        ![Untitled](/assets/img/bugbounty/Untitled%201.png)
        
- Sử dụng công cụ tự động hóa ( Bản thân mình không khuyến khích, công cụ ai cũng có thể dùng và quét ra được )

**Portswigger**

- Hiểu quy trình, nghiệp vụ của mục tiêu
    - Tập trung vào 1 loại lỗ hổng cụ thể ( Và kiểm tra lần lượt từng loại lỗ hổng )
        - Đọc các writeup, report về loại lỗ hổng đó
        - Tập trung vào tìm loại lỗ hổng này trên mục tiêu của bạn
    - Làm quen với ứng dụng, hiểu được nghiệp vụ, luồng, tính năng của ứng dụng
    - Tập trung tìm hiểu cách mọi thứ hoạt động **thay vì chạy các công cụ tự động**
- Tìm lỗ hổng ở những vị trí chưa có/ít người quan tâm
    - Chọn 1 program cũ, bounty nhỏ
    - Program có scope rộng ( nhiều subdomain, domain )
- Không ngừng học hỏi ( Đọc writeup, bug bounty report, blog, phân tích 1-day, … )
- Kiểm tra các attack vector không phổ biến
- Thực hiện các hành động không mong muốn (không gửi những gì ứng dụng, người phát triển mong muốn ) Thay vào đó, nghĩ về những điều mà mấy ông dev không nghĩ đến, không xem xét, bỏ sót.

**Zwink**

- Coi Bug bounty như 1 game nhập vai ( nghe hơi ảo game nhưng theo mình hiểu ý của Zwink là enjoy nó, vì bằng cách này hay cách khác, nó sẽ up level của bạn, và đừng buồn khi bị dup :)) Nó là điều tất yếu, bạn không bị dup thì tôi bị dup, và ngược lại. Luôn có người bị dup :)) )
- Học trên Portswigger Academy và tìm hiểu về các lỗ hổng hệ thống phân loại lỗ hổng của BugCrowd (BugCrowd VRT)
- Kiếm lỗ hổng valid đầu tiên ( P4 cũng ổn, P3, P2, P1 thì càng ok ) Quan trọng là nó sẽ giúp bạn có thêm động lực, có thêm cơ hội được mời vào private program ( đỡ cạnh tranh hơn )
- Test tay để tránh bị trùng lỗ hổng, sử dụng VPN phòng trường hợp bị firewall block
- Sau khi quen rồi thì tập trung vào tìm các lỗ hổng ở mức cao hơn

## Tài nguyên

Một bài mình thấy tổng hợp khá đủ: 

[Gold Bug Bounty Resources in 2022](https://shubhdhungana.medium.com/gold-bug-bounty-resources-web-application-android-ios-security-dc88bfb24eb)

Youtube (Nói chung tùy người, bạn thấy hợp ai thì xem người đó)

- **[LiveOverflow](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w)**
- **[Bugcrowd](https://www.youtube.com/channel/UCo1NHk_bgbAbDBc4JinrXww)**
- [**InsiderPhD**](https://www.youtube.com/c/InsiderPhD)
- **[Nahamsec](https://www.youtube.com/channel/UCCZDt7MuC3Hzs6IH4xODLBw)**
- **[STÖK](https://www.youtube.com/channel/UCQN2DsjnYH60SFBIA6IkNwg)**
- **[SecurityIdiots](https://www.youtube.com/channel/UCPPAYs04kwfXcHnerm_ueFw)**
- [**Z-winK University (ZU) - Bug Bounty Education**](https://www.youtube.com/channel/UCDl4jpAVAezUdzsDBDDTGsQ)
- [**Hack 'Em All**](https://www.youtube.com/c/HackEmAll-Live)
- [**John Hammond**](https://www.youtube.com/c/JohnHammond010)
- [**CyberJutsuTV**](https://www.youtube.com/c/CyberJutsuTV)

### Cơm thêm

[https://github.com/bobby-lin/study-bug-bounty](https://github.com/bobby-lin/study-bug-bounty)