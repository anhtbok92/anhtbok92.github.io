---
layout: entry
title: Giới thiệu tổng quan về Vue.js
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Vue.js là gì?
---

### 1. Mô hình MVVM trong Vue.js
Vue.js sử dụng mô hình MVVM (Model-View-ViewModel), nhìn vào các chữ đầu viết tắt, chúng ta cũng có thể dễ dàng nhận ra, trong Vue.js có 3 đối tượng cần quan tâm đó là : Model, View, và ViewModel.
Ví dụ:

* Một View : đơn giản là các thẻ html cơ bản, nơi mà chúng ta sẽ render ra dữ liệu để hiển thị cho người dùng. Ở đây, đơn giản nhất mình tạo 1 view đặt tên mà my_view.

```
<div id="my_view">
</div>

```
* Một Model: cũng giống như mô hình MVC, model trong view có thể hiểu là nơi chứa dữ liệu hoặc nó cũng có thể chỉ là một đối tượng đơn thuần trong javascript

```
<script type="text/javascript">
	var myModel = {
		name: "Nguyễn Tuấn Anh",
		url: "https://facebook.com/ahihi",
		author: "Nguyen Tuan Anh"
	};
</script>

```
* Một ViewModel: chính là một instance của Vue class, và chính là cầu nối giữa view (my_view) và Model (myModel)


```
var myViewModel = new Vue({
  el: '#my_view',
  data: myModel
});
```


### 2. Hiểu hơn về 2-way binding trong Vue
Trong ví dụ trên chỉ đơn giản là luồng dữ liệu 1 chiều, từ `Model -> ViewModel` và từ `ViewModel -> View`

Nhưng Vue còn làm được hơn thế nữa, luồng dữ liệu chúng ta mong muốn sẽ như thế này

```
Model <-> ViewModel <-> View
```
Tức là ngoài việc Model truyền dữ liệu của mình thông qua cầu nối ViewModel thì khi người dùng tác động vào view làm thay đổi dữ liệu ngoài View, nó sẽ tác động trở lại vào cầu nối ViewModel và update data trở lại Model. Việc làm này khiến Vue.js trở nên linh hoạt hơn.

### 3. Vue.js Component - Xây dựng ứng dụng theo hướng module hóa
#### a. Khai báo component trong Vue.js

Ví dụ:
```
<script type="text/javascript">
		Vue.component('product-item', {
			props: ['product'],
			template: '<div class="col-md-4"><div class="panel panel-success"><div class="panel-heading"><h3 class="panel-title">{{ product.name }}</h3></div><div class="panel-body">{{ product.price }}</div></div></div>'
		});
	</script>
```

trong component này chúng ta đặt tên là 'product-item' với dữ liệu được truyền từ cha xuống con bằng cú pháp props: ['product'], sau khi khai báo props chúng ta hoàn toàn có thể sử dụng biến này trong template của chúng ta để hiển thị ra name và price của sản phẩm.

Để có data sử dụng ở view, ta khai báo data của ViewModel như sau:

```
<script type="text/javascript">
var app6 = new Vue({
			el: '#app6',
			data: {
				productList: [
					{ name: 'Samsung Galaxy S8 Plus', price: '20.490.000₫'},
					{ name: 'Samsung Galaxy S8', price: '18.490.000₫' },
					{ name: 'Samsung Galaxy S7 Edge', price: ' 12.990.000₫' },
					{ name: 'Samsung Galaxy C9 Pro', price: '11.490.000₫' }
				]
			}
		});
</script>

```

Cách gọi component như sau:

```
<div class="container">
		<div class="row" id="app6">
			<product-item v-for="item in productList" v-bind:product="item"></product-item>
		</div>
	</div>
```

Chú thích: thẻ đóng mở <product-item> chính là một component chúng ta đã khai báo bên trên, cú pháp v-for cho phép chúng ta loop mảng productList chúng ta đã khai báo trong ViewModel bên trên. v-bind:production, như bài viết trước mình đã nói qua, v-bind là một directive có tiền tố v- biểu thị nó là một tiền tố đặc biệt được cung cấp bởi Vue.js, directive này cung cấp một reactive behavior cho DOM, ở đây xuất hiện với mục đích là, hãy truyền cho component này một props có tên là product, giá trị của product này được lấy từ item mà chúng ta vừa sử dụng một directive khác là v-for để tạo ra.

#### b. Cách giao tiếp giữa component cha và component con trong Vue.js
Trong Vue.js các component này có thể sử dụng component khác làm làm template của mình. Khi sử dụng như vậy tạo nên mối quan hệ cha-con giữa các component với nhau. Như ví dụ bên trên, component cha có thể truyền dữ liệu xuống component con sử dụng props, vậy component con mà muốn truyền dữ liệu đến component cha thì làm như thế nào? Câu trả lời là, component con chỉ có thể "thông báo" tới component cha mà thôi, tức là component con có thể gửi thông điệp của mình đến component cha thông qua các event (sự kiện) theo mô hình như sau:
![alt](https://drive.google.com/uc?id=0B05rqFCwNCjkUldSUzZldURIRjg&export=download)

Trước tiên, chúng ta cần hiểu về 2 khái niệm: $on và $emit

* $on(eventName): để lắng nghe sự kiện
* $emit(eventName): để trigger một sự kiện

Theo như tài liệu trên trang chủ của Vue.js, event của Vue.js độc lập với các event target của browser (https://developer.mozilla.org/en-US/docs/Web/API/EventTarget), có thể cách hoạt động của nó giống với addEventListener và dispatchEvent nhưng tuyệt đối nó không phải là một tên gọi khác của 2 event này.
Ngoài ra, 1 component cha có thể lắng nghe những event được emit từ 1 component con bằng cách sử dụng v-on trong template - nơi mà component con được sử dụng. Chú ý, bạn không thể sử dụng $on để lắng nghe những events được emited từ component con mà phải sử dụng directly v-on trong template

Ví dụ đơn giản để hiểu cách component con, truyền một "thông điệp" tới component cha như sau:

```
finding
```

#### c. Giao tiếp giữa các component không có quan hệ cha con
Nhiều khi chúng ta cần truyền thông tin giữa các component trong dự án, lúc này cách giao tiếp đơn giản giữa các component là sử dụng $emit và $on như trên.

Ta khởi tạo một Vue instance

```
var bus = new Vue()
```

Khi có component A sẽ tạo ra 1 sự kiện:
```
bus.$emit('event-name', 1)
```
và component B sẽ lắng nghe sự kiện:
```
bus.$on('event-name', function (id) {
  // ...
})
```
### Link tham khảo
<a href="https://vuejs.org/">https://vuejs.org/</a> 

<a href="http://vuejs.senviet.org/v2/guide/">http://vuejs.senviet.org/v2/guide/</a>

<a href="https://techtalk.vn/ly-do-nao-khien-vue-js-an-dut-react-js.html">https://techtalk.vn/ly-do-nao-khien-vue-js-an-dut-react-js.html</a>