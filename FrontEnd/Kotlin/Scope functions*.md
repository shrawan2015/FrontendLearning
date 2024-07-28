
**Scope Functions** provide a concise way to apply a series of operations on an object, as well as reduce the amount of boilerplate code needed to perform common tasks.

Scope functions make code more clear, readable, and concise which are Kotlin language’s main features.

- **Way of referring to a context object** (i.e. using either ‘this’ or ‘it’ keyword) and 
- **return value** (i.e. returns either ‘context object’ or ‘lambda result’)
- Scope function differ in that they return a lambda result or context object
- Lambda Result refers to the return value of a lambda expression
- “Context Object” refers to the environment in which a function is executed.
- **The point of a scope function is to take an existing object - called a **context object** [2](https://typealias.com/start/kotlin-scopes-and-scope-functions/#fn:2) - and represent it in a particular way inside that new scope.**

##  5 Kotlin Scope Functions

`_let_` _,_ `_run_`_,_ `_with_`_,_ `_apply_`_,_ and `_also_`.

# 1. let

- `let` function is used to perform an operation on a non-null object
- return a new value or do some further operations
- It can also be used to perform chains of operations on a non-null object.
- The `let` function can also be used to perform `null` checks and execute a block of code only if the object is not null.
- Performing an operation on a non-null object and returning a new value
- Performing null checks and executing a block of code only if the object is not null
- Performing chains of operations on a non-null object
-  **`let` function for executing lambdas on non-null objects and for introducing an expression as a variable in the local scope.**
- **let function is often used to provide null safety calls.**
- Use safe call operator(?.) with ‘let’ for null safety. It executes the block only with the non-null value.
- Can be used to invoke one or more functions on results of call chains.


```kotlin
val result = "Kotlin".let { it.toUpperCase() }.plus("!")

val nullableString: String? = null  
nullableString?.let {  
// this code block will only be executed if `nullableString` is not null  
it.length  
}
```


```kotlin
val numbers = mutableListOf<Int>()

    // When
    val count = numbers.let {
        it.add(1)
        it.add(2)
        it.count()
    }

    // Then
    assertThat(count).isEqualTo(2)
- Executes the `let` function on a list of integers
- The lambda adds to the list using the `it` variable and returns the resulting count.
```

```kotlin

 // Given 
    val optionalVal: String? = "Hello"
    
    // When
    val message = optionalVal?.let { "$it World!" }
    
    // Then
    assertThat(message).isNotNull().isEqualTo("Hello World!")


	// Given 
    val optionalVal: String? = null

    // When
    val message = optionalVal?.let { "This shouldn't be called." }

    // Then
    assertThat(message).isNull()
```

```kotlin


val numbers = mutableListOf("one", "two", "three", "four", "five")  
val resultList = numbers.map { it.length }.filter { it > 3 }  
println(resultList)  


#Using let  
val numbers = mutableListOf("one", "two", "three", "four", "five")  
numbers.map{ it.length }  
.filter { it > 3 }  
.let { println(it)  
// and more function calls if needed  
}
```

```kotlin

val str: String? = "Hello"  
//processNonNullString(str) // compilation error: str can be null  

val length = str?.let {  
	println("let() called on $it")  
	processNonNullString(it) // OK: 'it' is not null inside '?.let { }'  
	it.length  
}

```

# 2. run

- The `run` function is similar to `let`
-  it’s used to execute a block of code on a non-null object and return the result
- It’s often used to perform a series of operations on an object, without the need to create an additional variable.
- Performing a series of operations on a non-null object and returning the result
- Accessing properties and functions of a non-null object without needing to specify the object each time
- The `run` function is commonly used for object creation and computing a result
- **Context object:** as a receiver(this).
- **Return value:** lambda result.
- run is useful when your lambda both initializes objects and computes the return value.
- Using run we can perform null safety calls as well as other computations.
- **The `run()` function works the same as `with()` but it’s an extension function instead of a normal, top-level function**
- Another advantage of using `run()` instead of `with()` is that you can use the safe call  operator

```kotlin
address.run {
    street1 = "9801 Maple Ave"
    street2 = "Apartment 255"
    city = "Rocksteady"
    state = "IN"
    postalCode = "12345"
}
```

```kotlin

val firstName: String? = null  
var middleName: String?=null  
var lastName: String? = null  
  
middleName = "M "  
lastName = "Vasava"  
  
firstName?.run {  
	val fullName = this + middleName+ lastName  
	print(fullName) //print only M Vasava  
}

```

```kotlin

val service = HttpService()

val result = service.run {
    port = 8888
    context = "/acme"
    fetchResults()
}


val numbers = mutableListOf<Int>()

    // When
    val count = numbers.run {
        add(1)
        add(2)
        count()
    }

    // Then
    assertThat(count).isEqualTo(2)

```


```kotlin
val title = "The Robots from Planet X3"
val newTitle = title
    .removePrefix("The ")
    .run { "'$this'" }
    .uppercase()
```
# 3. with

- The `with` function is similar to `run`, but it can be used with any object, not just non-null ones. It allows you to access the object’s properties and functions without needing to specify the object each time.
- Accessing properties and functions of any object without needing to specify the object each time
- **The `with` function isn't an extension function, meaning it a regular function that takes the context object as a parameter and returns the result of the lambda.**
- **Context object:** as a receiver(this).
- **Return value:** lambda result.
-
## Note
Recommended use of ‘with’ for calling functions on context objects without providing the lambda result. In code, **with can be read as “with this object, do the following.”**

```kotlin

val numbers = mutableListOf(“one”, “two”, “three”)  
with(numbers) {  
	println("'with' is called with argument $this")  
	println("It contains $size elements")  
}
```


```kotlin
val numbers = mutableListOf<Int>(1, 2)

    // When
    val count = with(numbers) {
        count()
    }

    // Then
    assertThat(count).isEqualTo(2)
```


**When you need to use the same variable over and over again, you can end up with a lot of duplication**
```kotlin
address.street2 = "Apartment 255"
address.city = "Rocksteady"
address.state = "IN"
address.postalCode = "12345"
```


```kotlin
with(address) {
     street1 = "9801 Maple Ave"
     street2 = "Apartment 255"
     city = "Rocksteady"
     state = "IN"
     postalCode = "12345"
}

We can use the `with()` scope function to introduce a new scope where the `address` becomes an [implicit receiver]
```


# 4. apply

- The `apply` function is used to configure an object by setting its properties or calling its functions, and then return the modified object
- It’s often used to initialise objects in a concise and readable way.
- Configuring an object by setting its properties or calling its functions and returning the modified object
- Initializing objects in a concise and readable way
- **The `apply` function provides `this` as an object reference and returns the context object. The `apply` function is commonly used to configure objects.**
- **Context object:** as a receiver (this).
- **Return value:** object itself.
- - we recommend that you use it for code blocks that don’t return a value and that mainly operate on the members of the receiver object. The most common use case for apply is for object configuration. Such calls can be read as “apply the following assignments to the object.”


```kotlin
val person = Person("Dhaval", 25).apply {  
	address = "123 Main Street"  
	phoneNumber = "555–1234"  
}

val adam = Person(“Adam”).apply {  
	age = 32  
	city = "London"  
}  
println(adam) // print Person(name=Adam, age=32, city=London)

```


```kotlin

val numbers = mutableListOf<Int>().apply {
        add(1)
        add(2)
    }

    // Then
    assertThat(numbers).containsExactly(1, 2)
```
# 5. also

- The `also` function is similar to `let`, but it returns the original object instead of the result of the lambda expression. It’s often used for side effects, such as logging or debugging.
- Performing side effects, such as logging or debugging, on an object
- Chaining additional operations on the original object after performing side effects
- The `also` function is a scope function that is commonly used to provide additional effects to an object
- **Context object:** as an argument (it).
- **Return value:** object itself.

```kotlin
val person = Person("John", 25)  
	person.also {  
		println("Name: ${it.name}, Age: ${it.age}")  
	}.celebrateBirthday()
	
```


```kotlin
val numbers = mutableListOf<Int>().also {
        it.add(1)
        it.add(2)
    }

    // Then
    assertThat(numbers).containsExactly(1, 2)
```

![[Pasted image 20240728192357.png]]

# 32. Explain scope functions in Kotlin.

Scope functions in Kotlin are essential constructs that simplify the code structure by providing concise ways to perform operations on objects within a specific scope. These functions include let, run, with, apply, and also.

- **let**: Executes a given block of code on a non-null object and returns the result.
- run: It is similar to let, but used with extension functions and allows access to the object’s properties without the need for the explicit reference.
- **with**: Takes an object and a lambda expression as parameters, allowing direct access to the object’s members without the need for the explicit reference.
- **apply**: Applies a lambda expression to an object and returns the modified object. It is useful for initialising object properties.
- **also**: Performs additional actions on an object and returns the same object. It is used for logging or performing side effects.


- **_let_**_: working with nullable objects to avoid NullPointerException._
- **_apply_** _: changing object configuration._
- **_run_**_: operate on nullable object, executing lambda expressions._
- **_also_**_: adding additional operations._
- **_with_**_: operating on non-null objects._



![[Pasted image 20240728192637.png]]

![[Pasted image 20240728202725.png]]




Ref:
https://medium.com/@KaushalVasava/scope-functions-in-kotlin-48297147d408
https://medium.com/@vefacanbeytorun/scope-functions-in-kotlin-c8ca8f13e749
https://typealias.com/start/kotlin-scopes-and-scope-functions/

Famous questions:

**What is the scope function “let” in Kotlin?**
**What is the scope function “run” with receiver in Kotlin?**
