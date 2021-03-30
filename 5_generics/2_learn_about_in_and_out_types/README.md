# Learn about in and out types (Tìm hiểu về kiểu in out)

## Step 1: Define an out type (Khai báo một loại type)

1.

```kotlin
class Aquarium<out T: WaterSupply>(val waterSupply: T) {
    ...
}
```

2,

```kotlin
fun addItemTo(aquarium: Aquarium<WaterSupply>) = println("item added")
```

3. 

```kotlin
fun genericsExample() {
    val aquarium = Aquarium(TapWater())
    addItemTo(aquarium)
}
```

4.


<p align="center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/5_generics/Gallery/2/generic_example.png" />
</p>

## Step 2: Define an in type (Xác định kiểu in)

1. 

```kotlin
interface Cleaner<in T: WaterSupply> {
    fun clean(waterSupply: T)
}
```

2. 

```kotlin
class TapWaterCleaner : Cleaner<TapWater> {
    override fun clean(waterSupply: TapWater) = waterSupply.addChemicalCleaners()
}
```

3. 

```kotlin
class Aquarium<out T: WaterSupply>(val waterSupply: T) {
    fun addWater(cleaner: Cleaner<T>) {
        if (waterSupply.needsProcessing) {
            cleaner.clean(waterSupply)
        }
        println("water added")
    }
}
```

4. 

```kotlin
fun genericsExample() {
    val cleaner = TapWaterCleaner()
    val aquarium = Aquarium(TapWater())
    aquarium.addWater(cleaner)
}
```

<p align="center">
   <img src="https://github.com/KLD-VN/Learn-Kotlin/blob/main/5_generics/Gallery/2/in.png" />
</p>