
Extension functions allow you to add new functions to existing classes without modifying their source code. They enhance the functionality of classes, making them more versatile. Extension functions are defined outside the class they extend and are called as if they were members of the class.


fun String.isEmail(): Boolean {  
return this.contains("@")  
}  
  
val email = "example@example.com"  
val isValidEmail = email.isEmail() // true