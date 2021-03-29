# Comprehend collections (Tổng hợp các bộ sưu tập)

Tìm hiểu thêm về collections, bào gồm lists, và một collection type mới, hash maps.

## Step 1: Learn more about lists (Tìm hiểu về danh sách)

1. Một số hàm tích hợp sẵn cho lists.

|  **Chức năng**                          | **Mục đích**
|  add(element: E)                        | Thêm một số mục vào mutable list
|  remove(element: E)                     | Xóa một mục khỏi danh sách có thể thay đổi
|  reversed()                             | Trả về một bản sao của danh sách với thứ tự ngược lại
|  contains(element: E)                   | Trả về **true** nếu danh sách có item
|  subList(fromIndex: Int, toIndex: Int)  | Trả lại một phần của list, từ chỉ mục đầu tiên trở lên nhưng không bao gồm chỉ mục thứ 2

2. Dùng REPL -> tạo list các số và gọi **sum()** -> tổng hợp tất cả element.

```kotlin
val list = listOf(1, 5, 3, 4)
val (n1, n2, n3) = numbers
println(list.sum())

// => 13
```

3. Tạo danh sách các chuỗi và tính tổng danh sách

```kotlin
val list2 = listOf("a", "bbb", "cc")
println(list2.sum())

// => ⇒ error: none of the following functions can be called with the arguments supplied:
```

4. Nếu phần tử không phải là thứ **List** biết cách tính tổng trực tiếp, chẳng hạn như một chuỗi -> có thể chỉ định cách tính tổng nó bằng cách sử dụng **.sumBy()** một hàm lambda để tính tổng đọ dài của mỗi chuỗi. Tên mặc định cho đối số lambda là **it** -> **it** đề cập đến từng phần tử của danh sách khi danh sách được duyệt qua.

```kotlin
val list2 = listOf("a", "bbb", "cc")
println(list2.sumBy { it.length })

// => 6
```

5. Bạn có thể làm nhiều thứ hơn với list. Một cách tốt để xem những chức năng khả dụng là tạo list trong IntelliJ IDEA, thêm dấu chấm, sau đó xem danh các chức năng bạn có thể dùng trong tooltip

<p align="center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/4_extensions/Gallery/2/tooltip.png" />
</p>

6. Chọn **listIterator()** từ list, sau đó duyệt qua list với một câu lệnh **for** -> in ra tất cả phần tử bằng dấu cách.

```kotlin
val list2 = listOf("a", "bbb", "cc")
for (s in list2.listIterator()) {
   println("$s")
}

// => a bbb cc
```

## STEP 2: Try out hash maps (Dùng thử bản đồ băm)

Có thể ánh xạ nhiều thứ đến bất cứ thứ gì khác bằng cách sử dụng **hashMapOf()**. Hashmap giống như một list các pair, trong đó giá trị đầu tiên đóng vai trò là key

1. Tạo một HashMap phù hợp với symptoms (các triệu chứng), keys (khóa), dieases(bệnh tật) của cá, giá trị.

```kotlin
val cures = hashMapOf("white spots" to "Ich", "red sores" to "hole disease")
```

2. Bạn có thể lấy lại value bệnh dựa vào key triệu chứng, sử dụng **get()** hoặc ngắn hơn là square brackets (dấy ngoặc vuông) **[]**.

```kotlin
println(cures.get("white spots"))
// => Ich

println(cures["red sores"])
// => hole disease


```

3. Thử chỉ định một symptom không có trong map.

```kotlin
println(cures["scale loss"])

// => null
```

Tùy thuộc vào dữ liệu ma, thông thường không thể có kết quả phù hợp cho một khóa khả thi -> Kotlin cung cấp function **getOrDefault()** để giải quyết trường hợp này.

4. Tra cứu một khóa không khớp, bằng cách sử dụng **getOrDefault()**

```kotlin
println(cures.getOrDefault("bloating", "sorry, I don't know"))
// => sorry, I don't know
```

5. Thay đổi mã sử dụng **getOrElse()** thay thế **getOrDefault()**

```kotlin
println(cures.getOrElse("bloating") { "No cure for this"})
// => No cure for this
```

Thay vì trả về gía trị mặc định đơn giản, bất kỳ mã nào nằm trong dấu **{}** đều được thực thi. Ví dụ trên **else** chỉ cần trả về một chuỗi, nhưng cũng có thể thú vị như việc tìm một trang web có cách chữa và trả lại nó<br/><br/>

Giống như **mutableListOf**, bạn cũng có thể thực hiện một **mutableMapOf**. Map có thể thay đổi cho phép bạn put và remove item. **mutable** nghĩa là có thể thay đổi, **immutable** nghĩa là không thể thay đổi<br/>

6. Lập bản đồ tôn kho có thể sửa đổi, ánh xạ chuỗi trang bị với số lượng vật phẩm. Tạo nó với một lưới cá trong đó, sau đó thêm 3 máy chà bể vào hành trang cùng với **put()** và gỡ bỏ lưới cá **remove()**

```kotlin
val inventory = mutableMapOf("fish net" to 1)
inventory.put("tank scrubber" , 3)
println(inventory.toString())
inventory.remvoe("fish net")
println(inventory.toString())

// => {fish net=1, tank scrubber=3}{tank scrubber=3}
```

```diff
!Chú ý:
Immutable -> hữu ích trong môi trường phân luồng, nơi có thể xảy ra sự cố nếu nhiều luồng chạm vào cùng một tập hợp.
```