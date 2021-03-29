# Study constants (Nghiên cứu hằng số)

Tìm hiểu về constants trong Kotlin và các cách tổ chức chúng.

## Step 1: Learn about const vs. val (Tìm hiểu về const so với val)

1. Trong REPL, thử tạo một hằng số -> có thể tạo các hằng số cấp cao nhất và gán cho chúng một giá trị tại thời điểm biên dịch -> sử dungj **const val**.

```kotlin
const val rocks = 3
```

Giá trị được gán và không thể thay đổi, nghe giống **val**. Khác biệt giữa **const val** và **val** -> **const val**  được xác định tại thời điểm biên dịch còn **val** được xác định trong quá trình thực thi chương trình, nghĩa là **val** có thể được gán bởi một hàm tại thời điểm chạy.<br/><br/>

=> **val** có thể gán giá trị từ một hàm, nhưng **const val** thì không.

```kotlin
val value1 = complexFunctionCall() // OK
const val CONSTANT1 = complexFunctionCall() // NOT ok
```

Ngoài ra **const val** chỉ hoạt động ở cấp cao nhất và trong các class singleton được khai báo với **object**, không hoạt động với các lớp thông thường. Có thể dùng điều này để tạo tệp hoặc object singleton chỉ chứa các hằng số và import chúng khi cần 

```kotlin
object Constants {
   const val CONSTANT2 = "object constant"
}
val foo = Constants.CONSTANT2
```

## Step 2: Create a companion object (Tạo một đối tượng độc hành)

Để xác định các constant trong một class -> cần bọc chúng thàn các companion object được khai báo với từ khóa **companion** -> về cơ bản nó là một singleton object trong class.

1. Tạo một lớp với một companion object chứa một hằng số chuỗi.

```kotlin
class MyClass {
   companion object {
      const val CONSTANT3 = "constant in companion"
   }
}
```

Sự khác biệt cơ bản giữa companion object và object thông thường là:

* Companion object được khởi tạo từ phương thức khởi tạo tĩnh của lớp chứa -> chúng được tạo khi đối tượng được tạo.
* Objects thông thường được khởi tạo lười biếng trong lần truy cập đầu tiên vào đối tượng đó; nghĩa là chúng được sử dụng lần đầu tiên.
