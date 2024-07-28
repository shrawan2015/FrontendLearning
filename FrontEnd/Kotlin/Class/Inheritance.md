```
// 1
open class Person(var firstName: String, var lastName: String) {
  fun fullName() = "$firstName $lastName"
}

// 2
class Student(
  firstName: String,
  lastName: String,
  var grades: MutableList<Grade> = mutableListOf<Grade>()
) : Person(firstName, lastName) {

  open fun recordGrade(grade: Grade) {
    grades.add(grade)
  }
}”
```


**“The open keyword means that the Person class is open to be inherited from; the need for open is part of the Kotlin philosophy of requiring choices such as inheritance to be explicitly defined by the programmer.”**

“A class that inherits from another class is known as a subclass or a derived class, and the class from which it inherits is known as a superclass or base class.”

#### The rules for subclassing are fairly simple:
- A Kotlin class can inherit from only one other class, a concept known as single inheritance.
- A Kotlin class can only inherit from a class that is open.
- There’s no limit to the depth of subclassing, meaning you can subclass from a class that is also a subclass, like below (and first redefining Student with open)
```

“println(hallMonitor is OboePlayer) // true, since assigned it to oboePlayer
println(hallMonitor !is OboePlayer) // also have !is for "not-is"
println(hallMonitor is Person) // true, because Person is ancestor of OboePlayer”
“(oboePlayer as Student).minimumPracticeTime // Error: No longer a band member!”


```
##### Kotlin also provides the as infix operator to treat a property or a variable as another type:
- as: An unsafe cast to a specific type that is known at compile time to succeed, such as casting to a supertype.
- as?: A safe cast (to a subtype). If the cast fails, the result of the expression will be null.”


#### “Inheritance, methods and overrides”








- Class inheritance is one of the most important features of classes and enables polymorphism.
- Subclassing is a powerful tool, but it’s good to know when to subclass. Subclass when you want to extend an object and could benefit from an “is-a” relationship between subclass and superclass, but be mindful of the inherited state and deep class hierarchies.
- The open keyword is used to allow inheritance from classes and also to allow methods to be overridden in subclasses.
- Sealed classes allow you to create a strictly defined class hierarchy that is similar to an enum class but that allow multiple instances of each subtype to be created and hold state.
- Secondary constructors allow you to define additional constructors that take additional parameters than the primary constructor and take different actions with those parameters.
- Nested classes allow you to namespace one class within another.
- Inner classes are nested classes that also have access to the other members of the outer class.
- Visibility modifiers allow you to control where class members and top-level declarations can be seen within your code and projects.
