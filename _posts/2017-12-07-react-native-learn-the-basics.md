---
layout: entry
title: Các kiến thức cơ bản khi làm việc với React-Native
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Bài viết này sẽ giúp bạn làm quen với khái niệm cơ bản khi làm việc với React-Native.
---

React Native cũng giống như React, nhưng nó sử dụng native component thay vì web component để build các khối. Vì thế để hiểu cấu trúc đơn giản 
của ứng dụng React Native, bạn cần hiểu các khái niệm cơ bản của React như JSX, components, state và props. Nếu bạn đã biết về React rồi,
bạn vẫn cần học thêm về React-Native-specific, giống như native components. Hướng dẫn này nhắm đến nhiều đối tượng người đọc cho dù bạn có kinh nghiệm về React hay chưa có kinh nghiệm

Hãy cùng bắt đầu thôi nào !!!

#### Hello World

Như khi bắt đầu với các ngôn ngữ và công nghệ mới, chúng ta phải build một ứng dụng "Hello World". Đối với React-Native nó trông như thế này

```
import React, { Component } from 'react';
import { AppRegistry, Text } from 'react-native';

export default class HelloWorldApp extends Component {
  render() {
    return (
      <Text>Hello world!</Text>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => HelloWorldApp);
```

#### Đoạn code trên có ý nghĩa gì nhỉ ?

Các cú pháp `import, from, class, extends và ()` tất cả syntax đều là của ES2015. Nếu bạn không quen với ES2015, bạn có thể đọc và tìm hiểu thêm ở link <a href="https://babeljs.io/learn-es2015/">this page</a> sau để quen hơn với cú pháp của ES2015.

Những điều bất thường khác trong code example là `<Text>Hello world!</Text>`. Đây là JSX - một syntax để nhúng XML trong Javascript. Trong React, JSX chúng ta hãy cùng viết markup language bên trong code. Nó giống như HTML trong web có các thẻ hay sử dụng
như `<div>`, `<span>`, bạn sẽ sử dụng React Component. Trong trường hợp này, `<Text>` chính là thẻ `Buid-in` component, chính là để hiển thị một đoạn text

#### Component

Do đoạn code trên đang được khai báo là `HelloWorldApp`, một Component mới. Khi bạn đang xây dựng ứng dụng React Native, 
bạn sẽ đang tạo một vài component mới. Mọi thứ bạn nhìn thấy trên màn hình