# Summary

* Tạo tệp nguồn Kotlin trong IntelliJ IDEA

* Để biên dịch và chạy chương trình trong IntelliJ IDEA -> click vào tam giác xanh lá cây cạnh function **main()**. Đầu ra xuất hiện trong cửa sổ nhật ký bên dưới

* Trong IntelliJ IDEA, chỉ định đối số đối số dòng lệnh để chuyển đến function **main()** -> **Run > Edit Configurations**

* Hầu hết mọi thứ trong Kotlin đều có giá trị. Có thể làm mã ngắn hơn bằng cách sử dụng giá trị của một **if** hoặc **when** dưới dạng một biểu thức hoặc giá trị trả về.

* Các đối số mặc định loại bỏ nhu cầu về nhiều phiên bản của một hàm hoặc phương thức. Ví dụ: **fun swim(speed: String = "fast") {...}**

* Compact function (hàm nhỏ gọn), hoặc hàm single-expression (một biểu thức), làm mã dễ đọc hơn. Ví dụ: **fun isTooHot(temperature: Int) = temperature > 30**

* Kiến thức về filter, lambda. Ví dụ: **val beginsWithP = decorations.filter { it[0] == 'p' }**

* Lambda expression (biểu thức lambda) là biểu thức làm cho một function anonymous (chức năng ẩn danh). Biểu thức lambda xác định giữa các dấu ngoặc nhọn **{}**

* Trong **higher-order function**, chuyển một hàm chẳng hạn một biểu thức lambda cho một hàm khác dưới dạng dữ liệu. Ví dụ: **dirtyLevel = updateDirty(dirtyLevel) { dirtyLevel -> dirtyLevel + 23 }**