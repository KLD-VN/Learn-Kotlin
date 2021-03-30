# Explore generic classes (Khám phá các lớp chung)

## Introduction to generics (Giới thiêu về generics)

Kotlin cho phép tạo generic type -> cho phép tạo một lớp chung và do đó làm cho lớp linh hoạt hơn nhiều.

Tưởng tượng bạn đang triển khai class **MyList** chứa một danh sách các item. Nếu không có generic -> cần triển khai phiên bản mới của **MyList** từng loại: một cho **Double**, một cho **String**, một cho **Fish**. Sử dụng generic bạn có thể tạo danh sách chung, vì vậy nó chứa bất kỳ loại đối tượng nào -> Giống như việc biến một type thành một **ký tự đại diện** cho bất kỳ type nào.

Để xác định một generic type -> đặt T trong dấu ngoặc nhọn **<T>** sau tên class. (Có thể dùng chữ cái hoặc tên dài hơn, nhưng quy ước chung cho một loại là T.)

```kotlin
class MyList<T> {
   fun get(pos: Int) : T {
      TODO("implement")
   }
   fun addItem(item: T) {}
}
```

Kiểu trả về cho **get()** là **T** và tham số cho **addItem()** là **T**.


## Step 1: Make a type hierarchy (Tạo hệ thống phân cấp loại)

1. Tạo mới một package dưới **src** và gọi nó là **generics**.
2. Trong **generics** package, tạo mới file **Aquarium.kt**
3. Lập hệ thống phân cấp loại nước. Bắt đầu bằng cách tạo **WaterSupply** một **open** class để nó có thể được phân lớp.
4. Thêm một **var** tham số boolean, **needsProcessing** -> tự động tạo ra một thuộc tính có thể thay đổi, cùng với một getter và setter.
5. Tạo một subclass **TapWater** extend từ **WaterSupply**, thiết lập **true** cho **needsProcessing** vì nước máy chứa chất phụ gia có hại cho cá.
6. Trong **TapWater** -> tọa một function **addChemicalCleaners()** đặt **needsProcessing** thành **false** sau khi làm sạch nước. Thuộc tính **needProcessing** có thể được thiết lập từ **TapWater**, vì nó mặc định là **public** và có thể truy cập vào các lớp con.

```kotlin
package generics

open class WaterSupply(var needsProcessing: Boolean)

class TapWater : WaterSupply(true) {
    fun addChemicalCleaners() {
        needsProcessing = false
    }
}
```

7. Tạo thêm 2 lớp con **WaterSupply**, gọi **FishStoreWater** là **LakeWater**. **FishStoreWater** không cần xử lý, nhưng **LakeWater** cần được lọc bằng **filter()** method. Sau khi lọc không cần xử lý lại -> **needsProcessing = false**.

```kotlin
class FishStoreWater : WaterSupply(false)

class LakeWater : WaterSupply(true) {
    fun filter() {
        needsProcessing = false
    }
}
```

## Step 2: Make a generic class (Tạo một class generic)

Sửa đổi **Aquarium** class để hỗ trợ các loại cấp nước khác nhau.

1. 

2.

```kotlin
class Aquarium<T>(val waterSupply: T)
```

3. 

```kotlin
fun genericsExample() {
    val aquarium = Aquarium<TapWater>(TapWater())
}
```

4.

```kotlin
fun genericsExample() {
    val aquarium = Aquarium<TapWater>(TapWater())
    aquarium.waterSupply.addChemicalCleaners()
}
```

5.


```kotlin
fun genericsExample() {
    val aquarium = Aquarium(TapWater())
    aquarium.waterSupply.addChemicalCleaners()
}
```

6.

```kotlin
fun genericsExample() {
    val aquarium = Aquarium<TapWater>(TapWater())
    println("water needs processing: ${aquarium.waterSupply.needsProcessing}")
    aquarium.waterSupply.addChemicalCleaners()
    println("water needs processing: ${aquarium.waterSupply.needsProcessing}")
}
```

7. 

```kotlin
fun main() {
    genericsExample()
}
```

```
⇒ water needs processing: true
water needs processing: false
```

## Step 3: Make it more specific (Làm cho nó cụ thể hơn)

1.

```kotlin
fun genericsExample() {
    val aquarium2 = Aquarium("string")
    println(aquarium2.waterSupply)
}
```

2. 

```
=> string
```

3. 

```kotlin
fun genericsExample() {
    val aquarium3 = Aquarium(null)
    if (aquarium3.waterSupply == null) {
        println("waterSupply is null")
    }
}
```

4.

```
=> waterSupply is null
```

Tại sao có thể truyền **null** -> vì **T** là viết tắt của type nullable **Any?**.

```kotlin
class Aquarium<T: Any?>(val waterSupply: T)
```

5.

```kotlin
class Aquarium<T: Any>(val waterSupply: T)
```

Trong trường hợp này, **Any** -> gọi là [generic constraint](generic-constraint) -> nghĩa là bất kỳ type nào đều có thể thông qua **T** miễn là nó không **null**.

6.

```kotlin
class Aquarium<T: WaterSupply>(val waterSupply: T)
```

## Step 4: Add more checking (Kiểm tra thêm)

Tìm hiểu thêm về [check](check) đảm bảo mã của bạn hoạt động như mong đợi. Nó là function từ thư việc chuẩn trong Kotlin. Nó sẽ ném ra **IllegalStateException** nếu đối số nó đánh giá là **false**.

1.

```kotlin
class Aquarium<T: WaterSupply>(val waterSupply: T) {
    fun addWater() {
        check(!waterSupply.needsProcessing) { "water supply needs processing first" }
        println("adding water from $waterSupply")
    }    
}
```

2.

```kotlin
fun genericsExample() {
    val aquarium4 = Aquarium(LakeWater())
    aquarium4.addWater()
}
```

3.

```
Exception in thread "main" java.lang.IllegalStateException: water supply needs processing first
	at generics.Aquarium.addWater(Aquarium.kt:19)
```

4.

```kotlin
fun genericsExample() {
    val aquarium4 = Aquarium(LakeWater())
    aquarium4.waterSupply.filter()
    aquarium4.addWater()
}
```

```
⇒ adding water from generics.LakeWater@880ec60
```

```diff
+Tip: 
Sử dụng check() function giúp đảm bảo mã của bạn hoạt động đúng như mong đợi.
```

[generic-constraint]:https://kotlinlang.org/docs/generics.html#generic-constraints
[check]:https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/check.html