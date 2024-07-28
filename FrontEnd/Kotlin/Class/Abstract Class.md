

- In certain situations, you may want to prevent a class from being instantiated, but still be able to be inherited from.
- “This will let you define properties and behavior common to all subclasses. 
- You can only create instances of the subclasses and not the base, parent class. Such parent classes are called abstract.
- Classes declared with the abstract keyword are open by default and can be inherited from.


- In abstract classes, you can also declare abstract methods marked with abstract that have no body. The abstract methods **must** be overridden in subclasses.


**Answer:** An abstract class is a class that cannot be instantiated, and it can have abstract and non-abstract methods. An interface, on the other hand, is a collection of abstract methods and constants that can be implemented by any class. ==One key difference between the two is that a class can implement multiple interfaces, but it can only extend one abstract class.==
