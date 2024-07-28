

“interface List<out E> : Collection<E>”


“fun List<String>.toBulletedList(): String {
  val separator = "\n - "
  return this.map { "$it" }.joinToString(separator, prefix = separator, postfix = "\n")
}”


“Creating your own generic constraints”

```
“// 1
class Mover<T>(
    // 2
    thingsToMove: List<T>,
    val truckHeightInInches: Int = (12 * 12)
) {

  // 3
  private var thingsLeftInOldPlace = mutableListOf<T>()
  private var thingsInTruck = mutableListOf<T>()
  private var thingsInNewPlace = mutableListOf<T>()

  // 4
  init {
    thingsLeftInOldPlace.addAll(thingsToMove)
  }

  // 5
  fun moveEverythingToTruck() {
    while (thingsLeftInOldPlace.count() > 0) {
      val item = thingsLeftInOldPlace.removeAt(0)
      thingsInTruck.add(item)
      println("Moved your $item to the truck!")
    }
  }

  // 6
  fun moveEverythingIntoNewPlace() {
    while (thingsInTruck.count() > 0) {
      val item = thingsInTruck.removeAt(0)
      thingsInNewPlace.add(item)
      println("Moved your $item into your new place!")
    }
  }

  // 7
  fun finishMove() {
    println("OK, we finished! We were able to move your:${thingsInNewPlace.toBulletedList()}")
  }
}”
```


“interface Checkable {
  fun checkIsOK(): Boolean
}”
“class Mover<T: Checkable>”
“This updated constraint means that attempting to create a Mover with a class that does not conform to Checkable will fail at compile time. Before continuing, add one more private var to the Mover class below the other three to hold things that fail the check:”


“interface Container<T> {
  // 2
  fun canAddAnotherItem(): Boolean
  fun addItem(item: T)
  // 3
  fun canRemoveAnotherItem(): Boolean
  fun removeItem(): T
  // 4
  fun getAnother(): Container<T>
  // 5
  fun contents(): List<T>
}”

Excerpt From
Kotlin Apprentice
By Irina Galata
This material may be protected by copyright.