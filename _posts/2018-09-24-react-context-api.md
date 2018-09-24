---
layout: entry
title: React Context API
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Trong phiên bản React 16.3.0 đã giới thiệu khá nhiều khái niệm và tính năng mới của React
---

### 1 Context API là gì ?
Trong các phiên bản trước của React, context được sử dụng như 1 tham số thứ 2 trong constructor của 1 component
theo kiểu sau: 

```
class MyComponent extends React.Component {
  constructor(props, context) {
    super(props, context)
  }
}
```

Tính ứng dụng của context trong các phiên bản trước cũng vô cùng hạn hẹp vì có khuyến cáo nó sẽ bị thay đổi
trong tương lai nên việc sử dụng nó cũng được nhiều người cân nhắc. Nhưng từ phiên bản React 16.0.3
mọi thứ đã hoàn toàn thay đổi, khái niệm context đã được cải tiến và được giới thiệu như 1 cơ chế quản lý state 
của ứng dụng như Redux và Flux

### 2 Tại sao nên sử dụng React Context API

Khi sử dụng React, chúng ta rất khổ sở, nhiều khi mất ăn mất ngủ để refactor code sao cho thật đẹp,
nhưng khổ nỗi, với các version trước 16.3.0 chúng ta muốn truyền dữ liệu từ component ông nội xuống component
cháu chắt, không còn cách nào khác là chúng ta phải đi đúng trình tự component ông nội -> component cha -> component con
-> component cháu -> component chắt...

Ví dụ như sau : 
Giả sử component ông nội chỉ muốn truyền cho component cháu 10 tỷ, lúc này component ông nội không còn cách nào khác
là truyền money qua component bố, mặc dù component bố không sử dụng hoặc component ông nội không muốn, nhưng vẫn bắt buộc
phải truyền

```
const Chau = (props) => (
  <div className="chau">{props.money}</div>
);

const Bo = (props) => (
  <div className="bo">
    <Chau number={props.money} />
  </div>
);
 
class Ong_Noi extends Component {
  state = {
    money : 10
  };
  
  render() {
    return  <div className="ong_noi">
      {this.state.money}
      <Bo number={this.state.money} />
    </div>
  }
};

```

Trên đây là 1 ví dụ rất đơn giản cho việc truyền dữ liệu từ các component có quan hệ. Thử hình dung, 1 app chúng ta có 
hàng chục thâm chí hàng trăm component có quan hệ huyết thống, mà chúng ta vẫn phải truyền dữ liệu như 
cách trên thì thật là thảm họa. Thực tế, các ứng dụng thường sẽ có rất nhiều quan hệ phân cấp sâu, điều này thực sự đã làm
đau đầu rất nhiều lập trình viên React.

Thật may, có nhiều giải pháp cho vấn đề trên, khi có rất nhiều thư viện của bên thứ 3 support chúng ta định nghĩa các
store và truy xuất chúng khi cần. Có thể kể đến những thư viện rất nổi tiếng như Redux và Mobx. Chúng giúp ta không cần 
phải truyền data bằng props qua nhiều cấp nữa, mà thay vào đó, chúng sẽ tạo cho chúng ta 1 "global state" và khi component
nào cần sử dụng, thì có thể truy xuất tự nhiên. =))

Nhưng, với Redux, dù gì cũng là 1 lib bên ngoài, khi làm quen với Redux chúng ta phải gặp 1 đống các khái niệm mà có lẽ đối với 
người mới tìm hiểu cũng khá ngợp như React, JSX, Babel, Webpack...
Nếu React chính chủ lại có thể giải quyết công việc đó 1 cách êm đẹp thì tại sao lại không sử dụng nhỉ ?
. Và React Context hoàn toàn sẽ giúp chúng ta thay thế được Redux khi chúng ta gặp bài toán truyền data qua nhiều cấp thông qua props như
trên.


### 3 Luồng làm việc của React Context

1. Khai báo context ở component root (component to nhất trong App của bạn)
2. Tạo 1 method ở Root, có thể set/get state
3. Truyền method đó qua context
4. Khai báo nhận context ở các component con. Các component con chỉ việc sủ dụng method này để get/set state của Root
5. Mọi thông tin thay đổi ở component con, sẽ được update state ở component cha và component cha sẽ có nhiệm vụ render lại App
một cách tự động

Trong bước 1, chúng ta khởi tạo giá trị ban đầu cho context api bằng cách `React.createContext`, hàm này sẽ trả về 1 object
bao gồm là `Provider` và `Consumer`

```
const {Provider, Consumer} = React.createContext(defaultValue);
```

Chú ý rằng Provider được sử dụng trong Root component và giá trị được truyền thông qua props là `value`. Các
component con có thể sử dụng ở bất cứ nơi đâu dưới `Provider` bằng cách sử dụng `Consumer` có thể get giá trị truyền qua props `value`
của `Provider` thông qua props children

### 4 Quản lý state bằng React Context

Đến đây, chúng ta đã hiểu về khái niệm Context trong React và biết về luồng làm việc của React Context. Để dễ hình dung hơn chúng ta sẽ
làm 1 code demo để hiểu hơn về context

Chúng ta sẽ làm 1 ứng dụng Increment. Mình đã đọc và tham khảo code ở đây
https://hackernoon.com/how-to-use-the-new-react-context-api-fce011e7d87
Đây là 1 ứng dụng theo mình đánh giá là nhanh làm và dễ hiểu nhất đối với React Context. Mình sẽ
giải thích từng dòng code theo 5 bước bên trên để mọi người có thể áp dụng.

App chúng ta làm sẽ như hình dưới đây:

![list](/images/react-native/demo.gif) 

Chúng ta sẽ có 3 component có quan hệ huyết thống. Màu đỏ là component ông nội, màu xanh lam là component cha và
màu xanh lá cây là componet con.

Bước 1: Khai báo context ở component Root
Bước 2: Biến state là 1 object number, có thể thay đổi bằng hàm setState
Bước 3: Truyền method và các biến qua props value 
```
const AppContext = React.createContext()
```

```
class AppProvider extends Component {
  state = {
    number : 10,
  }
render() {
    return (
        <AppContext.Provider value={this.state}>
           {this.props.children}
        </AppContext.Provider>
    )
  }
}
```

Bước 4: Khai báo nhận context ở các component con. Sau khi setup xong Provider ở trên chúng ta có thể truy xuất data bằng cách 
sử dụng `Context Consumer`. Đến đây, ta đã gọi được biến context ở AppProvider. Ta không cần truyền props number xuống 2 component
Blue và Green nữa. Tất cả dữ liệu đã được xử lý bởi React Context

```
class Red extends Component {
  render() {
    return  <AppProvider> 
        <div className="red">
          <AppContext.Consumer>
            {(context) => context.number}
          </AppContext.Consumer>
          <Blue />
        </div>
    </AppProvider>
  }
}
```

```
const Blue = () => (
  <div className="blue">
    <Green />
  </div>
)
```

```
const Green = () => (
  <div className="green">
      <AppContext.Consumer>
        {(context) => context.number}
      </AppContext.Consumer>
  </div>
)
```

