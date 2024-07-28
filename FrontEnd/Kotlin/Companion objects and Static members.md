
“The static keyword is used in these other languages to denote a class member that is common to all instances of the class and is not specific to each instance. Static members remove the need to duplicate items that are common to all instances.

But removing code duplication is useful, so how does Kotlin allow you to define static members? You do so by creating a companion object inside the class.”


“You create the companion object by prepending companion to an object defined in the class. Add this class to your file:”

```

“class Scientist private constructor(
  val id: Int,
  val firstName: String,
  val lastName: String
) {

  companion object {
    var currentId = 0

    fun newScientist(
      firstName: String,
      lastName: String
    ): Scientist {
      currentId += 1
      return Scientist(currentId, firstName, lastName)
    }
  }

  var fullName = "$firstName $lastName"
}”
```

“A common use case for static members is to implement the factory pattern for creating new class instances. You’re using the factory pattern in Scientist by making the class primary constructor private and adding a factory method newScientist() to the companion object, which creates new scientist instances.”

“By making the constructor private, you enforce that the new scientist instances can only be created using the factory method, ensuring that your currentId value is correctly incremented whenever new scientest objects are instantiated.”

“You can create a repository of scientists as a singleton. Add the following ScientistRepository:”

```

“object ScientistRepository {
  val allScientists = mutableListOf<Scientist>()

  fun addScientist(scientist: Scientist) {
    allScientists.add(scientist)
  }

  fun removeScientist(scientist: Scientist) {
    allScientists.remove(scientist)
  }

  fun listAllScientists() {
    allScientists.forEach {
      println("${it.id}: ${it.fullName}")
    }
  }
}”
```



## Implicit name of Companion

“The companion object is given an ***implicit name of Companion***. You can use a custom name by adding it after the companion object keywords:”

```
“companion object Factory {
  // companion object members
}”

“Scientist isaac = Scientist.Factory.newScientist("Isaac", "Newton");”

```


## Using anonymous objects


“You use object to create the Kotlin version of anonymous classes called anonymous objects or object expressions”
“Anonymous classes are used in Java to override the behavior of existing classes without the need to subclass, and also to implement interfaces without defining a concrete class. In both cases, the compiler creates a single anonymous instance, to which no name need be given. 

```
interface Counts {
  fun studentCount(): Int
  fun scientistCount(): Int
}

“val counter = object : Counts {
  override fun studentCount(): Int {
    return StudentRegistry.allStudents.size
  }

  override fun scientistCount(): Int {
    return ScientistRepository.allScientists.size
  }
}

println(counter.studentCount()) // > 3
println(counter.scientistCount()) // > 3

“You create an instance of the counter using the object keyword followed by a colon and the name of the interface. Inside braces, you override each of the interface methods. Run this code so you can see the counts print out.”
```




- “The singleton pattern is used when you want only one instance of a type to be created in your app.
- The object keyword is unique to Kotlin compared with similar languages, and it gives you a built-in way to make singletons with named objects. It also lets you make anonymous objects, the Kotlin version of Java anonymous classes.
- A class companion object gives you the Kotlin equivalent of Java static members.
- Anonymous objects — or object expressions — let you create unnamed instances of interfaces and to override class behavior without subclassing.
- Using Show Kotlin Bytecode and decompiling in IntelliJ IDEA is an informative way to understand what the Kotlin compiler is doing.”





