 It is similar to normal functions. Unlike normal functions, **there is no function name**. It is defined directly with the **fun** keyword.

```kotlin
val anonymousFunc = fun(number1:Int, number2:Int) : Int = number1 + number2  
println(anonymousFunc(1,2))


val myAnonymousFunc= fun(): Unit {  
	println("Hello Stranger!")  
}
Example has no parameter and no return value 👇
```

The syntax of an anonymous function in Kotlin is similar to regular functions, but without a name:

```kotlin


fun(parameterList): ReturnType {  
// function body  
}


fun(a: Int, b: Int): Int {  
	return a + b  
}

val numbers = listOf(1, 2, 3, 4, 5)  
val evenNumbers = numbers.filter(fun(number: Int): Boolean {  
				  return number % 2 == 0  
				  })


val greet: (String) -> String = fun(name: String): String {  
		return "Hello, $name!"  
}  
  
println(greet("John")) // Output: Hello, John!


fun createMultiplier(factor: Int): (Int) -> Int {  
	return fun(value: Int): Int {  
				return value * factor  
			}  
}  
  
val double = createMultiplier(2)  
println(double(5)) // Output: 10
```

Notes:
- It has short and simple syntax. It is especially suitable for one-time and simple operations.
- Provides flexibility. Can be assigned to variables, returned from another function, or passed as arguments
- It can be used easily with higher order functions.
- Anonymous functions avoid name conflict problem.
- It is a suitable structure for callback functions.

**Lambdas and [anonymous functions](https://kotlinlang.org/docs/lambdas.html#anonymous-functions) are not the same.**

-- **Difference in return type**  
    The return type inference for anonymous functions works just like for normal functions: the return type is inferred automatically for anonymous functions with an expression body, but it has to be specified explicitly (or is assumed to be Unit) for anonymous functions with a block body.
    
- **Difference in return statement**  
    A difference between lambda expressions and anonymous functions is the behavior of non-local returns.  
    A return statement without a label always returns from the function declared with the `fun` keyword.  
    This means that a return inside a lambda expression will return from the enclosing function, whereas a return inside an anonymous function will return from the anonymous function itself.
    > When passing anonymous functions as parameters, place them inside the parentheses. The shorthand syntax that allows you to leave the function outside the parentheses works only for lambda expressions.



Ref:

- https://medium.com/huawei-developers/kotlin-lambda-expressions-kotlin-anonymous-functions-example-tutorial-88a4b622f8b9
- https://www.scaler.com/topics/kotlin/lambda-expression-and-anonymous-functions-in-kotlin/
- https://tugce-aras.medium.com/lambda-expression-and-anonymous-function-in-kotlin-53bf408b5699
- https://medium.com/@s.badamestani/lambda-in-kotlin-a6fc055a2c88
- https://medium.com/@chaewonkong/exploring-anonymous-functions-in-kotlin-f211919432f
- https://medium.com/huawei-developers/kotlin-higher-order-functions-and-lambda-expressions-b799b42e8158
- https://kotlinlang.org/docs/lambdas.html#anonymous-functions
- https://stackoverflow.com/questions/47110879/kotlin-when-and-how-should-one-use-lambda-expressions

Inline functions
noinline
crossinline
Infix notation
Sequences