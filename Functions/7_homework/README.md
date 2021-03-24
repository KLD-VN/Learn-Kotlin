# HOMEWORK

## Answer these questions

### Câu hỏi 1

Các **contains(element: String)** trả về **true** nếu chuỗi **element** được chứa trong chuỗi nó được gọi. Đầu ra của đoạn mã sau đây sẽ là gì?

**val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")**

**println(decorations.filter {it.contains('p')})**

▢ **[pagoda, plastic, plant]**

▢ **[pagoda, plastic plant]**

▢ **[pagoda, plastic plant, flowerpot]**

▢ **[rock, alligator]**

### Câu hỏi 2

Trong định nghĩa hàm sau, tham số nào là bắt buộc? **fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20, numDecorations: Int = 0): Boolean {...}**

▢ **numDecorations**

▢ **dirty**

▢ **day**

▢ **temperature**

### Câu hỏi 3

Bạn có thể chuyển một hàm dược đặt tên thông thường (không phải là kết quả của việc gọi nó) cho một hàm khác. Làm thế nào bạn sẽ vượt qua **increaseDirty( start: Int ) = start + 1để updateDirty(dirty: Int, operation: (Int) -> Int)**?

▢ **updateDirty(15, &increaseDirty())**

▢ **updateDirty(15, increaseDirty())**

▢ **updateDirty(15, ("increaseDirty()"))**

▢ **updateDirty(15, ::increaseDirty)**