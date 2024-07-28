
Sealed classes are useful when you want to make sure that the values of a given type can only come from a particular limited set of subtypes

“Sealed classes act very much like enum classes”

“Add a sealed class Shape that has subtypes Circle and Square:”

```
“sealed class Shape {
  class Circle(val radius: Int): Shape()
  class Square(val sideLength: Int): Shape()
}”

“val circle1 = Shape.Circle(4)
val circle2 = Shape.Circle(2)
val square1 = Shape.Square(4)
val square2 = Shape.Square(2)”
```

“You’re able to make as many Circles and Squares as you like, but no Shapes.”
```

“fun size(shape: Shape): Int {
  return when (shape) {
    is Shape.Circle -> shape.radius
    is Shape.Square -> shape.sideLength
  }
}

size(circle1) // radius of 4
size(square2) // sideLength of 2”

```


```
enum class DayOfTheWeek {

companion object {
  fun today(): DayOfTheWeek {
    // Code goes here
  }
}”
  // more code goes here
}

for (day in DayOfTheWeek.values()) {
  println("Day ${day.ordinal}: ${day.name}")
}

val dayIndex = 0
val dayAtIndex = DayOfTheWeek.values()[dayIndex]
println("Day at $dayIndex is $dayAtIndex")

val tuesday = DayOfTheWeek.valueOf("Tuesday")
println("Tuesday is day ${tuesday.ordinal}")
```


The  values() companion function on the enum class gives you a List of all the declared cases in the class, making it easy to go through all possibilities, and also to find out how many possibilities exist.

The ordinal property of each case gives that case’s index in the list of declared cases. You’ll note from what’s printed out that the order is zero-indexed.

The name property of each case takes the name of the case in code and gives back the String value of that name.”

```
val notADay = DayOfTheWeek.valueOf("Blernsday")
println("Not a day: $notADay")”
“Exception in thread "main" java.lang.IllegalArgumentException: No enum constant DayOfTheWeek.Blernsday
    at java.lang.Enum.valueOf(Enum.java:238)
    at DayOfTheWeek.valueOf(main.kt)
    at MainKt.main(main.kt:23)”
```


enum classes can have properties and functions”

enum class DayOfTheWeek(val isWeekend: Boolean)
enum class DayOfTheWeek(val isWeekend: Boolean = false)


```
val today = DayOfTheWeek.today()
when (today) {
  DayOfTheWeek.Monday -> println("I don't care if $today's blue")
  DayOfTheWeek.Tuesday -> println("$today's gray")
  DayOfTheWeek.Wednesday -> println("And $today, too")
  DayOfTheWeek.Thursday -> println("$today, I don't care 'bout you")
  DayOfTheWeek.Friday -> println("It's $today, I'm in love")
  DayOfTheWeek.Saturday -> println("$today, Wait...")
  DayOfTheWeek.Sunday -> println("$today always comes too late")
}
```


----

 A sealed class has a limited number of direct subclasses, all defined in the same file as the sealed class itself. It’s known as sealed as opposed to final


## There are a few key points to know about sealed classes:

- They are abstract. This means that you can’t instantiate an instance of the sealed class directly, only one of the declared subclasses.
- Related to that requirement, sealed classes can have abstract members, which must be implemented by all subclasses of the sealed class.
- Unlike enum classes, where each case is a single instance of the class, you can have multiple instances of a subclass of a sealed class.
- “You can’t make direct subclasses of a sealed class outside of the file where it’s declared, and the constructors of sealed classes are always private.
- You can create indirect subclasses (such as inheriting from one of the subclasses of your sealed class) outside the file where they’re declared, but because of the restrictions above, this usually doesn’t end up working very well.”


sealed class AcceptedCurrency {
  class Dollar: AcceptedCurrency()
  class Euro: AcceptedCurrency()
  class Crypto: AcceptedCurrency()
}


## “Enumeration as state machine”
