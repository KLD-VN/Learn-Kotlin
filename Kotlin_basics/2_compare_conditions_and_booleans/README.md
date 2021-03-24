# Compare conditions and booleans (So sánh điều kiện và boolean)

1. **if**/**else** statement

```kotlin
val numberOfFish = 50
val numberOfPlants = 23
if (numberOfFish > numberOfPlants) {
    println("Good ratio!") 
} else {
    println("Unhealthy ratio")
}

=> "Good ratio!"
```

2. Range in an **if** statement (Phạm vi trong câu lệnh if)

```kotlin
val fish = 50
if (fish in 1..100) {
    println(fish)
}

=> 50
```

3. **if** multiple cases -> **&&**, **||**, **else if**

```kotlin
if (numberOfFish == 0) {
    println("Empty tank")
} else if (numberOfFish < 40) {
    println("Got fish!")
} else {
    println("That's a lot of fish!")
}

=> "That's a lot of fish!"
```

4. **when** statement -> Cách tốt hơn thay thế cho chuỗi câu lệnh **if**/**else if**/**else** và nó giống switch trong các ngôn ngữ khác.

```kotlin
when (numberOfFish) {
    0 -> println("Empty tank")
    in 1..39 -> println("Got fish!")
    else -> println("That's a lot of fish!")
}

=> "That's a lot of fish!"
```



