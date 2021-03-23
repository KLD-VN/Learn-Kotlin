# Explore the main() function

```js
fun printHello() {
   println("Hello World")
}

printHello()

// => Hello World
```
Khai báo function -> **fun** keyword + tên của function + **()** chứa arguments (các tham số) + **{}** chứa code bên trong. Không có kiểu tra về cho hàm này vì nó không trả về bất cứ thứ gì.

## Step 1: Create a Kotlin file (Tạo một file kotlin)

1. Mở IntelliJ IDEA
2. Chọn **New Project**
![step_1_1](https://github.com/KLD-VN/Learn-Kotlin/blob/main/Functions/Gallery/1/step_1_1.png)

3. Đặt tên cho project -> **Functions**
![step_1_2](https://github.com/KLD-VN/Learn-Kotlin/blob/main/Functions/Gallery/1/step_1_2.png)

3. Tìm thư mục **kotlin** -> chuột phải chọn **New > Kotlin File / Class** -> tên file **Hello**
![step_1_3](https://github.com/KLD-VN/Learn-Kotlin/blob/main/Functions/Gallery/1/step_1_3.png)

## Step 2: Add code and run your program (Thêm code và chạy chương trình)

**main()** chỉ định để điểm nhập thực thi. Bất kỳ arguments nào được truyền dưới dạng một mảng chuỗi

* Nhập hoặc dán đoạn code sau vào trong file **Hello.kt**
```js
fun main(args: Array<String>) {
   println("Hello, world!")
}
```
2. Click vào button tam giác màu xanh lá cây để chạy -> chọn **Run 'HelloKt'**

3. IntelliJ IDEA biên dịch chương trình và chạy nó. Kết quả sẽ được hiển thị bên dưới cùng của IDEA

![step_1_4](https://github.com/KLD-VN/Learn-Kotlin/blob/main/Functions/Gallery/1/step_1_4.png)

## Step 3: Pass arguments to main() (Truyền tham số cho hàm main())

1. Chọn **Run > Edit Configurations** -> Hiện lên cửa sổ **Run/Debug Configurations**
2. Gõ **Kotlin!** trong trường **Program arguments**
3. Click **OK**

![step_3_1](https://github.com/KLD-VN/Learn-Kotlin/blob/main/Functions/Gallery/1/step_3_1.png)

## Step 4: Change the code to use a string template

Một [string template](string-template) chèn một biến hoặc biểu thức thành một chuỗi bằng cách sử dụng **$** + **{}** đóng khung biểu thức nếu có

1. Thay đổi thông báo chào mừng -> **args[0]** thay vì **world**

```js
fun main(args: Array<String>) {
   println("Hello, ${args[0]}")
}

// => Hello, Kotlin!
```





[string-template]: https://kotlinlang.org/docs/basic-types.html#string-templates











