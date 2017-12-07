---
layout: entry
title: React Native cơ bản
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Bài viết này sẽ giúp bạn cài đặt và xây dựng ứng dụng đầu tiên với React Native.
---

Trước khi bắt đầu với React Native, chúng ta có 2 cách : Quick Start và Building Projects with React Native
<a href="https://github.com/react-community/create-react-native-app">Create React Native App</a> là cách dễ dàng và nhanh nhất để bắt đầu xây dựng một ứng dụng React Native mới. Nó cho phép bạn bắt đầu một project không cần cài đặt và config với bất kỳ một công cụ build native code - như Xcode hoặc Android Studio.

Giả sử bạn đã cài Node, như vậy chúng ta có thể sử dụng npm để cài đặt create-react-native-app trong command line:

```
npm install -g create-react-native-app
```

Sau đó chạy command để tạo 1 dự án React Native mới được gọi là "AwesomeProject":

```
create-react-native-app AwesomeProject

cd AwesomeProject
npm start
```

Sau khi chạy xong, command sẽ hiển thị một QR code

### Chạy ứng dụng React Native của bạn

Cài đặt <a href="https://expo.io/">Expo</a> trên các thiết bị iOS và Android sau đó connect chúng với cùng mạng wifi với máy tính chúng ta đang dev. Sử dụng Expo app, scan QR code mà terminal sinh ra để cài đặt và mở project trên thiết bị điện thoại

#### Chỉnh sửa app của bạn
Bây giờ bạn đã cài đặt thành công app trên các thiết bị như Android và iOS, hãy chỉnh sửa nó. Mở file `App.js` trong một editor nào đó và edit một vài dòng. Ứng dụng sẽ được reload một cách tự động và thay đổi giống với nội dung bạn vừa mới chỉnh sửa sau khi bạn nhấn save file.

Chúc mừng !!! Bạn đã cài đặt và dev project thành công ứng dụng React Native đầu tiên.

### Tiếp theo là gì nhỉ?

- Create React Native App cũng có một <a href="https://github.com/react-community/create-react-native-app/blob/master/react-native-scripts/template/README.md">Hướng dẫn sử dụng</a> bạn có thể tham khảo nếu bạn gặp vấn đề nào đó.

- Nếu bạn không thể thực hiện được, có thể tham khảo phần Troubleshooting trong README cho Create React Native App

Nếu bạn tò mò muốn học thêm về React Native, hãy tiếp tục theo dõi <a href="https://facebook.github.io/react-native/docs/tutorial.html">Tutorial</a>

### Chạy ứng dụng của bạn trên simulator hoặc virtual device

Create React Native App tạo dễ dàng để chạy ứng dụng React Native trên thiết bị thật mà không cần cài đặt môi trường phát triển. Nếu bạn muốn chạy ứng dụng trên iOS Simulator hoặc Android Virtual Device, hãy tham khảo bài hướng dẫn building projects with native code để học cách cài đặt Xcode và cài đặt môi trường phát triển Android
 
Khi cài đặt xong, bạn sẽ chạy app trên Android Virtual Device bằng lệnh `npm run android` hoặc chạy trên iOS bằng cách chạy lệnh `nom run ios`

