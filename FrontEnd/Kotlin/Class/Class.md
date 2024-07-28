```
class Student(
  val firstName: String,
  val lastName: String,
  val grades: MutableList<Grade> = mutableListOf(),
  var credits: Double = 0.0
) {

  fun recordGrade(grade: Grade) {
    grades.add(grade)
    credits += grade.credits
  }
override fun equals(other: Any?): Boolean {
    if (this === other)
      return true
}

val jane = Student(firstName = "Jane", lastName = "Appleseed")

// Error: jane is a `val` constant
jane = Student(firstName = "John", lastName = "Appleseed")

```


data class StudentData(
  var firstName: String,
  var lastName: String,
  var id: Int
)”

val marieCopy = marie.copy()
“val (firstName, lastName, id) = marie”


**Classes are a named type that can have properties and methods.
Classes use references that are shared on assignment.
Class instances are called objects.
Objects are mutable.
Mutability introduces state, which adds complexity when managing your objects.
Data classes allow you to create simple model objects that avoid a lot of boilerplate for comparing, printing, and copying objects.
Destructuring declarations allow you to easily extract multiple properties of data class objects.”**

