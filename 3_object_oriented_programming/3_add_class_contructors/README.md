# Add class constructors (Thêm lớp khởi tạo)

Tạo một phương thức constructor cho lớp và tiếp tục làm việc với các thuộc tính

## Step 1: Create a constructor

Hàm **constructor** trong Kotlin được xác định trong chính khai báo class, chỉ định tham số như phương thức, và cũng có thể có thiết lập giá trị mặc định cho các tham số.

```kotlin
class Aquarium(length: Int = 100, width: Int = 20, height: Int = 40) {
   // Dimensions in cm
   var length: Int = length
   var width: Int = width
   var height: Int = height
...
}
```

2. Cách viết ngắn gọn hơn -> xác định các thuộc tính trong hàm **constructor**, sử dụng **var** hoặc **val**, kotlin cũng tự động tạo các **getters**, **setters**.

```kotlin
class Aquarium(var length: Int = 100, var width: Int = 20, var height: Int = 40) {
...
}
```

3. Khi tạo một object **Aquarium** với hàm **constructor**, có thể chỉ định không có đối số, một đối số hoặc nhiều hơn. 

```kotlin
fun buildAquarium() {
    val myAquarium = Aquarium()
    myAquarium.printSize()
    // default height and length
    val aquarium2 = Aquarium(width = 25)
    aquarium2.printSize()
    // default width
    val aquarium3 = Aquarium(height = 35, length = 110)
    aquarium3.printSize()
    // everything custom
    val aquarium4 = Aquarium(width = 25, height = 35, length = 110)
    aquarium4.printSize()
}
```

4. Chạy chương trình

```
=> Width: 20 cm Length: 100 cm Height: 40 cm 
Width: 25 cm Length: 100 cm Height: 40 cm 
Width: 20 cm Length: 110 cm Height: 35 cm 
Width: 25 cm Length: 110 cm Height: 35 cm 
```

```diff
!Lưu ý:
Không cần phải tạo nhiều phiên bản hàm constructor khác nhau cho từng trường hợp. Kotlin tạo ra những gì cần thiết từ các giá trị mặc định và các tham số được đặt tên.
```


## Step 2: Add init blocks (Thêm khối init)

Nếu cần thêm mã khởi tạo cho hàm **constructor**, có thể đặt nó trong khối **init**

1. Trong lớp **Aquarium**, thêm một khối **init** để in đối tượng đang khởi tạo và khối 2 là in thể tích bằng lít.

```kotlin
class Aquarium (var length: Int = 100, var width: Int = 20, var height: Int = 40) {
    init {
        println("aquarium initializing")
    }
    init {
        // 1 liter = 1000 cm^3
        println("Volume: ${width * length * height / 1000} l")
    }
}
```

2. Chạy chương trình

```
aquarium initializing
Volume: 80 L
Width: 20 cm Length: 100 cm Height: 40 cm 
aquarium initializing
Volume: 100 L
Width: 25 cm Length: 100 cm Height: 40 cm 
aquarium initializing
Volume: 77 L
Width: 20 cm Length: 110 cm Height: 35 cm 
aquarium initializing
Volume: 96 L
Width: 25 cm Length: 110 cm Height: 35 cm 
```

* Các khối **init** thực tự theo thứ tự xuất hiện trong định nghĩa class và đều được thực thi khi hàm constructor được gọi.

```diff
!Lưu ý
Tham số của hàm constructor có thể sử dụng trong các khối init. Bất kỳ thuộc tính nào được sử dụng trong các khối init phải được khai báo trước đó
```

## Step 3: Learn about secondary constructors (Tìm hiểu về các hàm tạo phụ)

Ngoài phương thức khởi tạo chính, có thể có một hoặc nhiều khối **init**. Kotlin cũng có thể có một hoặc nhiều phương thức khởi tạo phụ -> để cho phép nạp chồng phương thức khởi tạo, tức là các hàm tạo có đối số khác nhau.

```diff
!Lưu ý:
Chỉ nên có một hàm tạo sử dụng các giá trị mặc định và các tham số được đặt tên.
Mọi hàm tạo thứ cấp phải gọi constructor chính trước, hoặc sử dụng trực tiếp this() hoặc gián tiếp bằng cách gọi một hàm tạo thứ cấp khác.
Có nghĩa là bất kỳ khối **init** nào trong khối main sẽ được gọi cho tất cả các constructor và tất cả mã trong constructor chính sẽ được thực thi đầu tiên.
```

1. Trong lớp **Aquarium**, thêm constructor thứ cấp -> số lượng cá là đối số. tạo **val** thuộc tính bể

2. Trong hàm constructor thứ cấp, giữ nguyên chiều dài và chiều rộng, tính toán chiều cao cầnt thiết để bể có thể tích nhất định.

```kotlin
 constructor(numberOfFish: Int) : this() {
        // 2,000 cm^3 per fish + extra room so water doesn't spill
        val tank = numberOfFish * 2000 * 1.1
        // calculate the height needed
        height = (tank / (length*width)).toInt()
    }
```

3. Trong hàm **buildAquarium()**, thêm lệnh gọi tạo một constructor **Aquarium** phụ mới.

```kotlin
fun buildAquarium() {
val aquarium5 = Aquarium(numberOfFish = 29)
    aquarium5.printSize()
    println("Volume: ${aquarium5.width * aquarium5.length * aquarium5.height / 1000} l")
}
```

4. Chạy chương trình

```
=> Volume: 80 L
Width: 20 cm Length: 100 cm Height: 31 cm 
Volume: 62 L
```

**Volume** được in 2 lần -> lần 1 bởi khối **init** (trước phương thức constructor phụ), lần 2 là từ mã trong **buildAquarium()**.

* Có thể đưa **constructor** từ khóa vào hàm tạo -> không cần thiết trong hầu hết các trường hợp

## Step 4: Add a new property getter (Thêm một người nhận tài sản mới)

Thêm một thuộc tính **getter** rõ ràng -> khi giá trị của thuộc tính cần được điều chỉnh hoặc tính toán. 

1. Trong lớp **Aquarium**, xác định một properties **Int** được gọi **volume** và xác định một phương thức **get()** tính toán khối lượng

```kotlin
val volume: Int 
      get() = width * height * length / 1000 // 1000 cm^3 = 1 l
```

2. Loại bỏ **init** khối in volume
3. Loại bỏ mã in volume trong **buildAquarium()**
4. Trong phương thức **printSize()** , thêm một dòng để in volume

```kotlin
fun printSize() {
    println("Width: $width cm " +
            "Length: $length cm " +
            "Height: $height cm "
    )
    // 1 l = 1000 cm^3
    println("Volume: $volume l")
}
```

5. Chạy chương trình

```
=> aquarium initializing
Width: 20 cm Length: 100 cm Height: 31 cm 
Volume: 62 l
```

Kích thước và khối lượng giống trước, nhưng khối lượng chỉ được in một lần sau khi đói tượng được khởi tạo hoàn toàn bởi -> constructor chính và phụ.

## Step 5: Add a property setter (Thêm một thuộc tính thiết lập )

1. Trong lớp **Aquarium**, đổi **volume** thành một **var** để nó có thể được đặt nhiều lần.

1. Thêm một phương thức **set()** bên dưới getter, tính toán lại chiều cao dựa trên lượng nước được cung cấp. Theo quy ước đặt tên tham số của setter là **value**.

```kotlin
var volume: Int
        get() = width * height * length / 1000
        set(value) {
            height = (value * 1000) / (width * length)
        }
```

3. Trong **buildAquarium()**, thêm mã đặt thể tích bể cá thành 70 lít.

```
=> aquarium initializing
   Width: 20 cm Length: 100 cm Height: 34 cm 
   Volume: 68 l
   Width: 20 cm Length: 100 cm Height: 35 cm 
   Volume: 70 l
```