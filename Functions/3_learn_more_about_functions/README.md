# Learn more about functions (Tìm hiểu nhiều hơn về các hàm)

## Step 1: Create some functions (Tạo một số chức năng)

Tổng hợp những gì đã học và tạo các hàm với types khác nhau.


1. Viết một function **feedTheFish()** + **randomDay()** lấy một ngày ngẫu nhiên trong tuần. Sử dụng **string template** in ra một **food**.

```kotlin
fun feedTheFish() {
    val day = randomDay()
    val food  = "pellets"
    println("Today is $day and the firsh eat $food")

}
fun main(args: Array<String>) {
    feedTheFish()
}
```

2. Viết hàm **randomDay()** -> chọn một ngày ngẫu nhiên từ một mảng và trả về nó.

* Hàm **nextInt()** lấy một giới hạn số nguyên, trong đó giới hạn số từ **Random()** từ 0 đến 6 để phù hợp với mảng **week**.

```kotlin
fun randomDay(): String {
    val week = arrayOf ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
    return week[Random.nextInt(week.size)]
}
```

3. **Random()** và **nextInt()** functions được xác định trong **java.util.***. Thêm nó vào đầu file:

```kotlin
import java.util.* // required import
```
4. Chạy chương trình của bạn

```
=> Today is Tuesday and the fish eat pellets
```

## Step 2: Use a when expression (Xử dụng biểu thức when)

1. Trong file **Hello.kt** thêm function **fishFood()**, mỗi ngày là một **String** và trả về thức ăn của cá dưới dạng một **String**. Sử dụng **when**, để mỗi ngày cá nhận được một loại thức ăn cụ thể.

```kotlin
fun fishFood (day : String) : String {
   var food = ""
   when (day) {
      "Monday" -> food = "flakes"
      "Tuesday" -> food = "pellets"
      "Wednesday" -> food = "redworms"
      "Thursday" -> food = "granules"
      "Friday" -> food = "lettuce"
      "Saturday" -> food = "lettuce"
      "Sunday" -> food = "plankton"
   }
   return food
}

fun feedTheFish() {
   val day = randomDay()
   val food = fishFood(day)

   println("Today is $day and the fish eat $food")
}

// => Today is Monday and the fish eat flakes
```

2. Thêm nhánh mặc định vào **when** -> sử dụng **else**

* Có một nhánh mặc định đảm bảo **food** sẽ nhận được giá trị trước khi trả về -> không cần khởi tạo nữa -> khai báo **food** với **val** thay vì **var**

```kotlin
fun fishFood (day: String) : String {
    val food: String
    when (day) {
        "Monday" -> food = "flakes"
        "Thursday" -> food = "granules"
        "Friday" -> food = "mosquitoes"
        "Saturday" -> food = "lettuce"
        "Sunday" -> food = "plankton"
        else -> food = "nothing"
    }
    return food
}
```

3. Mọi biểu thức đều có một giá trị -> có thể trả về giá trị của biểu thức **when** và loại bỏ **food**. Giá trị của **when** là giá trị của biểu thức cuối cùng của nhánh thỏa mã điều kiện

```kotlin
fun fishFood (day: String) : String {
    return when (day) {
        "Monday" -> "flakes"
        "Thursday" ->  "granules"
        "Friday" ->  "mosquitoes"
        "Saturday" ->  "lettuce"
        "Sunday" ->  "plankton"
        else ->  "nothing"
    }
}
```

Và đây là phiên bản cuối cùng của chương trình


```kotlin
import java.util.* // required import

fun feedTheFish() {
    val day = randomDay()
    val food  = fishFood(day)
    println("Today is $day and the fish eat $food")

}

fun main(args: Array<String>) {
    feedTheFish()
}

fun randomDay(): String {
    val week = arrayOf ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")
    return week[Random().nextInt(week.size)]
}

fun fishFood (day: String) : String {
    return when (day) {
        "Monday" -> "flakes"
        "Thursday" ->  "granules"
        "Friday" ->  "mosquitoes"
        "Saturday" ->  "lettuce"
        "Sunday" ->  "plankton"
        else ->  "nothing"
    }
}
```