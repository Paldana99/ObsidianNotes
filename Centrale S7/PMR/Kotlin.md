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
equivalente al switch o case
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
---
## Classes:
- Auto-do getter-setter


```kt
class MyClass {

	val propertie_inmutabble: Int = 20
	var propertie_variable: Int = 10

	var propertie : Int
		get() = propertie_variable * 2
		// it can be private...
		set(value) {propertie - value}

	// Constructor
	constructor(parameter: Int) this() {
		val something = ...
	}
	
}
// Also:
class MyClass (val propertie1 : Int = 20, var prop2: Int = 1) {	
	// ...
}
```

### Class visibility:
- **Public** is used by default
- Private: Only file can access or Class, subclasses can't see.
- Protected: Inside class, Subclasses **can** see.
- Internal: Visible for the module

Classes with parameters: auto do getter and setter and make properties if we put *var* or *val*

```kt
class MyClass(var propertie1: Int = 10, val name: Sring = "some_name")
```

### Inheritance

We need to explicit put that the mother class is **open**, also for parameters

```kt
open class ClassParent (open var propertie1: Int = 10, val name: String = "the same name")

class ChildClass (val p3: Init = 10) ClassParent() {
	// it cannot acces to name
	override popertie1 = 20
} 
```

### Abstraction - Interfaces 
Both can't bee instantiated.

Differences: Abstraction have constructor

Abstraction for classes. **abstract** key for implement. The classes that will take inherith the abstract, need to implement all *abstract* methods/properties.
```kt
abstract class AquariumFish {
	abstract val color: String
}

class Shark: AquariumFish() {
	override val color = "gray"	
} 
```

Interface don't have constructor. 
```kt
interface FishAction {
	fun eat()
}

class Plecostumus: AquariumFish(), FishAction {
	// Take abstract class and interface
	override val color: String

	override fun eat() println("munch on algae")
}

// We can define fun that receive a Classes that need to implement an interface, this way we ensure it will have some properties/methos

fun feedFish (fish: FishAction) {
	// Receive a fish who implement an interface, 
	// so the method eat need to exist.
	fish.eat()
}
```

An abstract class can take an interface
```kt
interface FishAction {  
    fun eat()  
}  
  
abstract class AquariumFish : FishAction {  
    abstract val color : String  
    override fun eat() {  
        println("Eat...")  
    }  
}
```

#### Interface Delegation:  
> [!seealso] More info
> [Wikipedia: Delegation Pattern](https://en.wikipedia.org/wiki/Delegation_pattern)
> [Kotlin Wiki: Delegation](https://kotlinlang.org/docs/delegation.html)
> 

```kt
fun delegate() {  
    val pleco = Placostumus()  
    println("Fish has color: ${pleco.color}")  
    pleco.eat()  
}  
  
interface FishAction {  
    fun eat()  
}  
  
interface FishColor {  
    val color: String  
}  
  
// Object make a 1 instance only (Singleton Pattern)  
object GoldColor: FishColor {  
    override val color: String = "gold"  
}  
  
object RedColor: FishColor {  
    override val color: String = "red"  
}  
  
class PrintingFishAction(val food: String): FishAction {  
    override fun eat() {  
        println("Eat: ${food}")  
    }  
}  
  
class Placostumus(fishColor: FishColor = GoldColor):  
    FishAction by PrintingFishAction("algae"),  
    FishColor by fishColor
```
> [!note] Object
> Make a singletone class, only 1 instance is possible, every time is called, is always the same pointer. 
> ```kt
> object Singletone(val = id) {
> 	fun getID = return id
> }
> ```
### Data Class
```kt
Useful for classes that only hold data.
```kt
data class Decoration(val rocks: String, val wood: String, val diver: String)  
  
  
fun makeDecoration() {  
    var d1 = Decoration("crystal", "wood", "diver")  
    val d2 = Decoration("marble", "wood", "diver")  
  
    println( d1.equals(d2) ) // False  
    
    d1 = d2.copy() // Take same properties  
    println( d1.equals(d2)) // True  
  
    // Destructuring    
    val (rocks, wood, diver) = d1  
}
```

### Enum class
```kt
enum class Color(val rgb: Int) {
	RED(0xF000000)
	GREEN(0x00FF00)
	// ...
}
```
### Sealed class
_Sealed_ classes and interfaces represent restricted class hierarchies that provide more control over inheritance. All direct subclasses of a sealed class are known at compile time. No other subclasses may appear after a module with the sealed class is compiled.

```kt
sealed interface Error

sealed class IOError: Error

class FileError : IOError()
```

### Generic Class
Give any type to a class with **<T\>**, we can give bounds to this types with:
<T\> :  Any? or Any (for non null)
<T\> : Type
```kt
class MyList<T: Any?> {
	fun get(pos: Int): T {
		// ...
	}

val intList: MyList<Int> 
val fishList: MyList<Fish>
}
```
## Annotations
Everything can be annotades, and can receive parameters.