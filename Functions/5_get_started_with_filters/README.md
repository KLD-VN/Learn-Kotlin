# Get started with filters (Bắt đầu với bộ lọc)

Filters là một cách tiện lợi để lấy một phần của danh sahcs dự trên một số condition (điều kiện)

## Step 1: Create a filter (Tạo một filter)

1. Trong file **Hello.kt**. Xác định một list đồ trang trí bể nuôi cá ở level cao nhất với **listOf()**.

```kotlin
val decorations = listOf("rock", "pagoda", "plastic plant", "alligator", "flowerpot")
```

2. Tạo mới một hàm **main()** chỉ một dòng để in ra các trang trí bắt đầu bằng chữ **p**.
Mã điều kiện filter nằm trong dấu **{}**, và **it** tham chiếu tới từng mục khi filter lặp lại.
Nếu biểu thức trả về **true** mục đó sẽ được bao gồm

```kotlin
fun main() {
    println( decorations.filter {it[0] == 'p'})
}

// => [pagoda, plastic plant]
```

## Step 2: Compare eager and lazy filters (So sánh bộ lọc hăng hái và lười biếng)

Mặc định trong Kotlin **filter** là eager (háo hức) và mỗi lần filter, một danh sách mới sẽ được tạo.

Để tạo filter lazy (bộ lọc lười biếng) -> sử dụng [Sequence](Sequence). Là tập hợp chỉ có thể xem một mục tại một thời điểm, bắt đầu từ đầu và đi đến cuối. Đây chính xác là API mà filter lazy cần.
1. Trong **Hello.kt** thay đổi code để gán danh sách đã filter cho biến gọi là **eager**

```kotlin
fun main() {
    val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")

    // eager, creates a new list
    val eager = decorations.filter { it[0] == 'p' }
    println("eager: $eager")
}
```

2. Bên dưới mã đó, đánh giá filter bằng cách sử dụng **Sequence** với **asSequence()**. Gán chuỗi cho một biến được gị **filtered** và in ra.

```kotlin
// lazy, sẽ đợi cho tới khi yêu cầu được evaluate (đánh giá)
val filtered = decorations.asSequence().filter { it[0] == 'p' }
println("filtered: $filtered")
```

**filtered** sẽ không chứa một danh sách mới - nó chứa một **Sequence** trong các phần tử danh sách và hiểu biết về filter để áp dụng cho các phần tử đó.
 Bất cứ khi nào truy cập các phần tử của **Sequence** -> bộ lọc sẽ được áp dụng -> trả về kết quả

 3. Force evaluation (Buộc đánh giá) -> sequence -> bằng cách chuyển đổi nó thành **List** với **toList()**.

 ```kotlin
// buộc đánh giá lazy list
val newList = filtered.toList()
println("new list: $newList")
 ```

 4. Chạy chương trình

 ```kotlin
// => eager: [pagoda, plastic plant]
// filtered: kotlin.sequences.FilteringSequence@5e9f23b4
// new list: [pagoda, plastic plant]
 ```

Để hình dung những gì đang xảy ra vơi **Sequence** lazy evaluation, sử dụng hàm **map()**. 


5. Với **decoration** danh sách như trên -> thực hiện phép chuyển đổi **map()** chỉ cần trả về phần tử đã chuyển qua + theem **prinln()** hiển thị mỗi khi phần tử được truy cập và gán chuỗi cho một biến **lazyMap**.

```kotlin
val lazyMap = decorations.asSequence().map {
   println("access: $it")
   it
}
```

6. In **lazyMap**, phần tử đầu tiên **lazyMap** sử dụng **first()**, in **lazyMap** được chuyển thành **List**

```kotlin
println("lazy: $lazyMap")
println("-----")
println("first: ${lazyMap.first()}")
println("-----")
println("all: ${lazyMap.toList()}")
```

7. Chạy chương trình . In **lazyMap** chỉ in ra tham chiếu đến **Sequence**, bên trong **println** không được gọi. In phần tử đầu tiên chỉ truy cập phần tử đầu tiên. Chuyển **Sequence** thành một **List** truy cập tất cả phần tử.

```
=> lazy: kotlin.sequences.TransformingSequence@37a71e93d
-----
access: rock
first: rock
-----
access: rock
access: pagoda
access: plastic plant
access: alligator
access: flowerpot
all: [rock, pagoda, plastic plant, alligator, flowerpot]
```

8. Tạo mới **Sequence** bằng cách sử dụng bộ lọc gốc trước khi dùng **map**.

```kotlin
val lazyMap2 = decorations.asSequence().filter { it[0] == 'p' }.map{
        println("access: $it")
        it
    }
println("-----")
println("filtered: ${lazyMap2.toList()}")
```

9. Chạy chương trình. Giống việc lấy phần tử đầu tiên, phần tử trong **println()** chỉ được gọi cho các phần tử được truy cập.


```
⇒
-----
access: pagoda
access: plastic plant
filtered: [pagoda, plastic plant]
```



[Sequence]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.sequences/