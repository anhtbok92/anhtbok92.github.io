---
layout: entry
title: Vue.js những kiến thức cơ bản
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: VueJs chứa một sức mạnh lớn để xây dựng Single-Page Applications
---

VueJs là một thư viện tập trung vào phần view trong mô hình MVVM. VueJs chứa một sức mạnh lớn để xây dựng Single-Page Applications khi được kết hợp với công cụ build và các thư viện/component được xây dựng bởi cộng đồng

Mục tiêu của bài hướng dẫn này giúp bạn hiểu được các kiến thức cơ bản nhất, trước khi bước vào thế giới của VueJs.

### 1. Tạo một thể hiện của Vue.
Khi bắt đầu làm quen với VueJs, chúng ta có thể cài đặt VueJs thông qua NPM, Bower hoặc cách đơn giản nhất chỉ cần 1 link script từ CDN là có thể bắt đầu với Vue rồi. Để đơn giản, tôi sẽ hướng dẫn bạn cách nhanh nhất để bắt đầu với VueJs. Đó là sử dụng link VueJs từ CDN.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Hướng dẫn sử dụng VueJs cơ bản</title>
  </head>
  <body>
  <div id="vue-instance">
    <!-- Đây là DOM Element, nơi chúng ta sẽ gắn thể hiện của Vue -->
  </div>
  <script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>
  <script>
    var vm = new Vue({
      el: '#vue-instance'
    });
  </script>
  </body>
</html>
```

Nhìn vào đoạn code trên, một vue-instance đã được tạo bằng hàm constructor new Vue() và xác định DOM element để gắn object vào đó. Từ khóa el là viết tắt của element. Trong trường hợp này chúng ta đang tạo một vue instance và xác định element để đưa object vào thông qua CSS selector: #vue-instance. Chúng ta sẽ tiếp tục đi vào những tính năng được coi là nổi trội của Vue, giúp nó trở nên đẹp và gọn gàng hơn.

### 2. 2-Way Data Binding với v-model

VueJs cung cấp v-model sử dụng cho gắn dữ liệu theo 2 chiều. Nó tự động lấy dữ liệu được nhập vào và cập nhật xuống model. Tuy nhiên, v-model bỏ qua các thuộc tính thiết lập giá trị ban đầu cho từng thành phần HTML của form như value, checked, selected, nếu bạn muốn khởi tạo các giá trị này, khai báo trong phần data của vue instance.

#### TextBox
```
<div id="ex9">
  <input v-model="message" placeholder="Nhập tên của bạn">
  <p>Tên của bạn là: {{ message }}</p>
</div>
```

#### Textarea
```
<span>Multiline message is:</span>
<p style="white-space: pre">{{ message }}</p>
<br>
<textarea v-model="message" placeholder="add multiple lines"></textarea>
```

#### Checkbox
```
<input type="checkbox" id="checkbox" v-model="checked">
<label for="checkbox">{{ checked }}</label>
```

#### Radio
```
<input type="radio" id="one" value="One" v-model="picked">
<label for="one">One</label>
<br>
<input type="radio" id="two" value="Two" v-model="picked">
<label for="two">Two</label>
<br>
<span>Picked: {{ picked }}</span>
```
#### Select
```
<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selected: {{ selected }}</span>
```

### 3. Handling Events với v-on
Trong vueJs chúng ta có thể quản lý các sự kiện liên quan đến một view như click, hover...Nó rất đơn giản bằng cách thêm các phương thưc quản lý sự kiện (event handlder) vào ViewModel, trong phương thức này sử dụng this để truy xuất đến các thành phần trong dữ liệu của model. Trong đoạn code này, chúng ta đã tạo một phương thức sayHello trong object methods - nơi hiển thị alert box với tên được user nhập vào. Phương thức sayHello được gán vào sự kiện v-on:click khi người dùng click vào button.

```
<div id="vue-instance">
  Enter your name: <input type="text" v-model="name">
  <button v-on:click="sayHello">Hey there!</button>
</div>

<script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>

<script>
  var vm = new Vue({
    el: '#vue-instance',
    data: {
      name: ''
    },
    methods: {
      sayHello: function(){
        alert('Hey there, ' + this.name);
      }
    }
  });
</script>
```

Tất nhiên bạn không bị giới hạn chỉ có sự kiện click mà v-on còn chấp nhận các sự kiện khác như v-on:mouseover, v-on:keydown, v-on:submit, v-on:keypress, etc... hoặc sự kiện mà chính chúng ta định nghĩa hàm để làm những công việc đặc thù riêng nữa.

### 4. Điều kiện rendering với v-if và v-show
Giả sử bạn muốn hiển thị một thông báo chào mừng cho người dùng nếu họ đăng nhập hoặc hiển thị form đăng nhập nếu họ chưa login vào hệ thống.Vue làm điều này khá dễ dàng bằng cách sử dụng v-if và v-show. Hãy xem chúng ta có thể làm được điều này như thế nào nhé.

Chúng ta sẽ sử dụng những gì đã được học ở phần trước về xử lý sự kiện với v-on, chúng ta sẽ tạo ra 1 hàm đơn giản, sử dụng isLoggedIn set giá trị true và false để thay đổi giá trị khi người dùng nhấp vào nút đăng nhập hoặc đăng xuất.

Khi giá trị của isLoggedIn thay đổi, Vue sẽ tự động nhận giá trị trong điều kiện v-if và đưa ra nội dung đúng với điều kiện đó muốn hiển thị
```
<div id="vue-instance">
  <div v-show="isLoggedIn">
    Chào mừng bạn đã Login!
    <button @click="login" type="submit">Logout</button>
  </div>
  <div v-else>
    <input type="text" placeholder="username">
    <input type="password" placeholder="password">
    <button @click="login" type="submit">Login</button>
  </div>
</div>
```
### 5. Hiển thị danh sách với v-for
Giả sử bạn có một cửa hàng trực tuyến, và bạn muốn hiển thị các mặt hàng trong kho của bạn cho người dùng. v-for cho phép bạn render nội dung dựa trên các giá trị của một mảng bằng cách sử dụng một cú pháp đặc biệt như sau:
```
<body>

<div id="vue-instance">
  <ul>
    <li v-for="item in inventory">
      {{ item.name }} - ${{ item.price }}
    </li>
  </ul>
</div>

<script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>

<script>
var vm = new Vue({
  el: '#vue-instance',
  data: {
    inventory: [
      {name: 'MacBook Air', price: 1000},
      {name: 'MacBook Pro', price: 1800},
      {name: 'Lenovo W530', price: 1400},
      {name: 'Acer Aspire One', price: 300}
    ]
  }
});
</script>

</body>
```

### 6. Vuex - Quản lý state trong ứng dụng

Nếu bạn đã từng làm việc với React, bạn có thể đã từng nghe tới Flux và Redux. VueJs cũng vậy, việc tận dụng các component làm nên sức mạnh của VueJs, tuy nhiên ở vue chưa có cách nào giúp chia sẻ trạng thái giữa các component này, hoặc có nhưng mà nguồn rất khó duy trì đặc biệt đối với các dự án lớn. Vuex là một thư viện sinh ra với mục đích giúp quản lý trạng thái các component trong VueJs, nó là nơi lưu trữ tập trung cho tất cả các component trong 1 ứng dụng. 

Mình xin kết thúc bài tại đây, hẹn gặp lại mọi người phần 2 sẽ tập trung vào Vuex để bài viết đỡ bị loãng nhé. Thank all !!!
<Còn tiếp phần 2>

<h3>Link tham khảo</h3>
<a href="https://vuejs.org/">https://vuejs.org/</a>

<a href="http://vuejs.senviet.org/v2/guide/">http://vuejs.senviet.org/v2/guide/</a>

<a href="https://techtalk.vn/ly-do-nao-khien-vue-js-an-dut-react-js.html">https://techtalk.vn/ly-do-nao-khien-vue-js-an-dut-react-js.html</a>