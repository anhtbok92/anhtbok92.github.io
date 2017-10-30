---
layout: entry
title: Cải thiện Performance khi render component trong React.js
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: React được biết đến với tốc độ thực thi nhanh. Nhưng không có nghĩa là chúng ta không cần tối ưu hóa khi viết code. Một trong những mẹo quan trọng để giúp tăng performance cho ứng dụng react của chúng ta nhanh lên đó chính là optimize hàm `render()` của react.
---

React được biết đến với tốc độ thực thi nhanh. Nhưng không có nghĩa là chúng ta không cần tối ưu hóa khi viết code. Một trong những mẹo quan trọng để giúp tăng performance cho ứng dụng react của chúng ta nhanh lên đó chính là optimize hàm `render()` của react.

Chúng ta tạo 1 bài test đơn giản. Để so sánh tốc độ hàm render trong các điều kiện khác nhau.

- **Stateless** (functional) components vs **stateful** (class-based) components
- **Pure component** rendering (compnent của react) vs **stateless** components
- React 0.14 vs React 15 rendering performance trong môi trường development and production

### TLDR – Too long; didn’t read;

Dành cho những ai lười và chỉ muốn biết ngay kết quả trong 3 ví dụ chúng ta muốn test ở trên. Đây chính là danh sách những kết quả thu được từ example này

- **Stateless** (functional) components không nhanh hơn the **stateful** (class)
- Sử dụng **React 15** nhanh hơn khoảng 25% so với sử dụng **React 0.14**
- **Pure components** là nhanh nhất bằng cách sử dụng hàm **shouldComponentUpdate**
- Render trong môi trường **development** với** react 15** chậm hơn 2x lần so với **0.14** => Tại sao vậy nhỉ?

### Performance đã được test như thế nào?

Cách làm rất đơn giản. Chúng ta sẽ lặp lại trên hàm `render()`. Ta sẽ tạo ra 1 component cha và đặt tên là App.

Component này chứa 1 trong ba loại component như đã nói ở trên:

- A stateless component
- A stateful component
- A pure stateful component với hàm shouldComponentUpdate trả về false

```js
// Stateful component
class Stateful extends Component {
  render () {
    return <div>Hello Cmp1: stateful</div>;
  }
}
// Pure stateful with disabled updates
class Pure extends Component {
  shouldComponentUpdate() {
    return false;
  }

  render () {
    return <div>Hello Cmp2: stateful, pure, no updates</div>;
  }
}
// Stateless component
function Stateless() {
  return <div>Hello Cmp3: stateless</div>;
}
```

Các component ở trên rất đơn giản. Chỉ render là 1 thẻ div chứa đoạn text nhỏ bên trong và không thay đổi cây DOM. Chúng ta thực hiện render 100000 lần với mỗi 1 loại component kể trên. Thời gian render được đo từ lúc bắt đầu render tới khi kết thúc bằng cách sử dụng hàm **Performance.now** của trình duyệt.

Tất cả mã Javascript chạy với ES6 không sử dụng các bước chuyển đổi (chuyển sang ES5).

### Stateless components không nhanh hơn statefull components

![React Compare](https://drive.google.com/uc?id=0B05rqFCwNCjkWnA1RFBtSENNalE&export=download)

Đặc tính của React.js là khiến các component luôn ở trạng thái stateless một cách nhiều nhất có thể, khiến ta dễ dàng quản lý chúng

```js
var Form = React.createClass({
  onSubmit: function() {
    // Inform change to parent component
  },
  render: function() {
    return <form onSubmit={this.onSubmit}>...</form>;
  }
});

var List = React.createClass({
  render: function() {
    // Reform based on data received from parent component
    return <ul>{this.props.list.map(...)</ul>;
  }
});
```

Các component nhận data từ lớp mẹ và dựa vào đó để xây dựng View. Điểm mấu chốt ở đây là bản thân các component không mang một trạng thái nào. Nó chỉ có việc xuất ra hiển thị dựa vào những đầu vào từ bên ngoài (thường là từ component mẹ). Do đó những component đó sẽ dễ quản lí, dễ test và dễ tái sử dụng.

![State flow](https://drive.google.com/uc?id=0B05rqFCwNCjkSkF1X3g4emgyVEk&export=download)

Tất nhiên là nếu tất cả các component đều stateless thì chẳng khác nào 1 trang HTML tĩnh, vì thế ta cần cả những component có state nữa. Tuy nhiên, quan điểm của React.js là tối giản những component như vậy và xây dựng UI dựa vào những component stateless là chủ yếu.

Theo như biểu đồ hình cây bên dưới, chỉ phần gốc là có trạng thái còn tất cả các nhánh đều không cần.

Hơn nữa, khi ta thêm trạng thái cho một component thì cấu trúc của cây cũng sẽ tự động thay đổi. Ta không cần phải tự tay làm.  Về điểm này thì nó giống Angular – dữ liệu thay đổi thì hiển thị tự động thay đổi theo.

![Auto bind](https://drive.google.com/uc?id=0B05rqFCwNCjkWUxQRFBBMEVvVXM&export=download)

Về cơ bản thì trừ gốc ra, các component khác nên là stateless. Tuy nhiên, khi data phải thay đổi theo các input element hay user action thì khi đó vẫn cần có state. Vì vậy đôi khi ta không cần cố gắng để làm các component là stateless để nhằm mục đích tăng tốc độ cho website vì với kết quả đo như trên ta có thể thấy nó không nhanh hơn được bao nhiêu.

### Sử dụng hàm `shouldComponentUpdate`

`shouldComponentUpdate` là 1 người bạn tốt. Hãy sử dụng nó. Đừng sử dụng stateless component nếu ta có thể tối ưu hóa với hàm `shouldComponentUpdate`. Như chúng ta đã biết hàm `shouldComponentUpdate` thực hiện khi state và props thay đổi. Hàm này sẽ trả về kết quả true/false.

![shouldComponentUpdate](https://drive.google.com/uc?id=0B05rqFCwNCjkZTFqaWJTNDdqY2c&export=download)

Chúng ta sẽ sử dụng đến hàm này để xử lý xem có cần update component hay không. Hãy thử tưởng tượng, chúng ta cần render ra 1 dropdown list với 1 list các item rất lớn và css cũng như html cho việc render ra component đó cũng rất lớn. Nếu bằng việc sử dụng hàm `shouldComponentUpdate` sẽ giúp chúng ta biết được khi nào cần render thành phần dropdown đó, tránh việc render không cần thiết.

```js
shouldComponentUpdate(nextProps, nextState) {
    // Hàm này thực hiện khi state và props thay đổi
    // Hàm này sẽ trả về kết quả true/false, bạn sẽ cần sử dụng đến hàm này để xử lý xem có cần update component không
}
```

### Render thông minh hơn

Các biểu đồ trên cho ta thấy rằng hàm render() ảnh hưởng rất nhiều đến performance của app. Render chính là hoạt động cuối cùng để tối ưu hóa update cây DOM.

Các cách render đơn giản để update cây DOM nhanh hơn.

- Sử dụng ít mã Javascript trong quá trình xử lý, điều này rất quan trọng với mobile site và app.
- Việc return các thay đổi ít hơn sẽ làm tăng tốc độ tính toán cho DOM ảo.
- Render của 1 thành phần cha (container) sẽ kéo theo các hàm render ở các component con render theo. Điều đó có nghĩa là khối lượng tính toán lớn, dẫn đến performance không tốt.

Thật vậy, việc chỉ sử dụng mỗi phần gốc có state và tái cấu trúc mọi thứ khi nó thay đổi khiến cho mô hình trở nên đơn giản. Nhưng, việc cả DOM tree phải thay đổi theo 1 phần nhỏ như vậy sẽ khiến cho tốc độ xử lý bị ảnh hưởng, và react đã sử dụng Virtual DOM để giải quyết việc đó.

Virtual DOM, nói 1 cách tổng quát,  là 1 object của JavaScript mang trong mình một DOM tree, mỗi khi data thay đổi thì tự tính toán phần chênh lệch của object so với tree thật, nhằm mục đích tối giản việc re-rendering vào tree thật.

Tuy nhiên, số lượng thay đổi nhiều cũng sẽ làm tăng sự tính toán của DOM ảo cũng ảnh hưởng rất nhiều đến performance.

### Đừng quên Build trong môi trường Production

![React Dev](https://drive.google.com/uc?id=0B05rqFCwNCjkYzRIMWw5d29ZVHc&export=download)

Mặc định, React source được set là development mode. Không ngạc nhiên khi render sẽ chậm đáng kể. Tại sao lại như vậy, Trong development mode, React rất chu đáo trong việc cung cấp cho chúng ta hệ thống báo lỗi khá tốt nhưng chính điều này làm chậm quá trình đổ dữ liệu nên khi chuyển sang production mode, toàn bộ hệ thống này sẽ không được sử dụng, tức là các thành phần báo lỗi không hoạt động nên performance tăng lên là điều hiển nhiên.

```js
module.exports = {
  plugins: [
    new webpack.DefinePlugin({
      'process.env': {NODE_ENV: 'production'}
    })
  ],
}
```

### Sử dụng bản min cho browser

Việc này đơn giản nhưng lại đem lại hiệu quả cũng tương đối (được ít nào hay ít đấy). Vì lý do gì đó mà node luôn kiểm tra xem app của chúng ta có chạy production mode(process.env.NODE_ENV) không và việc này rất tốn kém (khoảng 1/3 thời gian load). Rất nhiều người đã báo bug này lên React nên mong là trong thời gian không xa bug sẽ được fix.

Lưu ý là sử dụng cách này cho production mode thôi nhé không dùng cho development mode, không là sẽ rất khó để debug.