# Summary

Mặc dù có thể bạn đã quen về object-oriented (hướng đối tượng) trong các ngôn ngữ khác. Nhưng kotlin cung cấp một số tính năng để giữ cho mã của bạn ngắn gọn và dễ đọc.

## Classes and constructors (Các lớp và hàm khởi tạo)

* Khai báo một class trong Kotlin sử dụng **class**.<br/>
* Kotlin tự động tạo setters và getters cho properties.<br/>
* Khai báo hàm constructor trực tiếp trong định nghĩa lớp. Ví dụ:
```kotlin
class Aquarium(var length: Int = 100, var width: Int = 20, var height: Int = 40)
```
* Nếu hàm constructor cần mã bổ sung -> viết nó vào trong một hoặc nhiều **init** blocks.
* Một lớp có thể khai báo một hoặc nhiều hàm tạo thứ cấp sử dụng **constructor**, nhưng kiểu của Kotlin là sử dụng một factory function thay thế.

## Visibility modifiers and subclasses (Các công cụ sửa đổi mức độ hiển thị và các lớp con)

* Mặc định các class và function trong Kotlin và **public**. Bạn có thể thay đổi khả năng hiển thị với **interal**, **private**, **protected**
* Để tạo một subclass, lớp cha phải được đánh dấu **open**
* Để ghi đè methods và properties trong subclass, methods và properties phải dược đánh dấu **open** trong class cha
* Một lớp sealed có thể phân lớp duy nhất trong tệp nơi đó được khai báo. Tạo một lớp sealed bằng cách đặt tiền tố **sealed**.

## Data classes, singletons, and enums (Các lớp dữ liệu, singletons, enums)

* Tạo một data class bằng cách đặt tiền tố khai báo với data
* **Destructuring** -> cách viết tắt để gán các thuộc tính của 1 **data** object cho các biến riêng biệt
* Để tạo một **singleton** sử dụng **object** thay vì **class**.
* Khai báo một enum sử dụng **enum class**.

## Abstract classes, interfaces, and delegation (Các lớp trừu tượng, giao diện, ủy quyền)

* Abstract classes và interfaces -> là 2 cách để chia sẽ chung các hành vi giữa các lớp
* Một **abstract class** khai báo properties và behavior (hành vi), nhưng để lại việc implement cho subclasses.
* Một **interface** khai báo một behavior, và có thể cung cấp implement mặc định đối với một số hoặc tất cả hành vi.
* Khi sử sụng **interface** trong một class, chức năng của lớp được mở rộng theo instances mà nó chứa 
* Interface delegation sư dụng composition(thành phần), nhưng cũng ủy quyền việc triển khai cho các lớp giao diện.
* Composition là một cách mạnh mẽ để thêm chức năng vào một lớp bằng cách sử dụng interface delegation. <br/>
Composition được ưu tiên hơn, nhưng kết thừ từ abstract class phù hợp hơn cho một số vấn đề.