# Get started with lambdas and higher-order functions (Bắt đầu với lambdas và các hàm bậc cao hơn)


Giới thiệu về [lambdas and higher-order functions](https://kotlinlang.org/docs/lambdas.html) trong Kotlin.

## Lambdas

**Lambdas** -> Khai báo hàm không tên. Một phần của của điều làm cho nó hữu ích là biểu thức lambda hiện có thể 
được chuyển dưới dạng dữ liệu. Ở các ngôn ngữ khác -> gọi là **anonymous function**, **function literals** hoặc các tên tương tự.

## Higher-order functions

Có thể tạo một hàm bậc cao hơn bằng cách truyền một lambda cho một hàm khác. Ví dụ như biểu thức lambda sau **filter**  làm điều kiện 
để kiểm tra: **{it[0] == 'p'}**


## Step 1: Learn about lambdas (Tìm hiểu về lambdas)


1. Lambdas có thể có các tham số. Các tham số (và kiểu nếu cần) nằm ở bên trái mũi tên hàm **->**. Mã thực thi nằm ở bên phải mũi tên
hàm. Khi lambda được gán cho một biến, bạn có thể gọi nó giống như một hàm.

```kotlin
var dirtyLevel = 20
val waterFilter = { dirty : Int -> dirty / 2}
println(waterFilter(dirtyLevel))

// => 10
```

Lambda nhận một **Int** tên **dirty** và trả về **dirty/2**

2. Cú pháp khai báo rõ ràng một biến chứa một hàm

```kotlin
val waterFilter: (Int) -> Int = { dirty -> dirty / 2}
```

* Thực hiện một biến được gội **waterFilter**
* **waterFilter** có thể là bất kỳ hàm nào nhận một **Int** và trả về một **Int**
* Gán một lambda cho **waterFilter**
* Lambda trả về giá trị của đối số **dirty** chia cho 2.

```diff
!Lưu ý
Không phải chỉ định kiểu của đối số lambda. Kiểu được tính toán sẽ được suy luận ra
```

## Step 2: Create a higher-order function (Tạo một hàm bậc cao hơn)

Sức mạnh thực sự của lambdas là sử dụng để tạo các hàm bậc cao hơn, trong đó đối số của một hàm là một hàm khác.

1. Viết một hàm bậc cao -> một hàm có 2 đối số -> một số nguyên + một function nhận một số nguyên và trả về một số nguyên.

```kotlin
fun updateDirty(dirty: Int, operation: (Int) -> Int): Int {
   return operation(dirty)
}
```

Phần thân của mã gọi hàm được truyền làm đối số thứ 2 và chuyển đối số đàu tiền cùng với nó

2. Gọi hàm -> chuyển cho nó một số nguyên và một function

```kotlin
val waterFilter: (Int) -> Int = { dirty -> dirty / 2 }
println(updateDirty(30, waterFilter))

// => 15
```

Hàm truyền không nhất thiết phải là lambda; có thể là một hàm đặt tên thông thường để thay thế. Chỉ định hàm thông thường,
sử dụng toán tử **::**. Bằng cách này Kotlin biết bạn đang truyền tham chiếu hàm dưới dạng đối số chứ không phải là gọi hàm.

```kotlin
fun increaseDirty( start: Int ) = start + 1

println(updateDirty(15, ::increaseDirty))

// => 16
```

```diff
!Lưu ý
"last parameter call syntax" -> giúp mã bạn gọn hơn. Trong trường hợp này, bạn có thể truyền lambda cho tham số hàm,
nhưng không cần đặ lambda bên trong dấu ngoặc đơn
```

```kotlin
var dirtyLevel = 19;
dirtyLevel = updateDirty(dirtyLevel) { dirtyLevel -> dirtyLevel + 23 }
println(dirtyLevel)

// => 42
```


[last parameter call syntax](last-parameter-call-syntax)

[lambdas-and-higher-order-functions]: https://kotlinlang.org/docs/lambdas.html
[last-parameter-call-syntax]: https://kotlinlang.org/docs/lambdas.html#passing-a-lambda-to-the-last-parameter