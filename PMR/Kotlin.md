# Kotlin
# CheatSheet:
## String
Template:
```kt
val day : String = Monday
println("Today is $day")
```
---
## Iterations
**WHEN:**
equivalente al swich o case
```kt
when(x) {
	1 -> println("x == 1")
	2 -> println("x == 2")
	else -> {
		println("x is other value")
	}
}
```
---
## Functions
Everything is an expression:
```kt
val time = 20
println(Thoday is: ${ if (day < 12) "Good Morning" else  "Good night"})
```

Filters: 
```kt
val decorations = listOf ("rock", "paper", "plastic")
println( decorations.filter{it[0] == 'p'} )
// return -> ["paper", "plastic"]
```
Lambdas : Function with no name.
```kt
val swim = { println("swim \n") }
swim()
// return -> swim

// Lambdas with an argument:
val waterFilter (Int) -> Int = { dirty -> dirty / 2 }
waterFilter(20)
// return -> 10

```
High Order functions: Functions that receive a function as parameter. 
```kt
// High order fun
updateDirty(dirty : Int, operation: (Int) -> Int) : Int {
	return operation(dirty)
}

val dirty : Int = 50
val waterFilter : (Int) -> Int = { dirty -> dirty / 2 }

fun feedFish (dirty : Int) = dirty + 10 

fun dirtyPoccesor() {
	// pass a lambda saved in var
	dirty = updateDirty(dirty, waterFilter)
	// pass a fun 
	dirty = updateDirty(dirty, ::feedFish)
	// pass a lambda defined
	dirty = updateDirty(dirty) {dirty -> dirty + 50}
}
```