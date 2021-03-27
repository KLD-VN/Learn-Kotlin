# Learn about singletons, enums, and sealed classes (Tìm hiểu về singleton, enums và các lớp niêm phong)

* Singleton classes
* Enums
* Sealed classes

# Step 1: Recall singleton classes (Nhớ lại các lớp singleton)

Ví dụ với **GoldColor**

```kotlin
object GoldColor: FishColor {
   override val color = "gold"
}
```

Bởi vì trong mọi trường hợp **GoldCOlor** làm những điều tương tự nhau -> kahi báo dưới dạng **object** thay vì **class** => khiến nó trở thành một singleton. Chỉ có thể có một trường hợp của nó

## Step 2: Create an enum (Tạo một enum)

Cho phép liệt kê một cái gì đó và gọi nó bằng tên. Khai bao enum bằng cách đặt tiền tố khai báo với từ khóa enum. Một khai báo cơ bản chỉ cần một danh sách các tên, cũng có thể xác định một hoặc nhiều trường liên kết với mỗi tên.

1. Trong **Decoration.kt** 

```kotlin
enum class Color (val rgb: Int) {
    RED(0xFF0000), GREEN(0x00FF00), BLUE(0x0000FF)
}
```

Enum hơi giống singletons - chỉ có thể có một và chỉ một trong mỗi giá trị trong phép liệt kê. Ví dụ: chỉ có thể có một **Color.RED**, một **Color.GREEN** và một **Color.BLUE**. Trong ví dụ này, giá trị RGB gán cho property **rgb** đại diện cho các thành phần màu. Bạn cũng có thể lấy giá trị thứ tự của một enum bằng cách sử dụng thuộc tính **ordinal** và tên của nó bằng cách sử dụng thuộc tính **name**.

2. Ví dụ khác về enum

```kotlin
enum class Direction(val degrees: Int) {
    NORTH(0),  SOUTH(180), EAST(90), WEST(270)
}

fun main() {
    println(Direction.EAST.name)
    println(Direction.EAST.ordinal)
    print(Direction.EAST.degrees)
}
```

## Step 3: Create a sealed class (Tạo một lớp kín)

**sealed** class -> có thể phân subclasses, nhưng chỉ bên trong tệp mà nó được khai báo. Nếu cố gắng phần lớp trong một tệp khác, bạn sẽ gặp lỗi.

Vì các class và subclasses nằm trong cùng 1 file, Kotlin sẽ biết tất cả các lớp con tĩnh-> nghĩa là tại thời điểm biên dịch, trình biên dịch sẽ thấy tất cả classes và subclasses và biết rằng đây là tất cả.

1. Trong **AquariumFish.kt**,

```kotlin
sealed class Seal
class SeaLion : Seal()
class Walrus : Seal()

fun matchSeal(seal: Seal): String {
    return when(seal) {
        is Walrus -> "walrus"
        is SeaLion -> "sea lion"
    }
}
```

Các **Seal** class khong thể được subclassed trong tập tin khác. Nếu muốn thêm nhiều loại **Seal**, bạn phải thêm chúng trong cùng một tệp. Điều này làm cho sealed class trở thành một cách an toàn để đại diện cho một số kiểu cố định. Ví dụ [returning success or error from a network API](returning_success_or_error_from_a_network_API)


[returning_success_or_error_from_a_network_API]: https://articles.caster.io/android/handling-optional-errors-using-kotlin-sealed-classes/