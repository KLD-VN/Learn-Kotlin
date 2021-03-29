# Learn about pairs and triples (Tìm hiểu về cặp và bộ ba)

Pairs và triples là các class được tạo sẵn cho 2 -> 3 mục chung. Ví dụ: khi một hàm trả về nhiều hơn một giá trị.<br/>

Giải sử có một **List** cá, và function **isFreshWater()** để kiểm tra xem là cá nươc ngọt hay mặn. **List partition()** trả về 2 danh sách, một danh sách có các mục điều kiện **true** và danh sách kia cho các mục điều kiện là **false**.

```kotlin
val twoLists = fish.partition { isFreshWater(it) }
println("freshwater: ${twoLists.first}")
println("saltwater: ${twoLists.second}")
```

## Step 1: Make some pairs and triples (Tạo một số cặp và bộ ba)

1. Mở REPL **(Tools > Kotlin > Kotlin REPL)**
2. Tạo một pair, liên kết một phần thiết bị với những gì nó được sử dụng, sau đó in các giá trị. 
Có thể tạo một pair bằng các tạo một biểu thức kết nối 2 giá trị, chẳng hạn như 2 chuỗi với từ khóa **to**, sau đó sử dụng **.first** hoặc **.second** để tham chiếu tới từng giá trị.

```kotlin
val equipment = "fish net" to "catching fish"
println("${equipment.first} used for ${equipment.second}")

// => fish net used for catching fish
```

3. Tạo một triples và in nó với **toString()**, sau đó chuyểnt đổi nó thành một list với **toList()**. Tạo một triple bằng cách sử dụng **Triple()** 3 giá trị. Sử đụng **.first**, **.second** và **.third** để chỉ mỗi giá trị.

```kotlin
val numbers = Triple(6, 9, 42)
println(numbers.toString())
println(numbers.toList())

// => (6, 9, 42)
// => [6, 9, 42]
```

Ví dụ trên sử dụng cùng kiểu cho tất cả các thành phần của pair hoặc triple, nhưng điều này không bắt buộc. Nó có thể là một chuỗi, một số hoặc một list - thậm chí là một pair hoặc triple khác.

4. Tạo một pair trong đó phần đầu tiên của pair chính nó là một pair

```kotlin
val equipment2 = ("fish net" to "catching fish") to "equipment"
println("${equipment.first} is ${equipment.second}\n")
println("${equipment2.first.second}")

// => (fish net, catching fish) is equipment
// => catching fish
```

## Step 2 Destructure some pairs and triples (Phá hủy một số cặp và bộ ba)

Tách các cặp và bộ ba thành các phần của chúng được gọi là cơ cấu **destructure**. Gán pair hoặc triple cho số lượng biến thích hợp -> Kotlin sẽ gán giá trị của từng phần theo thứ tự.


1. Destructure một pair và in giá trị

```kotlin
val equipment = "fish net" to "catching fish"
val (tool, use) = equipment
println("$tool is used for $use")

// => fish net is used for catching fish
```

2. Destructure một triple và in các giá trị

```kotlin
val numbers = Triple(6, 9, 42)
val (n1, n2, n3) = numbers
println("$n1 $n2 $n3")

// => 6 9 12
```

```diff
!Lưu ý:
destructuring pair và triples hoạt động giống với data classes
```