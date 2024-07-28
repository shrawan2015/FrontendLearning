

- In certain situations, you may want to prevent a class from being instantiated, but still be able to be inherited from.
- “This will let you define properties and behavior common to all subclasses. 
- You can only create instances of the subclasses and not the base, parent class. Such parent classes are called abstract.
- Classes declared with the abstract keyword are open by default and can be inherited from.
- In abstract classes, you can also declare abstract methods marked with abstract that have no body. The abstract methods **must** be overridden in subclasses.
- An abstract class is a class that cannot be instantiated, and it can have abstract and non-abstract methods. An interface, on the other hand, is a collection of abstract methods and constants that can be implemented by any class. ==One key difference between the two is that a class can implement multiple interfaces, but it can only extend one abstract class.==
- You can also declare a class as abstract, making it so the class can’t be instantiated. An abstract class usually contains abstract members that don’t have implementations and must be overridden in subclasses. Abstract members are always open, so you don’t need to use an explicit open modifier (just like you don’t need an explicit open modifier in an interface).”

```kotlin

“abstract class Animated {                     ❶
    abstract val animationSpeed: Double       ❷
    val keyframes: Int = 20                   ❸
    open val frames: Int = 60                 ❸
 
    abstract fun animate()                    ❹
    open fun stopAnimating() { /* ... */ }    ❺
    fun animateTwice() { /* ... */ }          ❺
}”

“This class is abstract: you can’t create an instance of it.

  ❷ This property is abstract: it doesn’t have a value, and subclasses need to override its value or accessor.

  ❸ Properties in abstract classes aren’t open by default but can be explicitly marked as open.

  ❹ This function is abstract: it doesn’t have an implementation and must be overridden in subclasses.

  ❺ Non-abstract functions in abstract classes aren’t open by default but can be marked as such.”


interface Expr
class Num(val value: Int) : Expr
class Sum(val left: Expr, val right: Expr) : Expr
 
fun eval(e: Expr): Int =
    when (e) {
        is Num -> e.value
        is Sum -> eval(e.right) + eval(e.left)
        else ->                                     ❶
            throw IllegalArgumentException("Unknown expression")
}

sealed class Expr                                     ❶
class Num(val value: Int) : Expr()
class Sum(val left: Expr, val right: Expr) : Expr()   ❷
 
fun eval(e: Expr): Int =
    when (e) {                                        ❸
        is Num -> e.value
        is Sum -> eval(e.right) + eval(e.left)
    }

```