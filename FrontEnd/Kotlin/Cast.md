
**Type-Checks and Casting**:- Checking that a particular data is of the same data type which it is going to store from another variable.
**_SMART CASTS:- “is” and “!is” operator_**

**EXPLICIT TYPE-CASTING :-**
**A. UNSAFE CAST OPERATOR:-**
**B. SAFE CAST OPERATOR:-**

The Kotlin compiler is quite smart when it comes to casting. It reduces the amount of repeated code and helps predict casting exceptions at runtime.
- Smart casting, which is the automatic insertion of safe casts when necessary

Let me first give you a brief introduction. We have

**is** for Type Check and
**as** for Cast

While **is** focuses on type checking and smart casting, the **as** **operator** comes into play for **_explicit casting_**. 


## `as` as Unsafe cast operator

For scenarios where you are certain about the type **as** **operator** can be used for non-nullable casting. Thus, it’s called an unsafe cast operator throws an exception if the cast isn’t possible.

```kotlin

val stringValue: String = obj as String

If obj is null, then it can not be cast to String because **stringValue** type is non-nullable and it throws an exception

//java.lang.NullPointerException: null cannot be cast to non-null type kotlin.String
```

.

```kotlin
val stringValue: String? = obj as String?

What if obj is not a String type?

//java.lang.ClassCastException: java.lang.Integer cannot be cast to java.lang.String
```


# `as?` as Safe cast operator

Here **as?** **operator** comes as saviour in nullability and type safety conversation.
It is a warrior

```kotlin
val stringValue: String? = obj as? String  
print("stringValue=$stringValue")

By using **as?** You are safe from risking your life at runtime exceptions and gracefully handle scenarios where cast might not be possible.
```


```kotlin
if (obj is String) {  
	// obj is automatically cast to String  
	print(obj.length)  
}

Kotlin knows that within the “if” block variable is treated as **String** type and allows access to **_String specific functions_**. It eliminates the need for explicit casting and makes your code more concise and expressive.

```


```kotlin
fun printStringLength(text: Any) {  
	if (text is String) {  
		println("Length of string: ${text.length}") // Smart cast to String  
	} else {  
		println("Not a string")  
	}  
}

fun printStringLengthSafely(text: String?) {  
if (text != null) {  
		println("Length of string: ${text.length}") // Smart cast to String  
	} else {  
		println("String is null")  
	}  
}

fun processValue(value: Any) {  
	when (value) {  
		is String -> println("String: ${value.length}")  
		is Int -> println("Integer: $value")  
		else -> println("Unknown type")  
	}  
}
```





```kotlin
fun sample() {|
	val test: String? = "hi there"|
	if (!test.isNullOrEmpty()){|
		println(test.capitalize())|
	}
}

Yes, the compiler automatically adds a (test as String).capitalize() casting, since it can guarantee that the locally declared val won’t have changed values (thus won’t have become null) after the nullity check in line 3.

```


```kotlin
var test: String? = "hi there"
fun sample() {
    if (!test.isNullOrEmpty()) {
        println(test.capitalize())
    }
}

**A:** No, since now some other function could access the test variable and assign it a value of null, after the execution of line 4 and before line 5. Thus, the Kotlin compiler cannot guarantee that test is not null and the code won’t compile.


```

```kotlin
fun sample() {
    val test: String? by lazy {
        "hi there"
    }
    if (!test.isNullOrEmpty()) {
        println(test.capitalize())
    }
}

 No, when using the lazy function, the compiler cannot be sure that every call to the variable’s get() function will return the same value, meaning that even if the call in line 5 does not return null, the call in line 6 might. Thus, the code above won’t compile.

```


```kotlin
data class SampleDataClass(var test: String? = null){
    // Some implementation
}

fun sample(){
    val sampleDataClass = SampleDataClass()
    if (!sampleDataClass.test.isNullOrEmpty()){
        println(sampleDataClass.test.capitalize())
    }
}
**A:** No, inside the implementation of SampleDataClass, the nullable variable test could have its value changed to null. And this change could occur between the execution of lines 7 and 8, thus, the code above won’t compile.

```


# Type Erasure

Kotlin ensures type safety for operations involving [generics](https://kotlinlang.org/docs/generics.html) at compile time, while, at runtime, instances of generic types don’t hold information about their actual type arguments.

In practice, at runtime, this means that `List<Int>`and `List<String>` are erased to `List<*>`. With this in mind,
```kotlin

fun sample(x: Any) {
    if (x is List<*>) {
        println(x[0])
    }
    if (x is List<String>) {
        println(x[0].length)
    }
}
a No, since at runtime `List<String>` are erased to `List<*>` , the second if statement fails to compile. The compiler identifies that this check would fail at runtime and fails right away

```

```kotlin

fun sample(){
    val test : MutableList<String> = mutableListOf("hi there")
    (test as MutableList<Int>).add(123)
    println(test)
}
**A:** Yes, it will compile. At runtime, `MutableList<Int>`and `MutableList<String>` have the same type, so there’s no way of checking whether the test `_MutableList_` _has Ints or Strings. To help us avoid unwanted behavior, we do get a warning from the compiler indicating there is an unchecked cast (on line 3), precisely because of type erasure._


```


Ref:

- https://medium.com/learn-to-earn/navigating-kotlins-type-system-a-guide-to-type-checks-and-casts-with-is-and-as-0368ae9e4337
- https://medium.com/@riztech.dev/exploring-kotlins-key-features-extension-functions-and-smart-casts-699ae4346c62
- https://medium.com/codex/casting-in-kotlin-do-you-really-know-it-73532a727a64
- https://adi22maurya.medium.com/type-casting-type-checks-and-casting-in-koltin-2022-d0856e7420a4
