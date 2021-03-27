# Create a data class (Tạo một lớp dữ liệu)

Một data class tương tự như **struct** trong một số ngôn ngữ khác -> chủ yếu để chứa một số dữ liệu. Tuy nhiên một object của data class vẫn là một object. Các object class trong Kotlin có mội số lợi ích bổ sung như -> in và sao chép.


# Step 1: Create a data class (Tạo mội lớp dữ liệu)

1. Thêm một package mới **decor** dưới **example.myapp** package để giữ code mới. -> Chuột phải **example.myapp** trong **Project** và chọn **File > New >Package**.

2. Tạo một class có tên **Decoration**

```kotlin
package example.myapp,decor

class Decoration {

}
```

3. Để tạo **Decoration** lớp dữ liệu, đặt tiền tố khai báo lớp bằng từ khóa **data**.
4. Thêm một thuộc tính **String** -> **rock** để cung cấp cho class một số data.

```kotlin
data class Decoration(val rocks: String){
}
```

5. Trong file, ngoài class -> thêm **makeDecorations()** function để tạo và in ra instance của một **Decoration** với **"granite"**.

```
=> Decoration(rocks=granite)
```

6. Trong **makeDecoration()**, khởi tạo thêm 2 **Decoration** object và cả 2 đều là **"slate"** và in chúng

```kotlin
fun makeDecorations() {
    val decoration1 = Decoration("granite")
    println(decoration1)

    val decoration2 = Decoration("slate")
    println(decoration2)

    val decoration3 = Decoration("slate")
    println(decoration3)
}
```

7. Trong **makeDecorations()**, thêm một câu lệnh print để in ra kết quả so sánh **decoration1** với **decoration2**, **decoration3** với **decoration2**. Sử dụng phương thức equals() được cung cấp bởi các lớp dữ liệu.

```kotlin
println(decoration1.equals(decoration2))
println(decoration3.equals(decoration2))
```

8. Chạy chương trình 

```
=> Decoration(rocks=granite)
Decoration(rocks=slate)
Decoration(rocks=slate)
false
true
```

```diff
!Lưu ý:
Có thể sử dụng == để kiểm tra xem d1 == d2 và d3 == d2. Trong Kotlin, sử dụng == trên các data class objects cũng giống như sử dụng equal() (structual equality). 
Nếu cần kiểm tra 2 biến có tham chiếu tới cùng một object hay không (referential equality), sử dụng táon tử ===.
```

Đọc thêm về [equality in Kotlin](equality)

```diff
!Lưu ý:
data class objects là objects -> gan một đối data class object cho một biến khác sẽ sao chép tham chiếu tới đói tượng đó, không phải nội dung. Để sao chép nội dung đối tượng mới -> sử dụng copy()
```

```diff
-Cảnh báo: Các hàm copy(), equal() và các tiện ích lớp dữ liệu khac chỉ tham chiêu các thuộc tính được xác định trong hàm tạo chính 
```

# Step 2. Use destructuring (Sử dụng cấu trúc hủy)

Để lấy thuộc tính của data object và  assign (gán) chúng cho biến -> chỉ định chúng từng biến một

```kotlin
val rock = decoration.rock
val wood = decoration.wood
val diver = decoration.diver
```

Thay vào đó có thể tạo các biến, một biến cho mỗi thuộc tính và gán đối tượng dữ liệu cho nhóm các biến. Kotlin đặt giá trị thuộc tính vào mỗi biến.

```kotlin
val (rock, wood, diver) = decoration
```

Đây gọi là [destructuring](destructuring-declaration) là một cách viết tắt hữu ích. Số lượng biến phải khớp với số thuộc tính và khai báo theo thứ tự khai báo trong class.

```kotlin
    val d5 = Decoration2("crystal", "wood", "diver")
    val (rock, wood, diver) = d5

    // Assign all properties to variables
    println(rock)
    println(wood)
    println(diver)
}
```

```
⇒ Decoration2(rocks=crystal, wood=wood, diver=diver)
crystal
wood
diver
```

Nếu không cần một hoặc nhiều thuộc tính, có thể bỏ qua chúng bằng cách sử dụng **_** tên biến thay thế

```kotlin
val (rock, _, diver) = d5
```

![equality]: https://kotlinlang.org/docs/equality.html
![destructuring-declaration]: https://kotlinlang.org/docs/reference/multi-declarations.html#destructuring-declarations