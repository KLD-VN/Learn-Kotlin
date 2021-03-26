# Learn about subclasses and inheritance (Tìm hiểu về lớp con và kế thừa)

Trong Kotlin, mặc định các class khong thể được subclassed (phân lớp). Tương tự properties và biến thành viên không thể bị ghi đề bởi các subclasses (mặc dùn chúng có thể được truy cập)

Đánh dấu một lớp là **open** để cho phép nó phân lớp. Tương tự với các thuộc tính và biến thành viên.
Từ khóa **open** cần thiết -> ngăn rò rỉ chi tiết thực hiện như một phần của giao diện lớp

## Step 1: Make the Aquarium class open (Thực hiện open class Aquarium)

1. Đánh đấu lớp **Aquarium** và tất cả thuộc tính của nó bằng từ khóa **open**.

```kotlin
open class Aquarium (open var length: Int = 100, open var width: Int = 20, open var height: Int = 40) {
    open var volume: Int
        get() = width * height * length / 1000
        set(value) {
            height = (value * 1000) / (width * length)
        }
}
```

## Step 2: Create a subclass (Tạo một class con)

1. Tạo một lớp con của **Aquarium** gọi là **TowerTank** -> bể hình trụ thay vì hình chữ nhật. Có thể thêm **TowerTank** dưới **Aquarium**, vì có thể thêm một lớp khác trong cùng một tệp với lớp **Aquarium**.

2. Trong **TowerTank**, ghi đè thuộc tính **height** được xác định trong hàm constructor -> sử dụng từ khóa **override** trong subclass

```diff
!Lưu ý:
Các lớp con phải khai báo các tham số phương thức khởi tạo một cách rõ ràng.
```

3. Trong hàm constructor **TowerTank** lấy một **diameter**. Sử dụng **diameter** cho cả **length** và **width** khi gọi ham constructor trong **Aquarium** lớp cha.

```kotlin
class TowerTank (override var height: Int, var diameter: Int) : Aquarium(height = height, width = diameter, length = diameter)
```

4. Ghi đè thuộc tính thể tích để tính hình trụ -> công thức: bình phương bán kính nhân chiều cao. Cần nhập hằng số **PI** từ **java.lang.Math**

```kotlin
override volume: Int
// ellipse area = π * r1 * r2
    get() = (width/2 * length/2 * height / 1000 * PI).toInt()
    set(value) {
        height = ((value * 1000 / PI) / (width/2 * length/2)).toInt()
    }
```
5. Trong **TowerTank**, ghi đề thuộc tính **water** thành 80% volume

```kotlin
override var water = volume * 0.8
```

6. Ghi đè cái **shape** thành **cylinder**

```kotlin
override val shape = "cylinder"
```
7. **TowerTank** sẽ như sau:

```kotlin
class TowerTank(override var height: Int, var diameter: Int) : Aquarium(height = height, width = diameter, length = diameter) {
    // ellipse are = π * r1 * r2
    override var volume: Int
        get() = (width/2 * length/2 * height / 1000 * PI).toInt()
    set(value) {
        height = ((value * 1000 / PI) / (width/2 * length/2)).toInt()
    }

    override var water = volume * 0.8
    override val shape = "cylinder"
}
```

8. Trong **buildAquarium()** -> tạo một **TowerTank** có đường kính 25cm và cao 45 cm.

```kotlin
package example.myapp

fun buildAquarium() {
    val myAquarium = Aquarium(width = 25, length = 25, height = 40)
    myAquarium.printSize()
    val myTower = TowerTank(diameter = 25, height = 40)
    myTower.printSize()
}
```

9. Chạy chương trình


```
=> aquarium initializing
rectangle
Width: 25 cm Length: 25 cm Height: 40 cm 
Volume: 25 l Water: 22.5 l (90.0% full)
aquarium initializing
cylinder
Width: 25 cm Length: 25 cm Height: 40 cm 
Volume: 18 l Water: 14.4 l (80.0% full)
```