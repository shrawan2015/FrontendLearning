
**Annotation** is a special kind of Kotlin class which allows you to define custom metadata and bind them to elements of your source code: declarations, expressions, or whole files. 
- Similar to their Java counterparts, Kotlin annotations can be accessed at runtime.
- Basic case is annotating a declaration when you put a @-prefixed annotation name into its modifier list.
- Annotations are means of attaching metadata to code
- They are pivotal in providing instructions to the compiler, guiding code analysis tools, and facilitating runtime processing
- Annotations in Kotlin are a form of metadata that provide data about the program but are not part of the program itself.
- Instead, they are used by the compiler and various tools during the build process,and can also be accessed at runtime through reflection.
- Kotlin annotations can be applied to classes, functions, properties, property accessors, parameters, and constructors.
-  Annotation parameters cannot have nullable types, because the JVM does not support storing `null` as a value of an annotation attribute.
- If an annotation is used as a parameter of another annotation, its name is not prefixed with the `@` character:


```kotlin
class MyTestCase { 

	@Test
	fun testOnePlusOne() { assert(1 + 1 == 2)} 
}
```


To declare an annotation, put the `annotation` modifier in front of a class:

```swift

annotation class Fancy
annotation class Special


@Special class MyClass { }
@Special fun myFunction() { }

// This annotation can be used to annotate various program elements.



// **Annotation Parameters**
annotation class Review(val reviewer: String, val date: String)
@Review(reviewer = "John Doe", date = "2022-01-01")
class Document { }

```

**Built-in Annotations**

```KOTLIN

@Deprecated("This function will be removed in future releases.")  
fun oldFunction() { }


@Fancy  
public class MyJavaClass { }
```

```kotlin

@Target(AnnotationTarget.CLASS, AnnotationTarget.FUNCTION, AnnotationTarget.TYPE_PARAMETER, AnnotationTarget.VALUE_PARAMETER, AnnotationTarget.EXPRESSION) @Retention(AnnotationRetention.SOURCE) @MustBeDocumented annotation class Fancy


@Fancy class Foo { 
	@Fancy fun baz(@Fancy foo: Int): Int {
		 return (@Fancy 1) 
	}
 }

class Foo @Inject constructor(dependency: MyDependency) { ... }
//annotate the primary constructor of a class 


class Foo { var x: MyDependency? = null @Inject set }
// You can also annotate property accessors:

```



```kotlin
annotation class Special(val why: String)
@Special("example") class Foo {}


annotation class ReplaceWith(val expression: String)

annotation class Deprecated( 
	val message: String, 
	val replaceWith: ReplaceWith = ReplaceWith("")) 

@Deprecated("This function is deprecated, use === instead", ReplaceWith("this === other"))


```



 - Custom annotations offer a way to express additional semantics, enforce constraints, or facilitate integration with frameworks and libraries in a declarative manner.
 - Custom annotations can significantly improve code readability by providing explicit markers for certain behaviors or characteristics.

```KOTLIN

annotation class Loggable


@Target(AnnotationTarget.FUNCTION, AnnotationTarget.CLASS)  
annotation class Loggable


annotation class Loggable(val level: String = "INFO")

@Loggable(level = "DEBUG")  
class UserService

@Loggable // Uses the default logging level "INFO"  
fun update(user: User) {  
// Function implementation  
}


fun checkLoggable(function: KFunction<*>) {  
function.findAnnotation<Loggable>()?.let {  
println("Function ${function.name} is loggable with level ${it.level}.")  
}  
}  
  
// Usage  
checkLoggable(::updateUser)

@Retention(AnnotationRetention.SOURCE)  
annotation class DebugLog



@Target(AnnotationTarget.CLASS, AnnotationTarget.FUNCTION)  
annotation class Todo

@Retention(AnnotationRetention.BINARY)  
@Target(AnnotationTarget.CLASS, AnnotationTarget.FUNCTION)  
annotation class WorkInProgress


```




```kotlin
annotation class ReplaceWith(val expression: String)

annotation class Deprecated(
        val message: String,
        val replaceWith: ReplaceWith = ReplaceWith(""))

@Deprecated("This function is deprecated, use === instead", ReplaceWith("this === other"))
```



Ref:
https://kotlinlang.org/docs/annotations.html#arrays-as-annotation-parameters
https://medium.com/@m.abuzaid.ali/how-to-create-custom-annotations-in-kotlin-f7ed238b52eb
https://kotlinlang.org/spec/annotations.html
https://kotlinlang.org/docs/annotations.html#arrays-as-annotation-parameters
https://ankur-s20.medium.com/kotlin-annotations-tutorial-for-beginners-with-example-55ad745f4ae8
https://americanexpress.io/advanced-kotlin-use-site-targets/