
In **Kotlin**, everything has a value. Always. 

Once you understand this, it is not difficult to imagine that even a method that doesn’t specifically return anything has a default value. 

- That default value is named Unit. 
- Unit is the name of exactly one object, the value things have if they don’t have any other value. 
- The type of the Unit object is, conveniently, named Unit.

- The whole concept of Unit can seem odd to Java developers who are used to a dis‐ tinction between expressions—things that have a value—and statements—things that don’t.


_Unit_ is a type in Kotlin, like _Boolean_ and _String,_ for example, but that only has one value, the _Unit_ object.

In general, _Unit_ is used when you would use _void_ in Java. For example, the following Kotlin code:


|   |
|---|
|fun sample(){} // i.e fun sample(): Unit {}|