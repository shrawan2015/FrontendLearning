

## Object expressions﻿[](https://kotlinlang.org/docs/object-declarations.html#object-expressions)

_Object expressions_ create objects of anonymous classes, that is, classes that aren't explicitly declared with the `class` declaration. Such classes are useful for one-time use. You can define them from scratch, inherit from existing classes, or implement interfaces. Instances of anonymous classes are also called _anonymous objects_ because they are defined by an expression, not a name.
**Object expression** is a structure that creates a single instance of an **object**:

```kotlin
val coords = object {  
    var x = 10  
    var y = 10  
}
println(coords.x) // Prints: 10
```

Object expressions create objects of anonymous classes, that is, classes that aren’t explicitly declared with the `class` declaration. Such classes are useful for one-time use.

1. To create an object of an anonymous class that inherits from some type (or types), specify this type after `object` and a colon (`:`). Then implement or override the members of this class as if you were inheriting from it:
2. Object expressions are executed (and initialised) immediately, where they are used.
3. Object expression can use variables declared in its enclosing scope.

### Creating anonymous objects from scratch﻿[](https://kotlinlang.org/docs/object-declarations.html#creating-anonymous-objects-from-scratch)

Object expressions start with the `object` keyword.

If you just need an object that doesn't have any nontrivial supertypes, write its members in curly braces after `object`:

```kotlin
val helloWorld = object {
    val hello = "Hello"
    val world = "World"
    // object expressions extend Any, so `override` is required on `toString()`
    override fun toString() = "$hello $world"
}

print(helloWorld)
```

### Inheriting anonymous objects from supertypes﻿[](https://kotlinlang.org/docs/object-declarations.html#inheriting-anonymous-objects-from-supertypes)
### Using anonymous objects as return and value types﻿[](https://kotlinlang.org/docs/object-declarations.html#using-anonymous-objects-as-return-and-value-types)



Ref:-
https://kotlinlang.org/docs/object-declarations.html#accessing-variables-from-anonymous-objects
https://medium.com/@shelar.akshata/objects-in-kotlin-aeae831ce21a
https://www.kotlinprimer.com/classes-what-kotlin-brings-to-the-table/objects/object-expressions/
https://blog.kotlin-academy.com/kotlin-programmer-dictionary-object-expression-vs-object-declaration-791b183ad16b