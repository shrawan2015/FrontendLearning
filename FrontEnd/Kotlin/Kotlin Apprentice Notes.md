
### Functions are the first step in grouping small pieces of code together into a larger unit. 


**Functions as variables**
Functions in Kotlin are simply another data type. You can assign them to variables and constants just as you can any other type of value, such as an Int or a String.

```kotlin
fun add(a: Int, b: Int): Int {
  return a + b
}
var function = ::add
function(4, 2)


fun printResult(function: (Int, Int) -> Int, a: Int, b: Int) {
  val result = function(a, b)
  print(result)
}
printResult(::add, 4, 2)

```


- Functions can have the same name with different parameters. This is called overloading.
- This is called overloading and lets you define similar functions using a single name.


These event loops are often started in an application by calling a function which is known to never return. If you start developing Android apps, think back to this paragraph when you encounter the main thread, also known as the UI thread.

Kotlin has a way to tell the compiler that a function is known to never return. You set the return type of the function to the Nothing type, indicating that nothing is ever returned from the function.

A crude, but honest, implementation of a function that wouldn’t return would be as follows:
```kotlin
fun infiniteLoop(): Nothing {
  while (true) {

  }
}
```


**A lambda expression is simply a function with no name; you can assign it to a variable and pass it around like any other value. This chapter shows you how convenient and useful lambdas can be.**

“Lambdas are also known as anonymous functions, ”


Here’s a declaration of a variable that can hold a lambda:
```kotlin
var multiplyLambda: (Int, Int) -> Int”
multiplyLambda = { a: Int, b: Int -> Int
  a * b
}

val lambdaResult = multiplyLambda(4, 2) // 8


var doubleLambda = { a: Int ->
  2 * a
}

doubleLambda = { 2 * it }
val square: (Int) -> Int = { it * it }

```

- The lambda expression returns the value of the last expression in the body.
- A lambda does not allow the use of names for arguments; for instance, you can't write multiplyLambda(a = 4, b = 2). Unlike functions, you can’t use the parameter names for labeling the arguments.

**Lambdas as arguments**

```kotlin
fun operateOnNumbers(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
  val result = operation(a, b)
  println(result)
  return result
}

val addLambda = { a: Int, b: Int ->
  a + b
}
operateOnNumbers(4, 2, operation = addLambda) // 6”

fun addFunction(a: Int, b:Int) = a + b

operateOnNumbers(4, 2, operation = ::addFunction) // 6”

operateOnNumbers(4, 2, operation = { a: Int, b: Int ->
  a + b
})

operateOnNumbers(4, 2, { a, b ->
  a + b
})

operateOnNumbers(4, 2, operation = Int::plus)

operateOnNumbers(4, 2) { a, b ->
  a + b
}

var unitLambda: () -> Unit = {
  println("Kotlin Apprentice is awesome!")
}
unitLambda()”

var nothingLambda: () -> Nothing = { throw NullPointerException() }


fun countingLambda(): () -> Int {
  var counter = 0
  val incrementCounter: () -> Int = {
    counter += 1
    counter
  }
  return incrementCounter
}”
val counter1 = countingLambda()
println(counter1())
println(counter1())
println(counter1()) 

```


```kotlin
“public inline fun <T> Iterable<T>.filter(predicate: (T) -> Boolean): List<T>”

“This means that filter takes a single parameter named predicate, which is a lambda (or function) that takes a T and returns a Boolean. The filter function then returns a list of T. In this context, T refers to the type of items in the list. In the example above, Double.”

```


# The heap vs. the stack

- When you create a reference type such as a class, the system stores the actual instance in a region of memory known as the **heap**. References to the class instances are stored in a region of memory called the **stack**, unless the reference is part of a class instance, in which case the reference is stored on the heap with the rest of the class instance.
- Both the heap and the stack have essential roles in the execution of any program:
- The system uses the stack to store anything on the immediate thread of execution; it is tightly managed and optimized by the CPU. When a function creates a variable, the stack stores that variable and then destroys it when the function exits. Since the stack is so well organized, it’s very efficient, and thus quite fast.
- The system uses the heap to store instances of reference types. The heap is generally a large pool of memory from which the system can request and dynamically allocate blocks of memory. Lifetime is flexible and dynamic. The heap doesn’t automatically destroy its data like the stack does; additional work is required to do that. This makes[…]”


- Since a class is a reference type, when you assign to a variable of a class type, the system does not copy the instance; only a reference is copied.


# object
- Kotlin uses object to denote a custom type for which only a single instance can be created. The name choice for the object keyword can sometimes lead to confusion with class instances, since they're also called objects. 
- You can also use object to create anonymous objects, for which multiple instances are created each time the anonymous object is used, another potential source of confusion.”
- *Use of singletons is sometimes discouraged because they introduce a global state into your application; therefore, you must be careful when accessing a singleton from different application threads. But singletons are useful in certain use cases wherein the scope of use is limited*.

**Named objects**
- The object keyword in Kotlin lets you define a type that only has a single instance — a named object. A type defined with object cannot have constructors: Since there is only one instance of an object, there is no reason to provide constructor functions to create other instances. In a sense, the type is the instance.

```KOTLIN
object X {
  var x = 0
}

object StudentRegistry {
  val allStudents = mutableListOf<Student>()

  fun addStudent(student: Student) {
    allStudents.add(student)
  }

  fun removeStudent(student: Student) {
    allStudents.remove(student)
  }

  fun listAllStudents() {
    allStudents.forEach {
      println(it.fullName)
    }
  }
}
StudentRegistry.addStudent(marie)
StudentRegistry.listAllStudents()

object JsonKeys {
  const val JSON_KEY_ID = "id"
  const val JSON_KEY_FIRSTNAME = "first_name"
  const val JSON_KEY_LASTNAME = "last_name"
}


```

There is no static keyword in **Kotlin**.

- The static keyword is used in these other languages to denote a class member that is common to all instances of the class and is not specific to each instance. Static members remove the need to duplicate items that are common to all instances.
- But removing this code duplication is useful, so how does Kotlin allow you to define static members? You do so by creating a companion object inside the class.”

```KOTLIN
class Scientist private constructor(
    val id: Int,
    val firstName: String,
    val lastName: String) {

  companion object {
    var currentId = 0

    fun newScientist(firstName: String, lastName: String): Scientist {
      currentId += 1
      return Scientist(currentId, firstName, lastName)
    }
  }

  var fullName = "$firstName $lastName"
}
```

- A common use case for static members is to implement the *factory pattern* for creating new class instances. You're using the factory pattern in Scientist by making the class **primary constructor private** and adding a **factory** method newScientist() to the companion object, which creates new scientist instances. 
- By making the constructor private, you enforce that the new scientist instances can only be created using the **factory method**, ensuring that your currentId value is correctly incremented whenever new scientest objects are instantiated.


You can create a **repository** of scientists as a singleton:

```KOTLIN

object ScientistRepository {
  val allScientists = mutableListOf<Scientist>()

  fun addScientist(student: Scientist) {
    allScientists.add(student)
  }

  fun removeScientist(student: Scientist) {
    allScientists.remove(student)
  }

  fun listAllScientists() {
    allScientists.forEach {
      println("${it.id}: ${it.fullName}")
    }
  }
}
val emmy = Scientist.newScientist("Emmy", "Noether")
val isaac = Scientist.newScientist("Isaac", "Newton")
val nick = Scientist.newScientist("Nikola", "Tesla")

ScientistRepository.addScientist(emmy)
ScientistRepository.addScientist(isaac)
ScientistRepository.addScientist(nick)

ScientistRepository.listAllScientists()

companion object Factory {
  // companion object members
}
Scientist isaac = Scientist.Factory.newScientist("Isaac", "Newton")
```