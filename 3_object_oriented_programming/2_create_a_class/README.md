# Create a class (Tạo một lớp)

Tạo một package (gói) và một class với một số thuộc tính và một method.

## Step 1: Create a package (Tạo một gói)

**Packages** giúp bạn giữ code có tổ chức

1. Trong **Project**, dưới project **Hello Kotlin** , chuột phải vào thư mục **src**
2. Chọn **New > Package** và gọi nó **example.myapp**.

## Step 2: Create a class with properties (Tạo một lớp với các thuộc tính)

1. Chuột phải vào **example.myapp** package.
2. Chọn **New > Kotlin File/ Class**.
3. Trong **Kind**, chọn **Class** và đặt tên cho lớp là **Aquarium**.
4. Tong lớp **Aquarium**, xác định khởi tạo **var** các thuộc tính **width**, **height**, **length**.
 Khởi tạo properties (thuộc tính) với các giá trị mặc định

```kotlin
package example.myapp

class Aquarium {
   var width: Int = 20
   var height: Int = 40
   var length: Int = 100
}
```
Kotlin tự đọng tạo các **getters** và **setters** cho các thuộc tính xác định trong lớp **Aquarium** -> có thể truy cập trực tiếp các thuộc tính.

## Step 3: Create a main() function

Tạo một file mới gọi là **main.kt** để giữ hàm **main()**

1. Trong **Project**, click chuột phải vào **example.myapp** package

2. Chọn **New > Kotlin File / Class**

3. Trong **Kind**, chọn **File** và đặt tên file là **main.kt**.
IntelliJ IDEA bao gồm tên gói, nhưng không bao gồm định nghĩa lớp cho file.

4. Xác định một hàm **buildAquarium()** và bên trong tạo instance của **Aquarium** bằng cách tham chiếu lớp như thể nó là một function **Aquarium()**.
Việc này gọi hàm constructor (hàm tạo) của lớp và một instance của **Aquarium** tương tự như **new** trong các ngôn ngữ khác

5. Xác định hàm **main()** và gọi **buildAquarium()**.

```kotlin
package example.myapp

fun buildAquarium() {
   val myAquarium = Aquarium()
}

fun main() {
   buildAquarium()
}
```

## Step 4: Add a method (Thêm một phương thức)

1. Trong lớp **Aquarium**, thêm một phương thức để in properties kích thước của bể cá.

```kotlin
fun printSize() {
   println( "Width: $width cm " +
            "Length: $length cm" +
            "Height: $height cm")
}
```

2. Trong **main.kt**, trong **buildAquarium()**, gọi **printSize()** phương thức trên **myAquarium**.

```kotlin
fun buildAquarium() {
   val myAquarium = Aquarium()
   myAquarium.printSize()
}
```

3. Chạy chương trình -> click button tam giác xanh lá cây cạnh hàm **main()**.

```
=> Width: 20 cm Length: 100 cm Height: 40 cm 
```

4. Trong **buildAquarium()**, thêm mã để đặt **height** thành 60

```kotlin
fun buildAquarium() {
    val myAquarium = Aquarium()
    myAquarium.printSize()
    myAquarium.height = 60
    myAquarium.printSize()
}
```

5. Chạy chương trình

```
=> Width: 20 cm Length: 100 cm Height: 40 cm 
Width: 20 cm Length: 100 cm Height: 60 cm
```

