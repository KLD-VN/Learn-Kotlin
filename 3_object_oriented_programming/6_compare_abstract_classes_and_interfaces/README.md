# Compare abstract classes and interfaces (So sánh các lớp và giao diện trừu tượng)

Để xác định hành vi hoặc thuộc tính chung để được chia sẻ giữa một số lớp liên quan. Kotlin cung cấp 2 cách để làm -> abstract và interfaces. </br>
Tạo một lớp trừu tượng **AquariumFish** cho các thuộc tính chung cho tất cả các loài cá.<br/>
Tạo một interfaces gọi là **FishAction** để xác định hành vi chung cho tất cả các loài cá.

* Cả một abstract hay một interface đều không thể được khởi tạo riêng -> nghĩa là không thể tạo đối tượng thuộc các kiểu đó một cách trực tiếp.

* Abstract classes có các hàm constructor.

* Interfaces không thể có bất kỳ logic phương thức constructor nào hoặc lưu trữ bất kỳ trạng thái nào.

```diff
!Lưu ý:
Các lớp trừ tượng luôn mở -> không cần đánh dấu bằng **open**.
Các thuộc tính và phương thức của một abstract class là non-abstract trừ khi đánh dấu chúng rõ ràng bằng từ khóa abstract.
Các lớp con có thể sử dụng sử dụng các lớp trừu tượng như đã cho.
Nếu các thuộc tình hoặc phương thức là abstract, subclasses phải triển khai chúng
```

# Step 1. Create an abstract class (Tạo một lớp trừu tượng)

1. Trong package **example.myapp", tạo file mới **AquariumFish.kt**
2. Tạo một class -> tên là **AquariumFish** -> đánh dấu nó là **abstract**
3. Thêm một thuộc tính **String**, **color** -> đánh dấu nó là **abstract**

```kotlin
package example.myapp

abstract class AquariumFish {
    abstract val color: String
}
```

4. Tạo 2 subclasses thuộc **AquariumFish**, **Shark** và **Plecostomus**
5. Vì **color** là abstract, subclasses cần phải triển khai chúng. Tạo **Shark** màu xám và **Plecostomus** màu vàng

```kotlin
class Shark: AquariumFish() {
    override val color = "gray"
}

class Plecostomus: AquariumFish() {
    override val color = "gold"
}
```

6. Trong **main.kt**, Tạo một function **makeFish()** để kiểm tra classes của bạn.
 Khởi tạo một **Shark** và một **Plecostomus**, in ra màu của mỗi loại.

7. Xóa code trước đó trong function **main()** và gọi function **makeFish()**. 

```kotlin
package example.myapp

fun makeFish() {
    val shark = Shark()
    val pleco = Plecostomus()

    println("Shark: ${shark.color}")
    println("Plecostomus: ${pleco.color}")
}

fun main () {
    makeFish()
}
```

8. Chạy chương trình

```
=> Shark: gray
Plecostomus: gold
```

Sơ đồ sau đại diện cho -> **Shark** class và **Plecostomus** class -> subclass của abstract class **AquariumFish**

<p align="center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/3_object_oriented_programming/Gallery/4/one_abstract_class_two_subclasses.png" />
</p>

## Step 2. Create an interface (Tạo một giao diện)

1. Trong **AquariumFish.kt** -> tạo một interface **FishAction** và method **eat()**

```kotlin
interface FishAction {
   fun eat()
}
```

2. Thêm **FishAction** vào mỗi subclasses và implement **eat()** bằng cách in ra những hành động của con cá.

```kotlin
class Shark: AquariumFish(), FishAction {
   override color = "gray"
   override fun eat() {
      println("hunt and eat fish")
   }
}
class Plecostumus: AquariumFish(), FishAction {
   override color = "gold"
   override fun eat() {
      println("eat algae")
   }
}
```

3. Trong function **makeFish()** với mỗi loài cá -> gọi function **eat()**.

```kotlin
fun makeFish() {
    val shark = Shark()
    val pleco = Plecostomus()

    println("Shark: ${shark.color}")
    shark.eat()
    println("Plecostomus: ${pleco.color}")
    pleco.eat()
}
```

4. Chạy chương trình và xem kết quả

```
=> Shark: gray
hunt and eat fish
Plecostomus: gold
eat algae
```

Biểu đồ sau đại diện cho 2 classes **Shark** và **Plecostomus** -> cả 2 được cấu tạo và implement **FishAction** interface.

<p align="center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/3_object_oriented_programming/Gallery/4/two_classes_one_interfaces.png" />
</p>

## When to use abstract classes versus interfaces (Khi nào sử dụng lớp trừu tượng so với giao diện)

Khi có nhiều classes tương quan với nhau -> sử dụng abstract classes và interface -> giữ thiết kế gọn gàng, có tổ chức hơn
và dễ bảo trì hơn. Các abstract class có thể có các hàm constructor còn interface thì không -> nhưng nếu không có constructor function thì chúng rất giống nhau

* Sử dụng interface nếu có nhiều phương thức hoặc một 2 implement mặc định

```kotlin
interface AquariumAction {
    fun eat()
    fun jump()
    fun clean()
    fun catchFish()
    fun swim() {
        println("swim")
    }
}
```

* Sử dụng abstract class khi không thể hoàn thành một class. Ví dụ: lớp **AquariumFish** -> implement tất cả từ **FishAction** và cung cấp implement default **eat** 
trong khi để lại **color** abstract vì không có màu cố định cho cá.

```kotlin
interface FishAction  {
    fun eat()
}

abstract class AquariumFish: FishAction {
   abstract val color: String
   override fun eat() = println("yum")
}
```