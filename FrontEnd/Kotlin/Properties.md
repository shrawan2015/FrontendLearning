
- “Properties are variables and constants that are part of a named type.
- Default values can be used to assign a value to a property within the class definition.
- Property initializers and the init block are used to ensure that the properties of an object are initialized when the object is created.
- Custom accessors are used to execute custom code when a property is accessed or set.
- The companion object holds properties that are universal to all instances of a particular class.
- Delegated properties are used when you want to observe, limit or lazily create a property. You’ll want to use lazy properties when a property’s initial value is computationally intensive or when you won’t know the initial value of a property until after you’ve initialized the object.
- lateinit can be used to defer setting the value of a property reference until after the instance is created.
- Extension properties allow you to add properties to a class outside of the class definition, for example, if you’re using a class from a library.”

## Constructor properties
## Property initializers

## Companion object properties
```kotlin

class Level(
  val id: Int,
  var boss: String,
  var unlocked: Boolean
) {
  companion object {
    var highestLevel = 1
  }
}

val level3 = Level(id = 3, boss = "Chupacabra", unlocked = false)
val highestLevel = level3.highestLevel
val highestLevel = Level.highestLevel // 1
```

Using a companion object property means you can retrieve the same property value from anywhere in the code for your app or algorithm. The game’s progress is accessible from any level or any other place in the game, like the main menu.


## Delegated properties

“Most of the property initialization you’ve seen so far has been straightforward. You provide an initializer for a property, for example, as a literal value or default value, or you use custom accessors to compute the value.

You may want to pass the initialization off to another object, or delay the initialization from when the instance is created.”

“You can also use delegated property observers to limit the value of a variable. Say you had a light bulb that could only support a maximum current flowing through its filament.”

```kotlin

class LightBulb {
  companion object {
    const val maxCurrent = 40
  }
  var current by Delegates.vetoable(0) {
    _, _, new ->
    if (new > maxCurrent) {
      println(
        "Current too high, falling back to previous setting.")
      false
    } else {
      true
    }
  }
}
```


## Lazy properties
“If you have a property that might take some time to calculate and you don’t want to slow things down until you actually need the property, say hello to lazy properties.”

```kotlin
class Circle(var radius: Double = 0.0) {
  val pi: Double by lazy {
    ((4.0 * Math.atan(1.0 / 5.0)) - Math.atan(1.0 / 239.0)) * 4.0
  }
  val circumference: Double
    get() = pi * radius * 2
}
```
”


## lateinit

“If you just want to denote that a property will not have a value when the class instance is created, then you can use the lateinit keyword.”

```kotlin
class Lamp {
  lateinit var bulb: LightBulb
}
```

Since the property has no value when the class instance is initialized, and the property will be changed at some later time, you must use var with lateinit and not val.


```kotlin
“val lamp = Lamp()
// ... lamp has no lightbulb, need to buy some!

println(lamp.bulb)
// Error: kotlin.UninitializedPropertyAccessException:
// lateinit property bulb has not been initialized

// ... bought some new ones
lamp.bulb = LightBulb()”

“If you try to access the lateinit bulb property before it’s been initialized, you’ll get an exception. Ouch!”

```

## Extension properties

To add an extension property, create a new property with the property name appended to the class name, like so:

```kotlin
val Circle.diameter: Double
  get() = 2.0 * radius
```

You’ve created an extension property named diameter on the Circle class, and are providing a custom getter for diameter. Extension properties do not have backing fields, so you can only define them using custom accessors.”
