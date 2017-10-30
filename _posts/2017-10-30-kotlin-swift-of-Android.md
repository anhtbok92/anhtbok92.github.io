---
layout: entry
title: Kotlin - Swift của Android
author: Nguyễn Tuấn Anh
author-email: victory1080@gmail.com
description: Ngày nay, Apple đã thay thế Object-C bằng Swift cho IOS.
---

Ngày nay, Apple đã thay thế Object-C bằng Swift cho IOS. Những ngôn ngữ mới xuất hiện để thay thế Java cho lập trình Android là điều hiển nhiên. Những ngôn ngữ như Scala, Groovy thật tiện lợi và mang lại nhiều tính năng mới mẻ.

Nhưng đáng chú ý gần đây chính là Kotlin. Một ngôn ngữ lập trình được tạo ra bởi JetBrains – hãng sản xuất ra các IDE tiện lợi và mạnh mẽ như **PHPStorm**, **IntelliJ** và **Android Studio**. Chúng ta hãy cùng đi qua các tính năng mới của Kotlin mang lại, cũng như tìm hiểu lập trình Android bằng Kotlin như thế nào.

### 1. Kotlin là gì?

Kotlin là ngôn ngữ lập trình kiểu tĩnh, chạy trên máy ảo JVM, được tạo ra bởi JetBrains. Cái tên Kotlin xuất phát từ một hòn đảo gần thành phố **Saint Petersburg (Nga)** – nơi JetBrains hoạt động nghiên cứu và phát triển. So với Java, Kotlin đang dần trở nên phổ biến bởi cú pháp ngắn gọn, hiện đại, an toàn và được xem là người kế nhiệm của Java.

Theo JetBrains, Java có những hạn chế và các vấn đề “hoặc không thể hoặc rất khó để sửa chữa do những vấn đề về tính tương thích ngược”. Vào ngày 15/2/2016 **phiên bản 1.0** đã được released. Nếu bạn đang tìm kiếm một ngôn ngữ cho việc **phát triển Android**, thì bạn nên thử qua Kotlin. Nó có thể thay thế hoàn toàn hoặc kết hợp cùng với Java trong dự án Android của bạn.


### 2. Các đặc điểm của Kotlin

#### Khai báo biến

Có 2 từ khóa khai báo biến trong Kotlin là `var` và `val`

```
val a: Int = 1
val b = 1   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 1       // definite assignment
```

```
var x = 5 // `Int` type is inferred
x += 1
```

- Từ khóa `var` sử dụng khi giá trị của biến thay đổi, `val` sử dụng khi giá trị của biến không thay đổi
- Từ khóa `val` giống như `readonly` trong C# hoặc final trong Java
- Biến `val` phải được khởi tạo lúc khai báo
- Từ khóa `Void` trong java hay C# sẽ được thay thế bằng `Unit` trong Kotlin

#### Null Safety

Một trong  những cạm bẫy phổ biến trong các ngôn ngữ lập trình, bao gồm cả Java là cho phép 1 thành phần nào đó được Null. Nếu không chắc chắn thành phần đó được phép Null hay không sẽ rất dễ xảy ra lỗi không lường trước được, gây nguy hiểm cho hệ thống của bạn. Cụ thể, trong java sẽ gây ra 1 exception là *NullPoiterException* hoặc viết ngắn gọi là NPE.

Kotlin nhằm mục đích xóa bỏ *NullPoiterException* trong code của chúng ta. Ngay khi khai báo biến với Kotlin, bạn đã phải chỉ rõ biến đó có được phép Null hay không. Có 2 trường hợp được phép đó là : **không thể** Null và **có thể** Null

- Khai báo 1 biến cho phép Null
```
var b: String? = "abc" // có thêm dấu ? sau kiểu của biến
b = null // compilation ok
val l = b.length // not safe
```
- Khai báo 1 biến không được phép Null
```
var a: String = "abc"
a = null // compilation error
val l = a.length // safe
```

Chúng ta có thể thấy Kotlin đã khắc phục được NPE trong Java. Các biến cho phép Null hay không được phép Null đã được xác định ngay trong quá trình khai báo biến, các **IDE** sẽ giúp chúng ta phát hiện ra lỗi ngay khi **compile**. Việc phát hiện ra lỗi sớm khi **compile** sẽ tốt hơn so với khi **runtime**. Nó giúp hệ thống của chúng ta an toàn hơn.

#### String template

String trong kotlin có thể chứa các biểu thức template, tức là những kết quả trả về hoặc biến có thể được nối vào trong 1 String. Một biểu thức template bắt đầu với ($) và tên.

```
val apples = 4
valbananas = 3
println(“I have $apples apples.”)
println(“I have $apples apples and ” + (apples + bananas) + “ fruits.”)

println(“I have $apples apples and ${apples + bananas} “ fruits.”)
```

#### Kế thừa và Override

Mặc định class trong Kotlin đều là final (tức là không được phép kế thừa).
```
open class Base {
    open fun v() {}
    fun nv() {}
}

class Derived() : Base() {
   override fun v() {}
}
```

Trong class final (tức là không có từ khóa “open”) thì việc khai báo các hàm, thuộc tính open bị cấm.

Ở 1 lớp con khác, hàm được đánh dấu là override thì chính nó là open (lại được kế thừa từ lớp khác), nếu muốn chống override thì lại sử dụng từ khóa final.
```
open class AnotherDerived() : Base() {
    final override fun v() {}
}
```

Trong interface, các member mặc định là "open".
```
interface B {
    fun f() { print("B") } // interface members are 'open' by default
    fun b() { print("b") }
}
```

Kotlin implement interface:
```
class C() : A(), B {
     // The compiler requires f() to be overridden:
     override fun f() {
         super<A>.f() // call to A.f()
         super<B>.f() // call to B.f()
     }
}
```

#### Chỉ định truy cập (Visibility Modifiers)

- Có 4 loại Visivility Modifiers trong Kotlin : **private**, **protected**, **internal**, và **public**.
- Nếu không chỉ rõ thì mặc định là **public**.
- Các chỉ định truy cập : **private**, **protected** và **public** giống cách sử dụng trọng java.
- Riêng **internal** ta có thể sử dụng trong cùng module.

#### Truyền tham số trong hàm

Kotlin cho phép thay đổi vị trí tham số trong hàm.
```
fun main(args : Array<String>) { 
    greet(firstName = "Frasensco", lastName = "Merini") 
    greet(lastName = "John", firstName = "Stamos") 
    greet("Borat", "Ismail") 
    greet("Crystal", lastName = "Stamos") 
    call("Xavier", age = 20, location = "Portugal") 
} 

fun greet(firstName : String, lastName : String){
    println("Good morning $firstName $lastName") 
} 

fun call(name : String, location : String, age : Int){ 
    println("Call $name who lives at $location and he is $age old") 
}
```

**Output:**

```sh
Good morning Frasensco Merini
Good morning Stamos John
Good morning Borat Ismail
Good morning Crystal Stamos
Call Xavier who lives at Portugal and he is 20 old
```

### 3. Cài đặt Kotlin trong Android Studio

Trong màn hình truy xuất nhanh của Android Studio, chọn **Configure > Plugins,  **hoặc chọn menu **Preferences**

![Kotlin 1](https://drive.google.com/uc?id=0B05rqFCwNCjkMmpkVkl4X1JJZ0E&export=download)

Trong màn hình kế tiếp , nhấp vào **Install JetBrains plugin…** ở phía dưới.

Chọn **Kotlin Extensions For Android** từ danh sách và nhấp vào **Install Plugin** ở phía bên phải.

![Kotlin 2](https://drive.google.com/uc?id=0B05rqFCwNCjkX1R6dnhPWlQydXM&export=download)

**Restart Android Studio** và thưởng thức Kotlin !!!

![Kotlin 3](https://drive.google.com/uc?id=0B05rqFCwNCjkRGt4MkhxVHROWjA&export=download)

### 4. Kết Luận

**Kotlin** cũng giống như nhiều ngôn ngữ lập trình không phải Java khác, tức là cũng sẽ chạy trên **JVM** và sử dụng các công cụ và thư viện hiện có của **Java**. Và ngược lại **Java** cũng có thể sử dụng các item được xây dựng trong **Kotlin**.

Theo website **JetBrains**, mục tiêu quan trọng của Kotlin là **tính hữu dụng**. Từ lúc giới thiệu vào năm 2011 cho đến khi phát hành phiên bản 1.0, JetBrains đã luôn chú trọng đến tính **tương hợp với Java.**

Mặc dù Kotlin có một số tính năng hoàn toàn mới chẳng hạn như một **type system** được thiết kế để ngăn chặn các bug như các **null pointer reference**, nhưng quan trọng là nó làm việc cùng với code và cơ sở hạ tầng hiện có của **Java**. Cuối cùng, **Kotlin** không có trình quản lý gói và build system của riêng nó, do Java đã có sẵn.

Kotlin đã được phát triển phần nào để mang đến sức mạnh cho IntelliJ Idea Java IDE. Thay vì sử dụng **Scala** – một ngôn ngữ dựa trên **JVM** khác – **JetBrains** đã chọn lựa việc xây dựng từ lúc chưa có gì trong khi tạo ra ngôn ngữ mới thu hút các lập trình viên Java hiện có và việc học ngôn ngữ mới dễ dàng hơn Scala.

Lập trình Android là một trong những lĩnh vực quan trọng mà JetBrains hướng đến với Kotlin. Ngôn ngữ mang đến tính tương thích ngược với Java 6 và 7, các phiên bản của Java hầu hết đều tương thích chặt chẽ với Android. **JetBrains** cũng hy vọng **Kotlin** sẽ được sử dụng trong các lĩnh vực khác chẳng hạn như các ứng dụng lớn và phức tạp, đề cao hiệu suất. Hãy thử Kotlin kết hợp cùng với Java trong dự án của bạn, chắc chắn nó sẽ mang lại cho bạn những tiện ích và trải nghiệm thú vị !


### Tham khảo

- [https://kotlinlang.org/docs/reference/java-interop.html](https://kotlinlang.org/docs/reference/java-interop.html)
- [https://kotlinlang.org/docs/tutorials/](https://kotlinlang.org/docs/tutorials/)
- [https://kotlinlang.org/docs/reference/](https://kotlinlang.org/docs/reference/)
- [https://gist.github.com/dodyg/5823184](https://gist.github.com/dodyg/5823184)


