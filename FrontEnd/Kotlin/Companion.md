
- A **companion object** is an object that is associated with a class, rather than an instance of the class. 
- It can be used to define static methods and properties for the class. For example, the following code defines a companion object for the MyClass class, with a static method “myStaticMethod”:
- `companion object` is a special type of object that is associated with a class rather than an instance of the class. It's similar to static members in other programming languages, but with some added functionality.
- companion objects are unique because they allow you to define members that can be called on the class itself rather than on instances of the class.

```kotlin
class MyClass {   
	 companion object {   
		 fun myStaticMethod() {   
		 /* code */ 
		 }  
	 }   
}

class MyClass {  
// Regular class members  
		companion object {  
		// Members of the companion object  
		const val CONSTANT_VALUE = 42  
		fun staticFunction() {  
		// Code for the static function  
		}  
	}  
}


- Inside `MyClass`, theres a companion object` declared using the `companion` keyword.
- Members inside the `companion object` can be accessed using the class name without creating an instance of the class.

// val value = MyClass.CONSTANT_VALUE  
//MyClass.staticFunction()


class MyClass {  
	companion object Factory {  
	// Members of the companion object  
	}  
}  
// Accessing members using the custom name  
MyClass.Factory.someMethod()


class MyClass private constructor() {  
	companion object {  
		fun create(): MyClass {  
			return MyClass()  
		}  
	}  
}


class Constants {  
	companion object {  
		const val PI = 3.14  
		const val VERSION = "1.0"  
	}  
}

class Singleton {  
	companion object {  
		val instance: Singleton by lazy { Singleton() }  
	}  
}

class Utils {  
	companion object {  
	fun performTask() {  
		// Implementation  
	}  
	}  
}


class SharedPreferencesManager {  
	companion object {  
		fun saveData(key: String, value: String) {  
		// Implementation  
		}  
  
		fun getData(key: String): String {  
			// Implementation  
		}  
	}  
}


class MathOperations {  
	companion object {  
	fun add(a: Int, b: Int): Int {  
		return a + b  
}  
  
fun multiply(a: Int, b: Int): Int {  
	return a * b  
}  
}  
}


class Logger {  
	companion object {  
		fun log(message: String) {  
// Implementation  
		}  
	}  
}

class StringExtensions {  
	companion object {  
		fun String.reverse(): String {  
			return this.reversed()  
		}  
	}  
}


class MyClass {  
	companion object {  
	// Initialization block  
	init {  
		// Initialization code  
	}  
	}  
}


```


 - A class is a blueprint for creating objects, while an object is a single instance of a class. Objects are often used to implement singletons in Kotlin.

```kotlin

**Namespace for Factory Methods:**
class User private constructor(val name: String) {  
	companion object {  
		fun newUser(name: String): User {  
			return User(name)  
		}  
	}  
}  
  
val user = User.newUser("John Doe")

**Constants and Utility Functions**

class Constants {  
	companion object {  
		const val MAX_AGE = 100  
		const val MIN_AGE = 1  
	}  
}  
  
println(Constants.MAX_AGE) // Output: 100  
println(Constants.MIN_AGE) // Output: 1


// **Encapsulation**
class Calculator {  
		companion object {  
			fun add(a: Int, b: Int): Int = a + b  
			fun subtract(a: Int, b: Int): Int = a - b  
	}  
}  
  
val result = Calculator.add(5, 3)  
println(result) // Output: 8



# Example: Using Companion Object for Factory Method
class User private constructor(val name: String) {  
		companion object {  
			fun newUser(name: String): User {  
				return User(name)  
			}  
		}  
}  
  
val user = User.newUser("John Doe")  
println(user.name) // Output: John Doe


# Companion Object with Constants
class Constants {  
		companion object {  
			const val MAX_AGE = 100  
			const val MIN_AGE = 1  
		}  
}  
  
println(Constants.MAX_AGE) // Output: 100  
println(Constants.MIN_AGE) // Output: 1



# Companion Object Extensions
class MyClass {  
		companion object {  
			fun greet() {  
			println("Hello from MyClass!")  
			}  
		}  
}  
  
fun MyClass.Companion.farewell() {  
		println("Goodbye from MyClass!")  
}  
  
MyClass.greet() // Output: Hello from MyClass!  
MyClass.farewell() // Output: Goodbye from MyClass!
```


Ref:

- https://medium.com/@mobiledev4you/companion-object-in-kotlin-c3a1203cd63c
- https://medium.com/@riztech.dev/understanding-companion-objects-in-kotlin-a93f1a5880a7#:~:text=Example%3A%20Using%20Companion%20Object%20for%20Factory%20Method&text=In%20this%20example%2C%20the%20User,to%20create%20instances%20of%20User%20.
