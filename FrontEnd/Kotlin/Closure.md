
“Lambas (as well as local functions) act as closures, which means that they can access and modify variables defined outside of their own scope. Unlike Java, variables declared in the outer scope can be modified within the closure.”

```kotlin

var result = 0
val sum = { a: Int, b: Int ->
  result = a + b
}

sum(5, 18)

```



