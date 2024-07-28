“Lambdas are also known as anonymous functions, and derive their name from the lambda calculus of Alonzo Church, in which all functions are anonymous.”

“Closures are so named because they have the ability to “close over” the variables and constants within the closure’s own scope. This simply means that a lambda can access, store and manipulate the value of any variable or constant from the surrounding context, acting as a nested function. Variables and constants used within the body of a lambda are said to have been captured by the lambda.

```
var multiplyLambda: (Int, Int) -> Int
multiplyLambda = { a: Int, b: Int -> Int
  a * b
}

```

“For a lambda that has only one parameter, you can shorten it even further using the it keyword. As an example, look at this lambda:

```
doubleLambda = { 2 * it }
var doubleLambda = { a: Int ->
  2 * a
}
```


```
fun operateOnNumbers(
  a: Int,
  b: Int,
  operation: (Int, Int) -> Int
): Int {
  val result = operation(a, b)
  println(result)
  return result
}
operateOnNumbers(4, 2, operation = { a: Int, b: Int ->
  a + b
})
”“operateOnNumbers(4, 2, { a, b ->
  a + b
})


operateOnNumbers(4, 2, operation = Int::plus)”
“operateOnNumbers(4, 2) { a, b ->
  a + b
}
```

```
var unitLambda: () -> Unit = {
  println("Kotlin Apprentice is awesome!")
}
unitLambda()”

“fun countingLambda(): () -> Int {
  var counter = 0
  val incrementCounter: () -> Int = {
    counter += 1
    counter
  }
  return incrementCounter
}
“val counter1 = countingLambda()
val counter2 = countingLambda()

println(counter1()) // > 1
println(counter2()) // > 1
println(counter1()) // > 2
println(counter1()) // > 3
println(counter2()) // > 2”

```



```
public inline fun <T> Iterable<T>.filter(predicate: (T) -> Boolean): List<T>
```

```
“This means that filter takes a single parameter named predicate, which is a lambda (or function) that takes a T and returns a Boolean. The filter function then returns a list of T. In this context, T refers to the type of items in the list. In the example above, Double.”

“var prices = listOf(1.5, 10.0, 4.99, 2.30, 8.19)

val largePrices = prices.filter {
  it > 5.0
}”

```


```
“Another handy function is fold, which takes a starting value and a lambda. The lambda takes two values: the current value and an element from the list. The lambda returns the next value that should be passed into the lambda as the current value parameter.”

“var sum = prices.fold(0.0) { a, b ->
  a + b
}”

“A function closely related to fold is reduce. In Kotlin, reduce uses the first element in the collection as the starting value:”
“sum = prices.reduce { a, b ->
  a + b
}
println(sum) // > 26.980000000000004”
```


```
“fun repeatTask(times: Int, task: () -> Unit)”
```



“Lambdas are functions without names. They can be assigned to variables and passed as arguments to functions.
Lambdas have shorthand syntax that makes them a lot easier to use than other functions.
A lambda can capture the variables and constants from its surrounding context.
A lambda can be used to direct how a collection is sorted.
There exists a handy set of functions on collections which can be used to iterate over the collection and transform the collection. Transforms include mapping each element to a new value, filtering out certain values, and folding or reducing the collection down to a single value.”




“lambda is a function literal, which can be invoked, passed as an argument or returned just like ordinary functions. In this chapter, you’ll learn a bit more about lambdas in the context of functional programming.

Recall the lambda syntax, using a lambda assigned to a variable pow:
val pow = { base: Int, exponent: Int ->
  Math.pow(base.toDouble(), exponent.toDouble())
}
A lambda expression is always defined in curly brackets. First, you declare the names and types of the lambda parameters, and, after the -> sign, you place the body of your lambda.”

“/** A function that takes 1 argument. */
public interface Function1<in P1, out R> : Function<R> {
  /** Invokes the function with the specified argument. */
  public operator fun invoke(p1: P1): R
}”
“It’s an interface with the single function invoke(), which receives a parameter of type P1 and return type of R.”


## Lambdas with receivers

“Just as you can specify a receiver for an extension function, you can do so for a lambda as well.”
“fun beginBattle(
  firstRobot: Robot,
  secondRobot: Robot,
  onBattleEnded: Robot.() -> Unit
) {
  var winner: Robot? = null
  battle(firstRobot, secondRobot)
  winner = if (firstRobot.isAlive) firstRobot else secondRobot
  winner.onBattleEnded()
}”

Excerpt From
Kotlin Apprentice
By Irina Galata
This material may be protected by copyright.