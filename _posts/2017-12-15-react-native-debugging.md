---
layout: entry
title: Debugging trong React Native
author: Nguyen Tuan Anh
author-email: victory1080@gmail.com
description: Bài viết này sẽ giúp bạn biết cách để debug ứng dụng React Native của mình
---

Các bạn click vào <a href="https://viblo.asia/p/react-native-guide-debuging-djeZ1BpGlWz">đây</a> để xem bài dịch nhé. 
Bài debug này mình định dịch lại từ trang chủ nhưng hiện tại có một bạn ở viblo.asia đã dịch rồi nên chúng ta có thể tham khảo bài này để có thể debug khi làm việc với react-native một cách dễ dàng. Các phần cần chú ý trong bài mình sẽ note lại ở dưới đây:


### Chrome Developer Tools

Bật máy ảo Genymotion mở Menu và chọn `Debug JS Remotely`. Trình duyệt sẽ được tự động mở tại http://localhost:8081/debugger-ui

### React Developer Tools

Sử dụng gói `react-devtools` bằng dòng lệnh sau

```
npm install -g react-devtools
```

sau đó chạy  `react-devtools` từ terminal của git trong thư mục dự án như sau:

```
react-devtools
```

Chú ý : Trong khi bật chạy react-devtools vẫn mở ứng dụng bằng lệnh `react-native start` để load các thay đổi mới nhất của các file js mà chúng ta thay đổi. Khi muốn debug bằng lệnh console.log trong các file js, chúng ta quan sát log xuất hiện trong màn hình được mở ban đầu là http://localhost:8081/debugger-ui.

### Kết Luận

Hy vọng với những chú ý nhỏ và bài viết mình chia sẻ bên trên, các bạn có thể debug một cách dễ dàng với ứng dụng React-Native, quả thực việc debug với React-Native cũng không
khác ứng dụng react trên web là mấy.