
**45. What is the difference between init and constructor in Kotlin?**


```
```class Student(
  val firstName: String,
  val lastName: String,
  val grades: MutableList<Grade> = mutableListOf(),
  var credits: Double = 0.0
) {

  fun recordGrade(grade: Grade) {
    grades.add(grade)
    credits += grade.credits
  }
}```

```class Person(var firstName: String, var lastName: String) {
  fun fullName() = "$firstName $lastName"
}

// is the same as

class Person constructor(var firstName: String, var lastName: String) {
  fun fullName() = "$firstName $lastName"
}```




`init` is an initialization block that is executed when an instance of a class is created. It is used to initialize properties or perform other setup operations. The primary constructor and any secondary constructors are responsible for creating the instance, while the `init` block handles the initialization logic. The main difference is that the `init` block is always executed regardless of which constructor is used. Here's an example: