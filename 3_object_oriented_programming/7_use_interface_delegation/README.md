# Use interface delegation (Sử dụng ủy quyền giao diện)

**Interface delegation** -> kỹ thuật nâng cao -> các phương thức của một interface được thực hiện bởi một helper (or delegate) object. Object này sau đó được sử dụng bởi một class. Technique hữu ích khi sử dụng một interface trong một loạt các class không liên quan: thêm chức năng interface cần thiết vào một class helper riêng biệt và mỗi class sử dụng một instance của class helper để triển khai chức năng

## Step 1: Make a new interface (Tạo một giao diện mới)

1. Trong **AquariumFish.kt**, xóa lớp **AquariumFish**. Thay vì kết thừa **Aquarium** -> **Plecostomus**, **Shark** sẽ implement interfaces cho cả hành động và màu sắc của chúng.

2. Tạo mới một interface, **FishColor** -> định nghĩa color dưới dạng một string.

```kotlin
interface FishColor {
    val color: String
}
```

3. Thay đổi **Plecostomus** để implement 2 interface, **FishAction**, **FishColor**. Bạn cần override **color** từ **FishColor** và **eat()** từ **FishAction**.

```kotlin
class Plecostomus: FishAction, FishColor {
    override val color = "gold"
    override fun eat() {
        println("eat algae")
    }
}
```

4. Thay đổi **Shark** class -> cũng implement 2 interface **FishAction**, **FishColor**. Thay vì inheriting từ **AquariumFish**.

```kotlin
class Shark: FishAction, FishColor {
    override val color = "gray"
    override fun eat() {
        println("hunt and eat fish")
    }
}
```

5. Cuối cùng code của bạn sẽ như thế này


```kotlin
package example.myapp

interface FishAction {
   fun eat()
}

interface FishColor {
   val color: String
}

class Plecostomus: FishAction, FishColor {
   override: val color = "gold"
   override fun eat() {
      println("eat algae")
   }
}

class Shark: FishAction, FishColor {
   override val color = "gray"
   override fun eat() {
      println("hunt and eat fish")
   }
}
```

## Step 2: Make a singleton class (Tạo một lớp singleton)

Triển khai thiết lập cho phần delegation bằng cách tạo một helper class để implement **FishColor**. 
Tạo một class cơ bản **GoldColor** implement **FishColor** -> tất cả việc của nó là nói color là gold<br/><br/>

Sẽ không hợp lý khi tạo ra nhiều trường hợp **GoldColor** -> vì tất cả chúng giống hệt nhau. Kotlin cho phép khai báo class -> chỉ có thể tạo 1 instance của nó -> sử dụng từ khóa **object** thay vì class. Kotlin tạo một instance và nó được tham chiếu bởi tên class. Tất cả  object khac chỉ có thể sử dụng 1 instance này - không có cách khác để tạo các instance của class này. 

1. Trong **AquariumFish.kt** -> tạo một object cho **GoldColor**.

```kotlin
object GoldColor : FishColor {
   override val color = "gold"
}
```

## Step 3: Add interface delegation for FishColor (Thêm ủy quyền giao diện cho FishCooor)

1. Trong **AquariumFish.kt**, xóa override **color** khỏi **Plecostomus**
2. Thay đổi **Plecostomus** để lấy màu **GoldColor** -> thêm **by GoldColor** vào khai báo class, tạo delegation. Việc này nói rằng -> thay vì implementing **FishColor** thì hãy implementation được cung cấp bởi **GoldColor**. Vì vậy, mỗi khi **color** được truy cập, nó được ủy quyền cho **GoldColor**.

```kotlin
class Plecostomus: FishAction, FishColor by GoldColor {
    override fun eat() {
        println("eat algae")
    }
}
```

Với class như thế, tất cả **Plecostomus** sẽ có màu vàng, nhưng chúng có thể có nhiều màu sắc. Có thể giải quyết việc này bằng cách thêm một tham số constructor cho color với **GoldColor** là màu mặc định cho **Plecostomus**.

3. Thay đổi **Plecostomus** class -> nhận một **fishColor** với constructor function của nó và mặc định là **GoldColor**. Thay đổi delegation từ **by GoldColor** thành **by fishColor**

```kotlin
class Plecostomus(fishColor: Fishcolor = GoldColor): FishAction, FishColor by fishColor {
   override fun eat() {
      println("eat algea")
   }
}
```

## Step 4: Add interface delegation for FishAction (Thêm ủy quyền giao diện cho FishAction)

1. Trong **AquariumFish.kt** -> tạo **PrintingFishAction** class implement **FishAction**, trong đó có một **String**, **food** in những gì là thức ăn cho cá 

```kotlin
class PrintingFishAction(val food: String) : FishAction {
   override fun eat() {
      println(food)
   }
}
```

2. Trong **Plecostomus** class -> xóa override function **eat()**, vì bạn sẽ thay thế nó bằng một **delegation**

3. Trong khai báo của **Plecostomus**, delegate **FishAction** cho **PrintingFishAction**, đi qua **"eat algae"**

4. Với tất cả delegation đó -> không có code trong phần thân của **Plecostomus** class => hãy xóa **{}**, vì tất cả các override được xử lý bởi interface delegation

```kotlin
class Plecostomus(fishColor: FishColor = GoldColor):
    FishAction by PrintingFishAction("eat algae"),
    FishColor by fishColor
```

Sơ đồ đại diện cho **Shark** và **Plecostomus** class, cả 2 đều bao gồm **PrintingFishAction** và **FishColor**, nhưng delegation được triển khai cho chúng.

<p style="text-align:center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/3_object_oriented_programming/Gallery/4/two_classes_two_interfaces_with_delegation.png" />
</p>

![two_classes_two_interfaces_with_delegation](https://github.com/KLD-VN/Learn-Kotlin/blob/main/3_object_oriented_programming/Gallery/4/two_classes_two_interfaces_with_delegation.png?style=centerme)

img[src$="centerme"] {
  display:block;
  margin: 0 auto;
}

Interface delegation rất mạnh -> nên xem xét cách sử dụng nó bất cứ khi nao sử dụng một abstract class. Cho phép sử dụng các thành phần để bổ sung các hành vi, thay vì yêu cầu nhiêu subclasses, mỗi lớp chuyên biệt theo một cách khác nhau.