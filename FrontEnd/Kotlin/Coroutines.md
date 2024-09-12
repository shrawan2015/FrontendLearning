
Running code in background
Suspend functions
Builders 
Jobs


# Scope:
Provides lifecycle methods for coroutines


- Build in scope and Custom scope coroutineScope
- Global scope
- ViewModel Scope
- Lifecycle scope - Lifecycle of android components



```kotlin

GlobalScope. Launch { this: CoroutineScope
		deLay (timeMilks; 1000)
		 println ("Coroutines")
}
print ("Hello ")

Thread. sleep ( millis: 2000)

}
```


Context:-
context is a set of data that relates to the coroutines
All coroutines have an associated context

Important elements of a context
- ﻿﻿Dispatcher - which thread the coroutine is run on
- Job - ﻿﻿handle on the coroutine lifecycle / Pause-destroy coroutines

# Dispatcher
Which type of threads does the coroutine run on-

**Dispatchers.Main** - lightweight tasks, have access to the main thread
**Dispatchers.IO** -  network, disk, database operations
**Dispatchers.Default** - intensive data processing
**runBlocking** - main thread / Block main thread - Block main thread


```kotlin

fun main(){
GlobalScope. Launch { this: CoroutineScope 
	println("Coroutine from global scope")
}
println ("Continue execution")
}

Output - Continue execution

Globalscope will not RUN


GlobalScope.laucnh(Dispatcher.IO) {

}

COUROTINE WILL RUN IN PARTICULAR DISPATCHER


```


**Suspend** 


# Builders:-

**launch** - starts a coroutine, does not return a result
**async** - returns a result from coroutines
**coroutineScope** - launch multiple coroutines 
**supervisorScope** - manages children failures
**runBlocking** - blocks current


# Jobs:-

Handle on coroutines.

- A .launch() call returns a Job
- Allows us to manipulate the coroutine lifecycle
- Live in the hierarchy of other Jobs both as parents or children
- If a job is cancelled, all its parents and children will be cancelled too

**25. Explain the suspend modifier in Kotlin.**
**26. What is the purpose of the withContext() function in Kotlin coroutines?**