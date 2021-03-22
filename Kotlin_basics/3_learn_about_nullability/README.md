# Learn about nullability (Tìm hiểu về tính vô hiệu)

Vì nulls gây ra rất nhiều bug -> Kotlin hạn chế nó bằng các biến non-nullable (không thể null)

## Step 1: Learn about nullability 

1. Khai báo viến kiểu **Int** và gán cho **null**

```
var rocks: Int = null
=> error: null can not be a value of a non-null type Int
```

2. **?** phía sau type biểu thị biến có thể **null**

```
var marbles: Int? = null
```

Khi có những kiểu data phức tạp hơn như **list**

* Cho phép các phần tử của list null
* Cho phép list null, nhưng nếu not null thì phần tử không thể là null
* Cho phép cả list và phần tử là null

## Step 2: Learn about the ? and ?: operators (Tìm hiểu về toán tử ? và ?:)

Có thể kiểu tra **null** với  toán tử **?** thay vì viết nhiều câu lệnh **if**/**else**

1. Sử dụng **if**/**else** để kiểm tra

```
var fishFoodTreats = 6
if (fishFoodTreats != null) {
   fishFoodTreats = fishFoodTreats.dec()
}
```

2. Sử dụng toán tử **?** 

```
var fishFoodTreats = 6
fishFoodTreats = fishFoodTreats?.dec()
```

3. Sử dụng toán tử **?:** -> xâu chuổi việc kiểm tra null

```
fishFoodTreats = fishFoodTreats?.dec ?: 0
```

* Nếu fishFoodTreats khác null -> giảm dần giá trị
* Nếu fishFoodTreats bằng null -> giá trị sẽ là 0


### A point about null  pointers (Một điểm về con trỏ null)

Nếu yêu **NullPointerExceptions** -> Sử dụng toán tử khẳng định not-null, !!(double-bang) 
=> Chuyển đổi bất kỳ giá trị nào không phải null và nếm ra exception nếu giá trị là **null**

```
val len = s!!.length // throws NullPointerException if s is null
```


