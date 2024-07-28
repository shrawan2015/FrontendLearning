
The following functions are automatically derived by the compiler for the data classes:

- equals() — The equals() function returns true if two objects have the identical contents. It operates similarly to “==,” although for Float and Double values it works differently.
- hashCode() — The hashCode() function returns the object’s hashcode value.
- copy() — The copy() function is used to duplicate an object, changing only a few of its characteristics while leaving the rest unaltered.
- toString() — This function returns a string containing all of the data class’s parameters.
To ensure consistency, data classes must meet the following requirements:

- At least one parameter is required for the primary constructor.
- val or var must be used for all primary constructor parameters.
- Abstract, open, sealed, or inner data classes are not possible.
- Only interfaces may be implemented by data classes.