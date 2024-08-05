

_Sealed_ classes and interfaces provide controlled inheritance of your class hierarchies. All direct subclasses of a sealed class are known at compile time. No other subclasses may appear outside the module and package within which the sealed class is defined. The same logic applies to sealed interfaces and their implementations: once a module with a sealed interface is compiled, no new implementations can be created.

When you combine sealed classes and interfaces with the `when` expression, you can cover the behavior of all possible subclasses and ensure that no new subclasses are created to affect your code adversely.

Sealed classes are best used for scenarios when:

- **Limited class inheritance is desired:** You have a predefined, finite set of subclasses that extend a class, all of which are known at compile time.
    
- **Type-safe design is required:** Safety and pattern matching are crucial in your project. Particularly for state management or handling complex conditional logic. For an example, check out [Use sealed classes with when expressions](https://kotlinlang.org/docs/sealed-classes.html#use-sealed-classes-with-when-expression).
    
- **Working with closed APIs:** You want robust and maintainable public APIs for libraries that ensure that third-party clients use the APIs as intended.

```kotlin

// Create a sealed interface sealed interface Error // Create a sealed class that implements sealed interface Error sealed class IOError(): Error // Define subclasses that extend sealed class 'IOError' class FileReadError(val file: File): IOError() class DatabaseError(val source: DataSource): IOError() // Create a singleton object implementing the 'Error' sealed interface object RuntimeError : Error
```

```kotlin
sealed class Error(val message: String) {
    class NetworkError : Error("Network failure")
    class DatabaseError : Error("Database cannot be reached")
    class UnknownError : Error("An unknown error has occurred")
}

fun main() {
    val errors = listOf(Error.NetworkError(), Error.DatabaseError(), Error.UnknownError())
    errors.forEach { println(it.message) }
}
// Network failure 
// Database cannot be reached 
// An unknown error has occurred
```


```kotlin
enum class ErrorSeverity { MINOR, MAJOR, CRITICAL } sealed class Error(val severity: ErrorSeverity) { class FileReadError(val file: File): Error(ErrorSeverity.MAJOR) class DatabaseError(val source: DataSource): Error(ErrorSeverity.CRITICAL) object RuntimeError : Error(ErrorSeverity.CRITICAL) // Additional error types can be added here }


sealed class IOError { // A sealed class constructor has protected visibility by default. It's visible inside this class and its subclasses constructor() { /*...*/ } // Private constructor, visible inside this class only. // Using a private constructor in a sealed class allows for even stricter control over instantiation, enabling specific initialization procedures within the class. private constructor(description: String): this() { /*...*/ } // This will raise an error because public and internal constructors are not allowed in sealed classes // public constructor(code: Int): this() {} }
```


```kotlin
sealed interface Error // enum class extending the sealed interface Error enum class ErrorType : Error { FILE_ERROR, DATABASE_ERROR }
```


```KOTLIN
// Sealed interface 'Error' has implementations only in the same package and module 
sealed interface Error 
// Sealed class 'IOError' extends 'Error' and is extendable only within the same package 
sealed class IOError(): Error 
// Open class 'CustomError' extends 'Error' and can be extended anywhere it's visible 
open class CustomError(): Error
```


```KOTLIN
// Function to log errors
fun log(e: Error) = when(e) {
    is Error.FileReadError -> println("Error while reading file ${e.file}")
    is Error.DatabaseError -> println("Error while reading from database ${e.source}")
    Error.RuntimeError -> println("Runtime error")
    // No `else` clause is required because all the cases are covered
}
```


```KOTLIN
sealed class UIState { data object Loading : UIState() data class Success(val data: String) : UIState() data class Error(val exception: Exception) : UIState() } fun updateUI(state: UIState) { when (state) { is UIState.Loading -> showLoadingIndicator() is UIState.Success -> showData(state.data) is UIState.Error -> showError(state.exception) } }
```


```KOTLIN
sealed class Payment { data class CreditCard(val number: String, val expiryDate: String) : Payment() data class PayPal(val email: String) : Payment() data object Cash : Payment() } fun processPayment(payment: Payment) { when (payment) { is Payment.CreditCard -> processCreditCardPayment(payment.number, payment.expiryDate) is Payment.PayPal -> processPayPalPayment(payment.email) is Payment.Cash -> processCashPayment() } }
```

Ref:- 
https://www.dhiwise.com/post/the-complete-guide-to-kotlin-sealed-classes
https://kotlinlang.org/docs/sealed-classes.html#api-request-response-handling
https://stackoverflow.com/questions/68326298/how-and-when-to-use-kotlin-sealed-classes-in-java?noredirect=1&lq=1