# Learn about operators and types

## STEP1: explore numeric operators (Khám phá toán tử số)

```kotlin
1 + 1
=> 2 (Int)

1/2
=> 0 (Int)

1.0/2.0
=> 0.5 (Double)

2.0 * 3.5
=> 7.0 (Double)

6.0 * 50
=> 300.0 (Double)
```

* Kết quả của các phép toán giữ các loại toán hạng => 1/2 = 0, nhưng 1.0/2.0 = 0.5

* Kotlin giữ các số dưới dạng primitives (Nguyên thủy). Nhưng cũng cho phép gọi methods trên các số như thể chúng là các object

```kotlin
2.times(3)
=> 6        (Int)

10.5.plus(20)
=> 30.5     (Double)

1.div(3.0)
=> 0.3333.  (Double)
```

## Step 2: Practice using types (Thực hành sưe dụng types)

1. Xác định kiểu 

```kotlin
val i: Int = 6
```

2. Auto-completion

```kotlin
val b1 = i.toBytes()
```

3. Gán các biến thuộc các kiểu khác nhau

```kotlin
val b2: Byte = 1
println(b2)
=> 1

val i1: Int = b2
=> error: type mismatch (Loại không phù hợp): inferred type is Byte but Int was expected (Loại suy ra là Byte nhưng Int là kiểu mong muốn)
```

4. Thay thế kiểu gán 

```kotlin
val i4: Int = b2.toInt()
=> 1

val i5 Double = b2.toDouble()
=> 1.0
```

5. Underscores (dấu gạch dưới) giữa các số -> dễ đọc

```kotlin
val oneMillion = 1_000_000
val socialSecurityNumber = 999_99_9999L
val bytes = 0b1110111_111011101_01110101_1010101
```

```diff
+ Lưu ý: Kotlin hỗ trợ kiểu mạnh -> không cần khai báo
```


## Step 3: Learn the value of variable types (Tìm hiểu các loại biến)

Kotlin hỗ trợ 2 kiểu: var, val
* var: có thể thay đổi
* val: không thể thay đổi

```kotlin
var fish = 1
fish = 2

var aquarium = 1
aquarium = 2

=> error: val cannot be reassigned
```

* Xác định một số biến và chỉ định kiểu một cách rõ ràng

```kotlin
var fish: Int = 12
var lakes: Double = 2.5
```

## Step 4: Learn about strings
 
* Variable interpolation (Nột suy biến)

```kotlin
val numberOfFish = 5
val numberOfPlants = 12
"I have $numberOfFish fish" + " and $numberOfPlants plants"

// => I have 5 fish and 12 plants
```

* Biểu thức bên trong chuỗi

```kotlin
"I have ${numberOfFish + numberOfPlants} fish and plants"
// => I have 17 fish and plants
```
