
“Kotlin uses object to denote a custom type that can only have a single instance.”

“The name choice for the object keyword can sometimes lead to confusion with class instances, since they’re also called objects. As you’ll see in this chapter, you can also use object to create anonymous objects, for which a new instance is created each time the anonymous object is used, another potential source of confusion

“In discussing your code, you’ll often have to rely on the context to determine whether an “object” is a class instance, the single instance of an entity created using object or an anonymous object.

The object keyword lets you easily implement a common pattern in software development: The singleton pattern.”


“Named objects

**The object keyword in Kotlin lets you define a type that only has a single instance — a named object.”**

**“A type defined with object cannot have constructors: Since there is only one instance of an object, there is no reason to provide constructor functions to create other instances. In a sense, the type is the instance.”**

object X {
  var x = 0
}


“An example use case for a singleton is an in-memory repository for a set of data. ”

```
object StudentRegistry {
  val allStudents = mutableListOf<Student>()

  fun addStudent(student: Student) {
    allStudents.add(student)
  }

  fun removeStudent(student: Student) {
    allStudents.remove(student)
  }

  fun listAllStudents() {
    allStudents.forEach {
      println(it.fullName)
    }
  }
}
“StudentRegistry.addStudent(marie)
StudentRegistry.addStudent(albert)
StudentRegistry.addStudent(emmy)

StudentRegistry.listAllStudents()”

```

“Using object, you create a registry that:
Maintains the list of students in a mutable list.
Lets you add and remove students from the registry.
Lets you print out the full name of all the students in the registry.”

```
object JsonKeys {
  const val JSON_KEY_ID = "id"
  const val JSON_KEY_FIRSTNAME = "first_name"
  const val JSON_KEY_LASTNAME = "last_name"
}

```

Comparison to classes

- While constructors are not allowed for objects, they do have many similarities with classes:
- Objects can have properties and member functions.
- Properties of the object must be initialized before use, either at declaration or in an init block.
- Objects can inherit from classes and implement interfaces.”
