---
layout: entry
title: Những điều mới mẻ có trong PHP7
author: Nguyen Tuan Anh
author-email: victory1080@gmail.com
description: ột ngôn ngữ lập trình phổ biến nhất trên thế giới, gần đây đã phát hành phiên bản PHP 7. Chúng ta hãy cùng tìm hiểu PHP version 7 có gì mới mẻ so với phiên bản stable mà hiện nay chúng ta đang sử dụng
---

PHP – Một ngôn ngữ lập trình phổ biến nhất trên thế giới, gần đây đã phát hành phiên bản PHP 7. Chúng ta hãy cùng tìm hiểu PHP version 7 có gì mới mẻ so với phiên bản stable mà hiện nay chúng ta đang sử dụng –  phiên bản 5.6. PHP 6 – là một dự án thử nghiệm, nhưng vì một số lý do nào đó mà nó chưa hoàn chỉnh, để người dùng tránh việc nhầm lẫn giữa các version thử nghiệm và hoàn chỉnh. Vì vậy, PHP 7 đã ra đời. Phiên bản alpha đầu tiên được phát thành vào tháng 6/2015 và phiên bản cuối cùng dự kiến được phát hành vào tháng 10/2015. Đến thời điểm bài viết, phiên bản PHP7.0.1 đã được cho ra mắt.

### Những điều mới mẻ có trong PHP7

#### Hiệu Năng

PHP sử dụng engine thông dịch đó là Zend engine (không nhầm lẫn với Zend Framework), mã nguồn mở viết = C. Các phiên bản PHP 5.x sử dụng Zend engine II. Với PHP7 sẽ nhận được những cải tiến rất nhiều từ phiên bản engine tiếp theo – Phiên bản 3.0, được thiết kế và tái cấu trúc để tăng tốc độ và giảm bộ nhớ. Điều này đồng nghĩa với việc ứng dụng vào việc thực tế : làm giảm đáng kể thời gian chạy và tăng trải nghiệm của người dùng. Ngoài ra, PHP 7.0 cũng sử dụng ít bộ nhớ hơn nhờ vào cấu trúc dữ liệu nhỏ gọn, tăng hiệu suất sử dụng bộ nhớ từ 30% – 50%, nó cho phép bạn phục vụ đồng thời nhiều người dùng hơn mà không cần bổ sung thêm máy chủ.

Ưu điểm dễ nhận biết nhất của PHP7.0 làm tăng hiệu suất từ 50% đến 200% đối với các ứng dụng thực tế mà không cần thay đổi bất kỳ dòng code nào. Dưới đây là những con số so sánh để thấy được sự thay đổi mạnh mẽ về Performance khi sử dụng PHP7 đối với CMS và Framework phổ biến là WordPress, Laravel và Zend.

[![wpphp7](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/wpphp7.jpg?fit=700%2C391)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/wpphp7.jpg)

[![343434](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/343434.jpg?fit=700%2C381)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/343434.jpg)

#### Những tính năng mới mẻ

PHP 7 có rất nhiều những tính năng mới mẻ được nhà sản xuất đưa ra. Chúng ta cùng điểm qua một vài tính năng mới nổi bật của nó.

- Toán tử Spaceship – Toán tử so sánh kết hợp

<span style="color: #333333;">Toán tử `Spaceship` chạy dưới tên chính thức là Combined Comparison Operator (toán tử so sánh kết hợp). Ký hiệu của toán tử mới trông như thế này: `<=>` (giống như một con tàu vũ trụ đơn giản, nếu bạn chịu khó tưởng tượng).</span>

<span style="color: #333333;">Toán tử `Spaceship` này trả về 0 nếu cả hai toán hạng bằng nhau, 1 nếu toán hạng bên trái lớn hơn, và -1 nếu toán hạng bên phải lớn hơn. Nó cũng được gọi là một toán tử so sánh three-way, và đã tồn tại trong những ngôn ngữ lập trình phổ biến khác như Perl và Ruby.</span>

[![1356353](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/1356353.jpg?resize=700%2C323)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/1356353.jpg)

- Toán tử Null Coalescing

<span style="color: #333333;">Toán tử `Null Coalescing` được thể hiện bằng hai dấu chấm hỏi (`??`). Bạn sử dụng nó khi muốn kiểm tra liệu 1 cái gì đó có tồn tại hay trả về một giá trị mặc định hay không?</span>
Trả về toán hạng đầu tiên nếu nó không null
Trả về toán hạng thứ 2 trong các trường hợp khác

[![78788](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/78788.png?resize=718%2C321)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/78788.png)

Lệnh `$username = $_GET[‘user’] ?? ‘nobody’;` Sẽ tương đương với : `$username = isset($_GET[‘user’]) ? $_GET[‘user’] : ‘nobody’`

Cùng một mục đích nhưng toán tử này giảm được thời gian viết code cũng như những khai báo cơ bản trong lập trình

- Hỗ trợ định nghĩa 1 mảng Constant sử dụng define()

Với PHP 7 chúng ta hoàn toàn có thể định nghĩa 1 mảng constants với từ khóa `define()`. Với phiên bản 5.6 chúng chỉ được định nghĩ duy nhất bằng cách sử dụng từ khóa const

[![333333](https://i0.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/333333-300x173.png?fit=300%2C173)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/333333.png)

- Group use declarations – Import từ cùng Namespace dễ dàng hơn

<span style="color: #3d3d3d;">Cú pháp mới cắt giảm mọi sự rườm rà, làm cho mã gọn gàng hơn, dễ nhìn hơn, giúp các lập trình viên tiết kiệm được rất nhiều thời gian gõ code.</span>

<span style="color: #3d3d3d;">Tính năng này cũng giúp cho việc đọc và debug code dễ dàng hơn bởi vì việc khai báo sử dụng nhóm giúp bạn dễ dàng xác định được các import thuộc về cùng một module nào.</span>

[![tuananhdfdfdf](https://i2.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/tuananhdfdfdf.png?resize=459%2C385)](https://i2.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/tuananhdfdfdf.png)

- Session Options

<span style="color: #3d3d3d;"><span style="color: #3d3d3d;">`Session_start()` với PHP 7 có thể cho phép là 1 mảng những lựa chọn</span></span>

```
<?php session_start([ 'cache_limiter' => 'private', 'read_and_close' => true, ]); ?>
```

- Chia nguyên với hàm `intdiv()`

```
Ví dụ : <?php var_dump(intdiv(10, 3)); ?> output : int(3)
```

- Anonymous classes

<span style="color: #333333;">PHP 7 cho phép bạn sử dụng các class vô danh (anonymous), đây là một đặc trưng đã có trong những ngôn ngữ lập trình hướng đối tượng khác như C# và Java. Một class anonymous là một class không có tên. Đối tượng mà nó khởi tạo có cùng chức năng như một đối tượng của một lớp có tên.</span>

<span style="color: #333333;">Cú pháp giống như chúng ta sử dụng trong các class PHP truyền thống, chỉ có thiếu cái tên class. Nếu các lớp vô danh (anonymous classes) được sử dụng tốt, chúng có thể làm tăng tốc độ thực thi. Các lớp vô danh là tuyệt vời khi một class chỉ được sử dụng một lần trong suốt quá trình thực thi và trong những trường hợp một class không cần phải được ghi tài liệu.</span>

[![plplplp](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/plplplp.jpg?fit=700%2C191)](https://i1.wp.com/vietnamlab.vn/wp-content/uploads/2015/12/plplplp.jpg)

- CSPRNG functions

<span style="font-size: 13.0pt; color: #333333;">Đặc điểm của 2 hàm mới này để tạo ra các số nguyên và chuỗi mã hóa an toàn </span>

```
string random_bytes(int length);
int random_int(int min, int max);
```

<span style="font-size: 13.0pt; color: #333333;">Cả 2 hàm này sẽ trả về `exception Error` nếu đầu vào không được tìm thấy.</span>

### Cài đặt PHP7 với vagrant

Thay vì phải cài đặt thủ công từng câu lệnh một, nhưng nhờ có vagrant – việc tạo môi trường có hỗ trợ các version PHP trở nên dễ dàng hơn.

Chúng ta có thể tải các box hỗ trợ PHP7 tại đây: [https://atlas.hashicorp.com/rasmus/boxes/php7dev](https://atlas.hashicorp.com/rasmus/boxes/php7dev)

Trước tiên, hãy tạo thư mục làm việc :

```
$ mkdir php7dev 
$ cd php7dev
```

Bên trong thư mục này, chúng ta có thể cài đặt vagrant vm:

```
$ vagrant box add rasmus/php7dev 
$ vagrant init rasmus/php7dev 
$ vagrant up
```

Nếu máy ảo yêu cầu nhập vào password thì bạn nhập “*vagrant”*

Bây giờ, hãy ssh vào máy và trải nghiệm PHP 7 thôi nào !!!

```
$ vagrant ssh
```

#### Các phiên bản PHP có bên trong VM

Rasmus’box mang đến các version PHP 5.3, 5.4, 5.5, 5.6 và 7. Mỗi một version lại cung cấp 4 phiên bản là : release, debug, zts-debug. Để lựa chọn version PHP và phiên bản sử dụng :

```
$ newphp {version number} {type}
```
Trong đó :

–  {version number} : là các version có trong box 5.3, 5.4,…7

– {type} : là phiên bản sử dụng release, debug…

Để sử dụng  PHP7 – debug :

```
$ newphp 7 
$ newphp 7 debug
```

Cuối cùng, check xem phiên bản PHP 7 đã cài đặt thành công hay chưa :

```
$ php -v
```

### Kết luận

<span style="color: #333333;">Bây giờ bạn đã có môi trường để trải nghiệm với PHP version 7, tuy nhiên chúng ta chỉ nên trải nghiệm và test các tính năng mới của nó, không nên áp dụng vào dự án thật của mình vì dù sao những phiên bản mới vẫn chưa ổn định và còn nhiều bug cũng như ít nhận được sự hỗ trợ từ cộng đồng. Chúng ta hãy chờ đón một tương lai mới, một sức mạnh mới mà những framework mang lại cùng với những điểm mới mẻ trong PHP 7.</span>

### Tài liệu tham khảo

- [https://akrabat.com/building-and-testing-php7/](https://akrabat.com/building-and-testing-php7/)
- [https://github.com/rlerdorf/php7dev](https://github.com/rlerdorf/php7dev)
- [https://php.net](https://php.net)


