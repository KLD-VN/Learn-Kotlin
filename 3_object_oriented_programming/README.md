# Terminology (Thuật ngữ)

* **Classes** là blueprint (bản thiết kế) cho **objects** -> sủ dụng để tạo và quản lý các đối tượng mới và hỗ trợ **inheritance** (kế thừa)

![class-and-object](https://github.com/KLD-VN/Learn-Kotlin/blob/main/3_object_oriented_programming/Gallery/1/class_and_object.png)

* **Object** là instances (thể hiện, các trường hợp của lớp) của **classes**

* **instance** là một một đối tượng cụ thể được tạo ra từ một lớp cụ thể.

* **Properties** là đặc điểm của lớp như -> chiều dài, chiều cao, cân nặng của người

* **Methods** còn gọi là  **member functions** -> là chức năng của lớp. Là nhưng gì có thể **làm** với object. Ví dụ **fillWithWater()**(đổ đầy nước) trong đối tượng **Aquarium** (Bể cá)

* **Interface** là specification (đặc điểm kỹ thật -> mô tả chi tiết về cách một cái gì đó nên, được thiết kế hay chế tạo như thế nào) mà một lớp có thể thực hiện.

```
Ví dụ : Tạo interface gọi là Clean định nghĩa một phương thức clean(). Áp dụng cho 2 lớp "Aquarium"" và "Car" để làm sạc bằng một chiếc khăn.
```

* **Packages** nhóm các mã liên quan -> giữ cho nó có tổ chức hoặc tạo một thư viện mã. Có thể import nội dung của **package** vào một file khác và sử dụng lại code và classes trong đó
