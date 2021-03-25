# Explore default values and compact functions (Khám phá các giá trị mặc định và các chức năng gọn nhẹ)

Tìm hiểu về giá trị mặc định cho các **functions** và **methods**

```diff
!Lưu ý:
-> Method và Function khá giống nhau trong cách hoạt động
-> Điểm khác nhau chính giữa Method và Function là khái niệm Class và Object
-> Function có thể được gọi bởi tên trong khi Method phải thông qua class hoặc object
-> Method định nghĩa trong class và phụ thuộc vào class đó
```

## Step 1: Create a default values and compact functions (Tạo một giá trị mặc định cho một tham số)

Trong Kotlin có thể truyền các đối số theo tên tham số. Có thể chỉ định giá trị mặc định cho arguments nếu người dùng không cung cấp đối số. 
Khi viết các 

1. Trong file **Hello.kt**, viết một hàm **swim()** + tham số có tên **speed** sau đó in ra tốc độ của cá. Giá trị mặc định của **speed** là **fast**

```kotlin
fun swim(speed: String = "fast") {
    println("swimming $speed")
}
```

2. Từ hàm **main()**, gọi hàm **swim()** theo 3 cách. Đầu tiên là hàm dùng giá trị mặc định.
Sau đó là gọi hàm và chuyền tham số **speed** mà không có tên, sau đó gọi hàm bằng cách đặt tên cho tham số **speed**

```kotlin
swim() // uses default speed
swim("slow") // positional argument
swim(speed="turtle-like") // named parameter

// => swimming fast
// => swimming slow
// => swimming turtle-like
```

```diff
!Lưu ý:
Đối số không nhất thiết phải dùng tên tham số; có thể chỉ chuyên các đối số theo thứ tự đã xác định.
Nên đặt các tham số không có giá trị mặc định trước và các tham số có giá trị mặc định sau
```

## Step 2: Add required parameters (Thêm các thông số bắt buộc)

Nếu không có giá trị mặc định nào được chỉ định cho một tham số, thì đối số tương ứng phải luôn được truyền

1. Trong file **Hello.kt**. Viết một hàm **shouldChangeWater()** nhận 3 tham số: **day**, **temperature**, **dirty**.
Hàm sẽ trả về **true** nếu nước cần được thay đổi, điều này xảy ra vào **Sunday** nếu **temperature** (nhiêt độ) quá cao hoặc nước quá **dirty** (bẩn).
Mặc định **temperature** là 22 và **dirty** là 20.

* Sử dụng **when** không có đối số -> như một chuỗi các câu lệnh **if/else if**

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20) : Boolean {
    return when {
        temperature > 30 -> true
        dirty > 30 -> true
        day == "Sunday" -> true
        else -> false
    }
}
```

2. Gọi **shouldChangeWater()** từ hàm **feedTheFish()** và cung cấp ngày. **day** không có giá trị mặc định nên cần chỉ định argument.

```kotlin
fun feedTheFish() {
    val day = randomDay()
    val food = fishFood(day)
    println ("Today is $day and the fish eat $food")
    println("Change water: ${shouldChangeWater(day)}")
}

// => Today is Sunday and the fish eat plankton
// => Change water: true
```

## Step 3: Make compact functions (Tạo các chức năng nhỏ gọn)

Các hàm nhỏ gọn hay còn gọi là [single-expression function](single-expression-functions), common pattern (mẫu chung) trong Kotlin.
Khi một hàm trả về kết quả của một biểu thức duy nhất, có thể chỉ định phần thân hàm sau một ký hiệu dấu **=**, bỏ qua **{}** và **return**

1. Trong file **Hello.kt**, thêm compact functions

```kotlin
fun isTooHot(temperature: Int) = temperature > 30

fun isDirty(dirty: Int) = dirty > 30

fun isSunday(day: String) = day == "Sunday"
```

2. Thay đổi hàm **shouldChangeWater()** để gọi các chức năng mới

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20) : Boolean {
    return when {
        isTooHot(temperature) -> true
        isDirty(dirty) -> true
        isSunday(day) -> true
        else -> false
    }
}
```

3. Chạy chương trình của bạn

## Default values

Gía trị mặc định cho một tham số không nhất thiết phải là một giá trị. Nó có thể là một chức năng khác

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = getDirtySensorReading()) : Boolean {
    ...
}
```

[single-expression-functions]:https://kotlinlang.org/docs/idioms.html#single-expression-functions

