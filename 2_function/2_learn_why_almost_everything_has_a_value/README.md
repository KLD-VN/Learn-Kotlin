# Learn why (almost) everything has a value (Tìm hiểu vì sao (hầu hết) mọi thứ đều có giá trị)

Trong Kotlin hầu như mọi thứ là một biểu thức va có một giá trị ngay cả khi giá trị đó là **kotlin.Unit**

1. Trong file **Hello.kt** -> viết đoạn mã vào **main()** để gán **println()** vào một biến **isUnit** và in nó ra (**println()** không trả về giá trị, nó trả về kotlin.Unit)

```kotlin
val isUnit = println("This is an expression")
println(isUnit)

/**
 * => This is an expression
   kotlin.Unit
 */
```

2. Khai báo **val** gọi **temperature** và khởi tạo nó thành 10
3. Khai báo **val** gọi **isHot** gán giá trị trả vê là một câu lệnh **if/else**. Vì nó là biểu thức nên có thể sử dụng giá trị của biểu thức này ngay

```kotlin
val temperature = 10
val isHot = if (temperature > 50) true else false
println(isHot)

// => false
```

4. Sử dụng **string template**

```kotlin
val temperature = 10
val message = "The water temperature is ${ if (temperature > 50) "too warm" else "OK" }."
println(message)

// => The water temperature is OK
```

```diff
!Lưu ý:
Vòng lặp là ngoại lệ với "mọi thứ đều có giá trị". 
Không có giá trị hợp lý cho for loop hoặc while loop, vì vậy chúng không có giá trị. 
Nếu cố gắng gán giá trị của vòng lặp cho một thứ gì đó, trình biên dịch sẽ báo lỗi.
```