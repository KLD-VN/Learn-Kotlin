# Learn about visibility modifiers (Tìm hiểu về công cụ sửa đổi khả năng hiển thị)

Trong **Kotlin** -> **classes**,**objects**, **constructor**, **function**, **properties**, **setter** chúng có thể có -> **Visibility modifiers** (thay đổi khả năng hiển thị):

* **public** -> có thể nhìn thấy bên ngoài lớp. Tất cả đều công khai, bao gồm các biến và methods

* **internal** -> chỉ hiển thị trong module -> tập các tệp Kotlin được biên dịch lại với nhau, là thư viện hoặc ứng dụng.

* **private** -> chỉ hiển thị trong class đó (hoặc trong source file nếu đang làm việc với function)

* **protected** giống **private**, nhưng nó hiển thị với các lớp con
```
Ví dụ:
-> Một mô-đun IntelliJ IDEA
-> Một Maven project
```

## Member variables (Biến thành viên)

Mặc định các biến sẽ là **public**. Nếu muốn property có thể đọc hoặc ghi nhưng mã bên ngoài chỉ có thể đọc -> khai báo getter hoặc setter là **private**.

```kotlin
var volume: Int
   get() = width * height * length / 1000 // 1000 cm^3 = 1 l
   private set(value) {
      height = (value * 1000) / (width * length)
   }
```