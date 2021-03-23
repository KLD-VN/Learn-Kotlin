# Explore arrays, lists, and loops (Khám phá mảng, danh sách và vòng lặp)

Tìm hiểu về **arrays**, **lists** và những cách tạo vòng lặp khác nhau trong Kotlin

## Step 1: Make lists (Lập danh sách)

1. Khai báo list sử dụng **listOf** -> list này không thể thay đổi

```js
val school = listOf("mackerel", "trout", "halibut")
println(school)

// => [mackerel, trout, halibut]
```

2. Khai báo list có thể thay đổi được **mutableListOf**

```js
val myList = mutableListOf("tuna", "salmon", "shark")
myList.remove("shark")

// => true (Boolean)
```
**remove()** method trả về **true** khi xóa thành công item passed

```diff
+Note:
Một list được khai báo với val -> không thể thay đổi list mà biến refers (đề cập đến), nhưng có thể thay đổi nội dung trong list
```

## Step 2: Create arrays (Tạo các mảng)

Array trong kotlin không có mutable version (phiên bản có thể thay đổi). Kích thước khi tạo array là cố định. Chỉ có add hoặc remove bằng cách copying sang một mảng mới

Quy tắc về **var** và **val** giống như list

1. Khai báo mảng string sử dụng **arrayOf**. Dụng **java.util.Arrays.toString()** để in nó ra

```js
val school = arrayOf("shark", "salmon", "minnow")
println(java.util.Arrays.toString(school))

// => [shark, salmon, minnow]
```

2. Mảng được khai báo với **arrayOf** không liên kết type với các phần tử -> có thể mix các kiểu với nhau

```js
val mix = arrayOf("fish", 2)
println(java.util.Arrays.toString(mix))

// => [fish, 2]
```

3. Có thể khai báo type cho tất cả các phần tử trong mảng. Khai báo mảng integers sử dụng **intArrayOf()**. Sẽ có các trình xây dựng hoặc hàm khởi tạo tương ứng cho các mảng thuộc loại khác nhau

```js
val number = intArrayOf(1, 2, 3)
println(java.util.Arrays.toString(number))

// => [1, 2, 3]
```

```diff
+Note:
Sử dụng primitive type (kiểu nguyên thủy) như Int hay Byte sẽ tránh được overhead of boxing (boxing là việc bao bọc con số bằng một object) 
```

4. Kết hợp 2 mảng với toán tử **+**

```js
val numbers = intArrayOf(1,2,3)
val numbers3 = intArrayOf(4,5,6)
val food2 = numbers3 + numbers

println(food2[5])

// => 3
```

5. Lồng arrays và lists. Phần tử trong array có thể là list và ngược lại

```js
val numbers = intArrayOf(1, 2, 3)
val oceans = listOf("Atlantic", "Pacific")
val oddList = listOf(numbers, oceans, "salmon")
println(oddList)

// => [[I@3cd3cf6b, [Atlantic, Pacific], salmon]
```

* Phần tử đầu tiên **numbers** là một **Array**. Khi không sử dụng array utility (tiện ích mảng) để in value. Kotlin sẽ in ra địa chỉ thay vì nội dung của mảng

6. Tính năng khởi tạo arrays bằng code thay vì bằng 0.

```js
val array = Array (5) { it * 2 }
println(java.util.Arrays.toString(array))

// => [0, 2, 4, 6, 8]
```

* Mã khởi tạo nằm trong dấu **{}**. **it** là chỉ số của mảng bắt đầu từ 0

## Step 3: Make loops

1. Dùng **for** để lặp qua và in ra các phần tử của mảng


```js
val school = arrayOf("shark", "salmon", "minnow")
for (element in school) {
   println(element + " ")
}

// => shark salmon minnow 
```

2. Lặp qua **elements** và **indexes** cùng lúc

```js
for ((index, element) in school.withIndex()) {
     println("Item at $index in $element\n")
 }

 // Item at 0 in shark 
 // Item at 1 in salmon
 // Item at 2 in minnow
```

3. Chỉ định ranges (phạm vi) số hoặc ký tự , bảng chữ cái, nhảy **n** bước, lùi lại bằng **downTo**

```js
for (i in 1..5) print(i)

// => 12345

for (i in 5 downTo 1) print(i)

// => 54321

for (i in 3..6 step 2) print(i)

// => 35

for (i in 'd'..'g') print(i)

// => defg
```

4. Vòng lặp **while**, **do...while**, **repeat** và toán tử **++**, **--**

```js
var bubbles = 0
while (bubbles < 50) {
   bubbles++
}
println("$bubbles bubbles in the water\n")

do {
   bubbles--
} while (bubbles > 50) 
println("$bubbles bubbles in the water\n")

repeat(2) {
   println("A fish is swimming")
}

// => 50 bubbles in the water
// => 49 bubbles in the water
// => A fish is swimmingA fish is swimming
```
