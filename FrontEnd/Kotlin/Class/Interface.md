

Interfaces aren’t anything you instantiate directly. Instead, they define a blueprint of behavior that concrete types conform to. 

With an interface, you define a common set of properties and behaviors that concrete types go and implement. The primary difference between interfaces and other custom types is that interfaces themselves cannot contain state.”

interface Vehicle {
  fun accelerate()
  fun stop()
}


An interface can be implemented by a class or object, and when another type implements an interface, it’s required to define the methods and properties defined in the interface. Once a type implements all members of an interface, the type is said to conform to the interface.


class Unicycle: Vehicle {
  var peddling = false

  override fun accelerate() {
    peddling = true
  }

  override fun stop() {
    peddling = false
  }
}
“Here, you create a Unicycle that inherits from and conforms to Vehicle.”



“enum class Direction {
  LEFT, RIGHT
}

interface DirectionalVehicle {
  fun accelerate()
  fun stop()
  fun turn(direction: Direction)
  fun description(): String
}”

“Methods declared in interfaces can contain default parameters, just like methods declared in classes and top-level functions. Add this class as an example:”

“interface OptionalDirectionalVehicle {
  fun turn(direction: Direction = Direction.LEFT)
}”


class OptionalDirection: OptionalDirectionalVehicle {
  override fun turn(direction: Direction) {
    println(direction)
  }
}

### Notice that when you implement turn() you don’t need to repeat the default value of the direction parameter.


## Default method implementations

```
interface SpaceVehicle {
  fun accelerate()
  // 1
  fun stop() {
    println("Whoa, slow down!")
  }
}

class LightFreighter: SpaceVehicle {
  // 2
  override fun accelerate() {
    println("Proceed to hyperspace!")
  }
}
```


```
class Starship: SpaceVehicle {
  override fun accelerate() {
    println("Warp factor 9 please!")
  }

  override fun stop() {
    super.stop()
    println("That kind of hurt!")
  }
}
```


### Properties in interfaces


```
interface VehicleProperties {
  val weight: Int // abstract
  val name: String
    get() = "Vehicle"
}
```


##Interfaces cannot themselves hold state## , as there are no backing fields to hold the data stored in an interface property. You must either let the property be abstract with no value, or give the property a default getter, like for name in VehicleProperties.

```
class Car: VehicleProperties {
  override val weight: Int = 1000
}

class Tank: VehicleProperties {
  override val weight: Int
    get() = 10000

  override val name: String
    get() = "Tank"
}
```


### Iterator

Kotlin lists, maps, and other collection types all provide access to Iterator instances. Iterator is an interface defined in the Kotlin standard library, and declares methods next(), which should give the next element of the collection, and hasNext(), which returns a boolean indicating whether the collection has more elements.