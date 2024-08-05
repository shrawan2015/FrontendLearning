
Dispatch is the act of sending something somewhere.
- There are two forms of dispatch, `**static**` and `**dynamic**`. The former means that a call to a method is resolved at **compile time** and the latter means that is resolved at **run time**. Dynamic dispatch is the mechanism that allows polymorphic operations.

- Static dispatch means the function is resolved at compile-time to the receiver’s static type’s function. The function cannot be overridden by subtypes. The function can sure be defined in subtypes, but they will not be invoked.

- Dynamic dispatch means the function is resolved at runtime to the receiver’s dynamic type’s function. The function can be overridden by subtypes. Overridable functions are also called virtual functions.



Extensions do not actually modify classes they extend. By defining an extension, you do not insert new members into a class, but merely make new functions callable with the dot-notation on variables of this type.

We would like to emphasize that extension functions are dispatched **statically**, i.e. they are not virtual by receiver type. This means that the extension function being called is determined by the type of the expression on which the function is invoked, not by the type of the result of evaluating that expression at runtime.


If I rephrase this again, the “virtual”(overridable) members would be among the following

- members(functions or properties) in _normal classes_ with `open` inheritance modifier (members are either `final`(default) or `open`; `abstract` members are not allowed)
- members in _interfaces_ (members are either `open` or `abstract`, depending on the existence of implementation; `final` members are not allowed)
- members in _abstract classes_ with `open` or `abstract` modifiers (members are `final`(default) or `open` or `abstract`)



**Althoug members of companion objects are resolved dynamically as well. The compiler will generate a static acess to get the instance of the companion object. After that it is treated as any other instance in kotlin. If you want static dispatch for companion object members you have to annotate them wiht `@JvmStatic` (I don’t think there is a JS or native equivalent).**

Actually, the difference exists in kotlin, too. Extension functions are statically dispatched, meaning you cannot polymorphically override them in a subclass. In order for the overriding method to be called, the static (compile-time) type needs to be the subclass. This is the difference to member functions, which are dynamically dispatched.

This might not be a big issue. But it can definitely confuse developers that try to override them. And here it could lead to a bug: if the static type is not the subtype, It would silently fail the developer’s intention.

Ref:-
- https://discuss.kotlinlang.org/t/what-does-the-term-dispatch-and-virtual-mean-in-the-documentation/16579/2
- https://kotlinlang.org/docs/extensions.html#nullable-receiver
- https://stackoverflow.com/questions/30408010/what-are-the-limits-on-dynamic-double-dispatch-in-kotlin
- https://medium.com/ingeniouslysimple/static-and-dynamic-dispatch-324d3dc890a3
- https://discuss.kotlinlang.org/t/how-does-generics-specialization-work-in-kotlin/21067
- https://discuss.kotlinlang.org/t/how-does-generics-specialization-work-in-kotlin/21067/5
- https://kotlinlang.org/spec/overload-resolution.html#overload-resolution
- https://users.scala-lang.org/t/dynamic-dispatch-on-object-but-static-dispatch-on-arguments-sometimes/5350/2
- https://en.wikipedia.org/wiki/Multiple_dispatch
- https://betterprogramming.pub/static-dispatch-over-dynamic-dispatch-a-performance-analysis-47f9fee3803a
- https://discuss.kotlinlang.org/t/what-does-the-term-dispatch-and-virtual-mean-in-the-documentation/16579/4
- https://discuss.kotlinlang.org/t/use-an-operator-other-than-dot-for-extension-function-calls/8352/4
- https://medium.com/@senazincircioglu/extension-functions-of-kotlin-c66862737868
https://www.kotlinprimer.com/extension-functions/basics/what-extension-functions-are-not/
https://cs.hofstra.edu/~cscccl/csc17/dd.java
https://discuss.kotlinlang.org/t/a-way-to-enforce-static-properties-in-sub-classes/11777/2
https://www.dhiwise.com/post/the-complete-guide-to-kotlin-sealed-classes

https://kotlinlang.org/spec/overload-resolution.html#overload-resolution