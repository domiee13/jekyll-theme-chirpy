---
title: CyberJutsu Upload File Challenge
date: 2022-05-19 11:00:00 +0700
categories: [Writeup]
tags: [writeup, upload_file]     # TAG names should always be lowercase
---
# CyberJutsu UploadFile

---

## Level 1

Source code của level 1

```php
<?php
    error_reporting(0);

    // Create folder for each user
    session_start();
    $dir = 'upload/' . session_id();
    if ( !file_exists($dir) )
        mkdir($dir);

    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        $error = '';
        $success = '';
        try {
            $file = $dir . "/" . $_FILES["file"]["name"];
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Đoạn code trên sẽ thực hiện tạo một đường dẫn tạm thời bằng cách nối chuỗi “upload” với session id của người dùng. Biến $_FILES là một biến mảng toàn cục của PHP, lưu toàn bộ thông tin về file upload. Sau khi check xem `$_FILES["file"]` đã được khởi tạo chưa, chương trình sẽ lưu file trong thư mục tạm thời đã tạo ở trên và đưa ra đường link đến file vừa upload.

Tạo file test.php với nội dung

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled.png)

Thực hiện upload file test.php, ta thấy trang web báo thành công và trả về đường link đến file vừa upload

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%201.png)

Click vào đường link trên, ta thấy file php được thực thi và trả về kết quả

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%202.png)

Thay đổi nội dung file, thực hiện upload và truy cập đường link, trang web trả về kết quả của câu lệnh `whoami`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%203.png)

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%204.png)

---

## Level 2

Source code của level 2:

```php
<?php
    error_reporting(0);

    // Create folder for each user
    session_start();
    if (!isset($_SESSION['dir'])) {
        $_SESSION['dir'] = 'upload/' . session_id();
    }
    $dir = $_SESSION['dir'];
    if ( !file_exists($dir) )
        mkdir($dir);

    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        $error = '';
        $success = '';
        try {
            $filename = $_FILES["file"]["name"];
            $extension = explode(".", $filename)[1];
            if ($extension === "php") {
                die("Hack detected");
            }
            $file = $dir . "/" . $filename;
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Đoạn code trên sẽ thực hiện tách tên file bằng hàm [explode](https://www.php.net/manual/en/function.explode.php). Hàm explode là một hàm xử lý chuỗi trong php, dùng để tách 1 chuỗi được phân tách với nhau bằng 1 kí tự (trong đoạn code trên là kí tự `"."` ) và trả về 1 mảng những chuỗi đã được phân tách. Ví dụ:

```php
$a = "he.llo.wor.ld";
var_dump(explode(".",$a));
//Return array(4) {
//  [0]=>
//  string(2) "he"
// [1]=>
//string(3) "llo"
//[2]=>
//string(3) "wor"
//[3]=>
//string(2) "ld"
//}
```

Sau khi tách chuỗi, chương trình sẽ check xem chuỗi ở vị trí thứ 1 trong mảng có phải .php không, nếu có sẽ dừng chương trình và in ra “Hack detected”

Bypass bằng cách thêm 1 đuôi file nữa vào (ở đây mình thêm đuôi .png) , khi này, mảng `$extension` sẽ có giá trị `[”ten_file”,”png”,”php”]` và biến `$extension` sẽ có giá trị “png”

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%205.png)

Upload file và truy cập đường dẫn

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%206.png)

Trang web hiển thị kết quả của câu lệnh `whoami`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%207.png)

---

## Level 3

Source code của level 3

```php
<?php
    error_reporting(0);

    // Create folder for each user
    session_start();
    if (!isset($_SESSION['dir'])) {
        $_SESSION['dir'] = 'upload/' . session_id();
    }
    $dir = $_SESSION['dir'];
    if ( !file_exists($dir) )
        mkdir($dir);

    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        $error = '';
        $success = '';
        try {
            $filename = $_FILES["file"]["name"];
            $extension = end(explode(".", $filename));
            if ($extension === "php") {
                die("Hack detected");
            }
            $file = $dir . "/" . $filename;
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Đoạn code trên có phần tương tự với level 2, nhưng thay vì lấy đuôi file ở vị trí thứ 1 trong mảng như level 2 thì chương trình này sẽ lấy đuôi file cuối cùng

Bypass bằng cách sử dụng đuôi `.[phar](https://filegi.com/file-info/phar-3781/)`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%208.png)

Upload file đuôi phar

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%209.png)

Trang web hiển thị kết quả của câu lệnh `whoami`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2010.png)

---

## Level 4

Source code của Level 4

```php
<?php
    error_reporting(0);

    // Create folder for each user
    session_start();
    if (!isset($_SESSION['dir'])) {
        $_SESSION['dir'] = 'upload/' . session_id();
    }
    $dir = $_SESSION['dir'];
    if ( !file_exists($dir) )
        mkdir($dir);

    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        $error = '';
        $success = '';
        try {
            $filename = $_FILES["file"]["name"];
            $extension = end(explode(".", $filename));
            if (in_array($extension, ["php", "phtml", "phar"])) {
                die("Hack detected");
            }
            $file = $dir . "/" . $filename;
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Level này trang web sử dụng blacklist, nếu đường dẫn của file là `php`, `phtml`, `phar` thì chương trình sẽ dừng và in ra dòng chữ “Hack detected”

Bypass bằng cách ghi đè file .htaccess

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2011.png)

Upload file `.htaccess` vừa tạo

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2012.png)

Đổi đuôi file sang `php2` và tiến hành upload file

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2013.png)

Trang web hiển thị kết quả câu lệnh `whoami`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2014.png)

---

## Level 5

Source code level 5:

```php
<?php
    error_reporting(0);

    // Create folder for each user
    session_start();
    if (!isset($_SESSION['dir'])) {
        $_SESSION['dir'] = 'upload/' . session_id();
    }
    $dir = $_SESSION['dir'];
    if ( !file_exists($dir) )
        mkdir($dir);

    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        $error = '';
        $success = '';
        try {
            $mime_type = $_FILES["file"]["type"];
            if (!in_array($mime_type, ["image/jpeg", "image/png", "image/gif"])) {
                die("Hack detected");
            }
            $file = $dir . "/" . $_FILES["file"]["name"];
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Đoạn code thực hiện check [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) của file được upload lên, nếu không là 1 trong 3 kiểu `"image/jpeg", "image/png", "image/gif"` thì chương trình sẽ dừng và in ra màn hình chuỗi “Hack detected”

Sử dụng Burp Suite để bắt POST request upload file

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2015.png)

Chỉnh sửa Content-Type thành `image/gif` và gửi lại request, ta thấy trang web thông báo upload thành công

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2016.png)

Truy cập url chứa file đã upload

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2017.png)

## Level 6

Soure code level 6:

```php
<?php

    // Create folder for each user
    session_start();
    $dir = 'upload/' . session_id();
    if ( !file_exists($dir) )
        mkdir($dir);

    $error = '';
    $success = '';
    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
    if(isset($_FILES["file"])) {
        try {
            $finfo = finfo_open(FILEINFO_MIME_TYPE);
            $mime_type = finfo_file($finfo, $_FILES['file']['tmp_name']);
            $whitelist = array("image/jpeg", "image/png", "image/gif");
            if (!in_array($mime_type, $whitelist, TRUE)) {
                die("Hack detected");
            }
            $file = $dir . "/" . $_FILES["file"]["name"];
            move_uploaded_file($_FILES["file"]["tmp_name"], $file);
            $success = 'Successfully uploaded file at: <a href="/' . $file . '">/' . $file . ' </a>';
        } catch(Exception $e) {
            $error = $e->getMessage();
        }
    }
?>
```

Đoạn code sử dụng hàm [finfo_file](https://www.php.net/manual/en/function.finfo-file.php) để lấy [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types) của file, sau đó check xem có trong whitelist đã được khai báo trước không, nếu không có trong whitelist định trước chương trình sẽ dừng và in ra chuỗi “Hack detected”

Bypass bằng cách thêm header của file gif vào trước đoạn code php

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2018.png)

Bypass và upload file thành công

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2019.png)

Truy cập url của file đã upload

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2020.png)

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2021.png)

## Level 7

Ở level này, trang web cho phép người dùng upload 1 file nén, phía backend của trang web sẽ unzip (giải nén) và lưu vào folder cho người dùng

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2022.png)

Tiến hành upload thử một file

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2023.png)

Mình chú ý đến câu lệnh để unzip file được in phía dưới, tên file sẽ được đưa vào một câu lệnh để giải nén file, và tên file là do phía người dùng cung cấp nên chúng ta có thể chỉnh sửa tên file để khai thác lỗ hổng OS Command Injection

```php
Unzipper command: unzip /usr/upload/616609e23f10f16ea1ff8e114b4974c3/e66ea8344f034964ba0b3cb9879996ff.tar -d /usr/upload/616609e23f10f16ea1ff8e114b4974c3
```

Thực hiện bắt post request upload file và chỉnh sửa tên file thành `ten_file & <command> &` .Payload `& <command> &` với `&` là một toán tử câu lệnh trong linux với mục đích chạy ngầm 1 câu lệnh. Thay command = echo hell, ta thấy trang web trả về chuỗi “hell”

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2024.png)

Thay command thành `whoami` , trang web trả về www-data

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2025.png)

---

## Level 8

```php
<?php
    error_reporting(0);
    if (!isset($_GET['game'])) {
        header('Location: /?game=fatty-bird-1.html');
    }
    $game = $_GET['game'];
    if(isset($_GET["debug"])) die(highlight_file(__FILE__));
?>

<!DOCTYPE html>
<html lang="en">
    <head>
        <?php include './views/header.html'; ?>
    </head>

    <body>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a href="?game=fatty-bird-1.html&debug">Debug source</a>
        </nav>
        <br><br>
        <h3 class="display-4 text-center">File upload workshop</h3>
        <h4 class="display-4 text-center">Level 8</h4>
        <p class="display-5 text-center">Goal: read /etc/passwd</p>

        <br>
        <div style="background-color: white; padding: 20px;">
            <?php include './views/' . $game; ?>
        </div>

    </body>

    <?php include './views/footer.html' ?>
</html>
```

Đoạn code trên thực hiện lấy GET parameter “game” và truyền vào phần dưới của trang web:

```php
 <?php include './views/' . $game; ?>
```

Đây là lỗi **Path Traversal**, như quan sát thấy, chúng ta đang ở thư mục views, là thư mục con của /var/www/html/ (Thư mục default của apache) vì vậy cần sử dụng 4 lần `../` để về thư mục gốc của hệ điều hành, sau đó truy cập /etc/passwd

**Payload: `../../../../etc/passwd`**

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2026.png)

---

## Level 9

Source code của phần game:

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2027.png)

Tương tự như lv 8, lv 9 cũng dính lỗi **Path Traversal**

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2028.png)

Trang Profile có chức năng upload avatar người chơi

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2029.png)

Upload file hehe.php với nội dung

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2030.png)

Ta thấy trang web không hề filter file php

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2031.png)

Truy cập file avatar từ trang Hall of fame, ta thấy tên file đã được đổi thành avatar.jpg và code php không được thực thi

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2032.png)

Check file source code của trang profile, ta thấy đường dẫn lưu file avatar do người dùng upload lên là `/usr/upload`

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2033.png)

Sử dụng Path Traversal để truy cập đến avatar của bản thân, ta thấy câu lệnh `whoami` được thực thi và in ra kết quả

![Untitled](/assets/img/cyberJutsuUploadFile/Untitled%2034.png)

**_Shout out to CyberJutsu vì challenge chất lượng ❤️_**
