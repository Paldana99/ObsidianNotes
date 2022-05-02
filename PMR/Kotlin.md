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