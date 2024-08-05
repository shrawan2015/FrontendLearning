
In summary,  
an `object` or a `companion object` is one singleton object in Kotlin.  
You can assign variables in an _object_ or _objects_, and then use the variables just like they were singletons.

`object` or `companion object` is instantiated when it is first used. `val`s and `var`s in an `object` are initialized when the `object` is first instantiated (i.e., when the `object` is first used).

**EDIT**: "a `companion object` is when the class is loaded."

```kotlin
object MySingleton
```

```kotlin
object MySingleton {
    fun someFunction(...) {...}
}
```

```kotlin
object UtilProject {

    // here you put all member functions, values and variables
    // that you need in your singleton Util class, for example:

    val maxValue: Int = 100

    fun compareInts(a: Int, b: Int): Int {...}
}

UtilProject.compareInts(1, 2)
//or
var value = UtilProject.maxValue

```

```kotlin
companion object {
    val instance = UtilProject()
} 

class UtilProject {
    ....
    companion object {
        val instance = UtilProject()
    }
}

class AnotherClass {
    ...
    companion object {
        val instance = AnotherClass()
        const val abc = "ABC"
    }
}

fun main(args: Array<String>) {
    val a = UtilProject.instance // UtilProject.instance will be initialized here.
    val b = AnotherClass.abc // AnotherClass.instance will be initialized here because AnotherClass's companion object is instantiated.
    val c = AnotherClass.instance
}


class UtilProject {
    ....
    companion object {
        fun f() = ...
    }
}

class AnotherClass {
    ...
    companion object {
        const val abc = "ABC"
    }
}

object UtilProjectSingleton {
    val instance = UtilProject()
}

object AnotherClassSingleton {
    val instance = AnotherClass()
}

fun main(args: Array<String>) {
    UtilProject.f()
    println(AnotherClass.abc)

    val a = UtilProjectSingleton.instance // UtilProjectSingleton.instance will be initialized here.
    val b = AnotherClassSingleton.instance // AnotherClassSingleton.instance will be initialized here.

    val c = UtilProjectSingleton.instance // c is a.
}



class UtilProject {
    ....
    companion object {
        fun f() = ...
    }
}

class AnotherClass {
    ...
    companion object {
        const val abc = "ABC"
    }
}

object Singletons {
    val utilProject = UtilProject()
    val anotherClass = AnotherClass()
}

fun main(args: Array<String>) {
    val a = Singletons.utilProject
    val b = Singletons.anotherClass 
}


companion object {
    val instance: UtilProject by lazy { UtilProject() }
}


class MyClass(context: Context) : Dialog(context) {
    companion object {
    lateinit var INSTANCE: MyClass

    @JvmStatic
    fun getInstance(context: Context): MyClass{
        if (!::INSTANCE.isInitialized) {
            INSTANCE = MyClass(context)
        }

        return INSTANCE
    }
}}

```


Ref:
https://stackoverflow.com/questions/51834996/singleton-class-in-kotlin#:~:text=an%20object%20or%20a%20companion,when%20it%20is%20first%20used.
https://blog.mindorks.com/how-to-create-a-singleton-class-in-kotlin/
https://in-kotlin.com/design-patterns/singleton/
https://kiwix.ounapuu.ee/content/stackoverflow.com_en_all_2023-11/questions/52183717/kotlin-singleton-how-to-copy-object-from-singleton
https://kiwix.ounapuu.ee/content/stackoverflow.com_en_all_2023-11/questions/35587652/kotlin-thread-safe-native-lazy-singleton-with-parameter