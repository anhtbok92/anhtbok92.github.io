---
layout: entry
title: Designning Beautiful Rest APIs
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: RESTful APIs là gì?
---


### 1. Phân biệt Web và Web service

Khi chúng ta truy cập 1 website trên thanh URL của trình duyệt, chúng ta sẽ nhận được 1 trang web. Những thông tin của website sẽ hiển thị ra màn hình để chúng ta đọc được, kết hợp với css và html giúp các thông tin hiển thị đẹp hơn và bắt mắt hơn. Đó là nội dung dành cho người dùng cuối.

Trong khi đó, **Web Service** là 1 dịch vụ web, khái niệm **Web Service** rộng hơn Web thông thường. Các thông tin **Web Service** cung cấp là các thông tin thô, khó hiểu với nhiều người dùng. Có thể hiểu, Nó là 1 dạng UI dành cho developer, developer sẽ tương tác với application của ta thông qua hệ thống API, và API phục vụ đối tượng end user là developer. Ví dụ, Khi ta truy cập vào trang [https://openweathermap.org/api](https://openweathermap.org/api), làm theo các hướng dẫn ta sẽ lấy được thông tin thời tiết được trả về, nó là 1 dịch vụ web chuyên cung cấp các số liệu thời tiết ứng với từng vùng miền khác nhau. Các **Web Service** thường cung cấp dữ liệu trả về dưới 2 dạng là **XML** và **JSON.**

### 2. RESTful APIs là gì?

**REST** (**RE**presentational **S**tate **T**ransfer) được đưa ra vào năm 2000 trong luận văn tiến sĩ của **Roy Thomas Fielding** (đồng sáng lập giao thức HTTP). Trong luận văn ông giới thiệu khá chi tiết về các ràng buộc, quy ước cũng như cách thức thực hiện với hệ thống để có được một hệ thống **REST.**

Nói ngắn gọn, REST định nghĩa các quy tắc kiến trúc theo 1 quy chuẩn để chúng ta thiết kế Web services, chú trọng vào tài nguyên hệ thống, bao gồm các trạng thái tài nguyên được định dạng như thế nào và được truyền tải qua HTTP, và được viết bởi nhiều ngôn ngữ khác nhau. Trong kiến trúc REST mọi thứ đều được coi là tài nguyên, chúng có thể là: tệp văn bản, ảnh, trang html, video, hoặc dữ liệu động… REST server cung cấp quyền truy cập vào các tài nguyên, REST client truy cập và thay đổi các tài nguyên đó. Ở đây các tài nguyên được định danh dựa vào URI, REST sử dụng một vài đại diện để biểu diễn các tài nguyên như văn bản, JSON, XML.

### 3. Các nguyên tắc cơ bản để thiết kế Web Service

#### Sử dụng các phương thức HTTP một cách rõ ràng

Rest đề xuất developer sử dụng các phương thức HTTP rõ ràng, nhất quán với cách chúng được định nghĩa. Theo đó.

- Tạo 1 tài nguyên trên server : POST
- Đọc tài nguyên trên server : GET
- Cập nhật tài nguyên : UPDATE
- Xóa tài nguyên : DELETE

Việc sử dụng phương thức GET để tạo hoặc cập nhật thông tin về lý thuyết thì không sai, nhưng về mặt ngữ nghĩa nó sẽ gây ra các hiểu lầm tai hại. Vì thế, các nguyên tắc trên sinh ra làm cho mọi thứ trở nên rõ ràng, dễ hiểu.

 

#### Phi trạng thái

Một đặc điểm quan trọng của Rest đó là stateless (phi trạng thái), tức là không lưu giữ thông tin của client. Rest không quản lý phiên làm việc. Việc server không lưu trữ thông tin nào của client giúp cho hệ thống của bạn dễ phát triển, duy trì và mở rộng vì không tốn công CRUD trạng thái của client. Ngoài ra còn một số nguyên nhân liên quan đến bộ nhớ, cân bằng tải…Tóm lại, việc tách biệt công việc của client và server mang lại rất nhiều lợi ích cho hệ thống của bạn.

#### Cấu trúc thư mục như URI

URI cần phải đơn giản, có thể đoán biết được, và dễ hiểu với đa số developer. Khi nhìn vào 1 URI ta cần phải biết nó thực hiện công việc gì, chức năng ra làm sao, như thế nào. Tránh gây hiểu  nhầm cho người khác, đặc biệt các tham số phải rõ ràng, đơn giản, không nên truyền quá nhiều param mới lấy được thông tin.

#### Chuyển đổi XML, JSON hoặc cả 2

 

<div class="df-fragment df-cktext-default">Khi Client gửi một yêu cầu tới web service nó thường được truyền tải dưới dạng XML hoặc JSON và thông thường nhận về với hình thức tương tự. Đôi khi Client cũng có thể chỉ định kiểu dữ liệu nhận về mà nó mong muốn (JSON, hoặc XML,..), các chỉ định này được gọi là các kiểu MINE, nó được gửi kèm trên phần HEADER của request. Cụ thể ở đây ta có thể sử dụng các một vài kiểu MIME thông dụng sau: JSON, XML, XHTML. Điều này cho phép các service sử dụng bởi các client viết bởi các ngôn ngữ khác nhau, chạy trên nhiều nền tảng và thiết bị khác nhau. Sử dụng các kiểu MIME cho phép client chọn dạng dữ liệu phù hợp với nó.</div>** **

 


