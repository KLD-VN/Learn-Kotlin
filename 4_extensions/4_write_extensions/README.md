# Write extensions (Viết phần mở rộng)

Việc viết các hàm tiện ích để mở rộng hành vi của một lớp là rất phổ biến. Kotlin cung cấp cú pháp thuận tiện để khai
báo các hàm tiện ích này: extension functions.<br/><br/>

Các extension functions cho phép thêm các chức năng vào một lớp hiện có mà không cần phải truy cập mã nguồn của nó. Ví dụ: ban có thể khai
báo chúng trong tệp **Extensions.kt** là một phần của package của bạn. Điều này không sửa đổi class, nhưng nó cho phép bạn sử dụng ký hiệu
dấu chấm khi gọi hàm trên các object của class đó.

## Write extension function (Viết hàm mở rộng)

1. Trong REPL, viết extension function đơn giản, **hasSpaces()** để kiểm tra một chuỗi có chứa khoảng trắng hay không.
Tên hàm được đặt trước với lớp mà nó hoạt động. Bên trong hàm, **this** tham chiếu đến đối tượng mà nó được gọi và **it** tham chiếu đến trình lặp trong lệnh gọi **find()**

```kotlin
fun String.hasSpaces(): Boolean {
     val found = this.find { it == ' ' }
     return found != null
 }
println("Does it have spaces?".hasSpaces())

// => true
```

2. Đơn giản hóa chức năng **hasSpaces()**. Các **this** không cần thiết một cách rõ ràng, và các chức năng có thể được giảm đến một biểu thức duy nhất và trở về, 
vì vậy dấu ngoặc nhọn **{}** không cần thiết.


```kotlin
fun String.hasSpaces() = find { it == ' ' } != null
```

## Step 2: Learn the limitations of extensions (Tìm hiểu những hạn chế của tiện ích mở rộng)

Các extension function chỉ có quyền truy cập và API cong khai của lớp mà chúng đang mở rộng. Các biến **private** không thể truy cập được.

1. Thử thêm chưc năng mở rộng vào thuộc tính đươc đánh dấu **private**.

```kotlin
class AquariumPlant(val color: String, private val size: Int)

fun AquariumPlant.isRed() = color == "red"    // OK
fun AquariumPlant.isBig() = size > 50         // gives error

// => error: cannot access 'size': it is private in 'AquariumPlant'
```

```diff
!Lưu ý:
Các extension function được giải quyết tĩnh, tại thời điểm biên dịch, dựa trên kiểu của biến.
```

2. Kiểm tra mã bên dưới và tìm ra những gì nó sẽ in

```kotlin
open class AquariumPlant(val color: String, private val size: Int)

class GreenLeafyPlant(size: Int) : AquariumPlant("green", size)

fun AquariumPlant.print() = println("AquariumPlant")
fun GreenLeafyPlant.print() = println("GreenLeafyPlant")

val plant = GreenLeafyPlant(size = 10)
plant.print()
println("\n")
val aquariumPlant: AquariumPlant = plant
aquariumPlant.print() 

// => GreenLeafyPlant
// AquariumPlant
```

**plant.print()** để in **GreenLeafyPlant** hoặc có thể muốn **aquariumPlant.print()** để in **GreenLeafyPlant** vì nó đã được gán giá trị **plant**.
Nhưng type được giải quyết tại thời điểm biên dịch, vì vậy **AquariumPlant** sẽ được in.

## Step 3: Add an extension property (Thêm thuộc tínht tiện ích mở rộng)

Ngoài cac extension function, Kotlin cũng cho phép bạn thêm các extension property. Giống như các extension function, bạn chỉ định lớp
bạn đagn mở rộng, theo sau là dấu chấm, theo sau là tên thuộc tính.

1. Vẫn hoạt động trong REPL, thêm thuộc tính tiện ích mở rộng **isGreen** vào **AquariumPlant**, thuộc tính này **true** nếu màu xanh lục.

```kotlin
val AquariumPlant.isGreen: Boolean
     get() = color == "green"
```

**isGreen** thuộc tính có thể được truy cập giống như một tài sản thông thường; khi được truy cập, getter cho **isGreen** được gọi để lấy giá trị.

2. In thuộc tính **isGreen** cho **aquariumPlant** biến và xem kết quả.

```kotlin
aquariumPlant.isGreen

// => res49: kotlin.Boolean = true
```

## Step 4: Know about nullable receivers (Biết về bộ thu nullable)

Lớp mà bạn extend gọi là **receiver** và có thể làm cho lớp đó vô hiệu. Nếu bạn làm điều đó, **this** biến được sử dụng trong phần thân
có thể được **null**. Bạn sẽ muốn nhận một nullable receivers nếu bạn mong đợi rẳng những người gọi sẽ muốn call method extend của bạn trên 
các biến nullable hoặc nếu bạn muốn cung cấp hành vi mặc định khi hàm của bạn được apply **null**.

1. Trong REPL, xác định một **pull()** phương thức sử dụng nullable receivers. Điều này biểu thị bằng dấu **?** sau type, trước dấu chấm. Bên trong body
, bạn có thể kiểm tra **this** có **null** không bằng cách sử dụng dot-apply **?.apply**.

```kotlin
fun AquariumPlant?.pull() {
   this?.apply {
       println("removing $this")
   }
}

val plant: AquariumPlant? = null
plant.pull()
```

2. Trong trường hợp này sẽ không có đầu ra khi bạn chạy chương trình. Bởi **plant** là **null**, bên trong **println()** không được gọi