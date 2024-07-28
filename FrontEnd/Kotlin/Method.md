


A class definition is like a blueprint, whereas an instance is a real object. To access the value of an instance, you use the keyword this inside the class.”
“The keyword this acts as a reference to the current instance. Make a SimpleDate3 with this transformed method:

```kotlin

fun monthsUntilWinterBreak(): Int {
  // 2
  return months.indexOf("December") - months.indexOf(this.month)
}
```

## Object methods

For class companion objects, like companion object properties, you can use companion object methods to access data across all instances. You call companion object methods on the class itself, instead of on an instance. To define a companion object method, you put its definition inside the companion object block.

Object methods are useful for things that are about a type in general, rather than something about specific instances.


```kotlin

class MyMath {
  // 1
  companion object {
    fun factorial(number: Int): Int {
      // 2
      return (1..number).fold(1) { a, b -> a * b }
    }
  }
}

// 3
MyMath.factorial(6) // 720”
```


## Extension methods
```kotlin

fun SimpleDate.monthsUntilSummerBreak(): Int {
  val monthIndex = months.indexOf(month)
  return if (monthIndex in 0..months.indexOf("June")) {
    months.indexOf("June") - months.indexOf(month)
  } else if (monthIndex in
      months.indexOf("June")..months.indexOf("August")) {
    0
  } else {
    months.indexOf("June") + (12 - months.indexOf(month))
  }
}”

“This creates an extension method monthsUntilSummerBreak() on the SimpleDate class.

“fun Int.abs(): Int {
  return if (this < 0) -this else this
}

println(4.abs())    // > 4
println((-4).abs()) // > 4”

```


## Companion object extensions

“If your class has a companion object, you can add extension methods to it by using the implicit companion object name Companion, or by using the custom name if the companion object has one.”

```kotlin

fun MyMath.Companion.primeFactors(value: Int): List<Int> {
  // 1
  var remainingValue = value
  // 2
  var testFactor = 2
  val primes = mutableListOf<Int>()
  // 3
  while (testFactor * testFactor <= remainingValue) {
    if (remainingValue % testFactor == 0) {
      primes.add(testFactor)
      remainingValue /= testFactor
    } else {
      testFactor += 1
    }
  }

  if (remainingValue > 1) {
    primes.add(remainingValue)
  }

  return primes
}
```