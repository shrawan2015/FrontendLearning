
**Extension functions** allow you to add new functions to existing classes without modifying their source code. 

- They enhance the functionality of classes, making them more versatile. 
- Extension functions are defined outside the class they extend and are called as if they were members of the class.

```kotlin

fun String.isEmail(): Boolean {  
	
	return this.contains("@")  

}  

val email = "example@example.com"  
val isValidEmail = email.isEmail() // true


import strings.lastChar
val c = "Kotlin".lastChar()”



import strings.*
val c = "Kotlin".lastChar()”



import strings.lastChar as last
val c = "Kotlin".last()”


```


**“No overriding for extension functions”**
- Method overriding in Kotlin works as usual for member functions, but you can’t override an extension function

```KOTLIN

“fun View.showOff() = println("I'm a view!")
fun Button.showOff() = println("I'm a button!")
 
fun main() {
    val view: View = Button()
    view.showOff()              ❶
    // I'm a view!
}”

“❶ The extension function is resolved statically.”

“It might help to recall that an extension function is compiled to a static function in Java with the receiver as the first argument. Java would choose the function the same way:”

“As you can see, overriding doesn’t apply to extension functions; Kotlin resolves them statically.”


“fun <T> List<T>.last(): T { /* returns the last element */ }
fun Collection<Int>.sum(): Int { /* sum up all elements */ }”

```



## Extension properties

```KOTLIN

val String.lastChar: Char
    get() = this.get(length - 1)”


“var StringBuilder.lastChar: Char
    get() = this.get(length - 1)          ❶
    set(value) {                          ❷
        this.setCharAt(length - 1, value)
    }”


```


```KOTLIN

class User(val id: Int, val name: String, val address: String)
 
fun User.validateBeforeSave() {
    fun validate(value: String, fieldName: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException(
               "Can't save user $id: empty $fieldName")   ❶
        }
    }
 
    validate(name, "Name")
    validate(address, "Address")
}
 
fun saveUser(user: User) {
    user.validateBeforeSave()                             ❷
 
    // Save user to the database
}


```