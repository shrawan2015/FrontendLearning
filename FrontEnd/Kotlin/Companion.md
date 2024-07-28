
- A **companion object** is an object that is associated with a class, rather than an instance of the class. 
- It can be used to define static methods and properties for the class. For example, the following code defines a companion object for the MyClass class, with a static method “myStaticMethod”:

```kotlin
class MyClass {   
 companion object {   
 fun myStaticMethod() {   
 /* code */ 
 }  
 }   
}
```


 - A class is a blueprint for creating objects, while an object is a single instance of a class. Objects are often used to implement singletons in Kotlin.
