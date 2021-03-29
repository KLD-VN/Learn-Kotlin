# Summary

* Pairs và triples có thể được sử dụng để trả về nhiều giá trị từ một hàm. Ví dụ: **val twoLists = fish.partition { isFreshWater(it) }**

* Kotlin có nhiều chức năng hữu ích cho **List**, chẳng hạn như **reversed()**, **constants()**, và **subList()**

* Một **HashMap** có thể được sử dụng để ánh xạ các khóa thành các giá trị. Ví dụ: **val cures = hashMapOf("white spots" to "Ich", "red sores" to "hole disease")

* Khai báo compile-time (thời gian biên dịch) hằng số -> **const**. Có thể đặt chúng ở cấp cao nhất, sắp sếp chúng trong một singleton object hoặc đặt trong một companion object.

* Một companion object là một singleton object trong định nghĩa lớp -> định nghĩa bằng từ khóa **companion**

* Các function và property extend có thể thêm function vào một class. Ví dụ: **fun String.hasSpaces() = find { it == ' ' } != null

* Nullable receiver cho phép bạn tạo phần mở rộng trên một class có thể được **null**. Các toán tử **?.** có thể kết hợp với **apply** để kiểm tra **null** trước khi thực hiện mã. Ví dụ: **this?.apply { prrintln("removing $this) }**