# Swift Notes

## Basics

### Comments

<pre><code> 
// Standard comment.
/* Multi-Line
*/ 
</code></pre>
Multiline comments <b>will</b> nest.

<pre><code>/// Doc comments
/// Useful doc comment features for <b>methods:</b>
/// - Returns:
/// - Parameters:
/// - x: does something
/// - y: does something else!
/// - Parameter z: will be parameter comment for z
</code></pre>
Doc comments support markdown.
</br>Can use doc comments for classes and methods.

### Imports
<pre><code>import framework
@testable import framework
</code></pre>
Testable relaxes access rules for things you might have supressed access to when testing.

### Print
<pre><code>let s = world
print("hello\(s)", appendNewLine=false)</code></pre>
Print automatically adds new line unless specified.

### Available
<pre><code> if #available(iOS 8.0, OSX 10.0, *) {
	...
}
@available(iOS 8.0, OSX 10.0, *)
func onlyWorksWithNewerOS() { }
</code></pre>
Code will only run if specified OS versions are met.

### Operators
<pre><code>range 1…3 // up to and including 3
range 1..<3 // up to and NOT including 3

a&+b a&-b a&*b //arithmetic overload operators.
</code></pre>

Unary operators (++ — ! ~ + - &) bind tightly.
</br>Other operators have precedence levels.  Look up if necessary :)

### Declarations and Types
<pre><code>var someVar = 10		   // define variable

let anotherVar: Int		// define constant
anotherVar = 10
</code></pre>
Swift infers type.  Can specify type if want. </br>

6 basic types: Uint, Int, Double, Float, Bool, String.</br>
</br>First class objects. Have methods, can extend.

<b>NO implicit type conversion!</b></br></br>




Swift has String, Apple frameworks have NSString </br>
compiler bridges String->NSString </br>
Sometimes you NEED to declare NSString..

<pre><code>var swiftString : String = “abc”
var objcString : NSString = “def”

objcString = swiftString <b>(OKAY!)</b>
swiftString = objcString <b>(NOT OKAY!)</b>
swift = objcString as String <b>(OKAY!)</b>
</code></pre>

#### Strings
String is subclass of NSString (can’t assign super class as subclass)

<pre><code>string.characters.count() //<b>no string.length</b>

s[s.startIndex] —> first char in string
s[s.startIndex.successor()] —> second char
s[s.endIndex.predecessor()] —> last char
s[advance(s.startIndex, 2)] —> advances start index by 2, gets that char
s[advance(s.endIndex, -2)] negative advancement works too.

s.insert(“|”, atIndex: advance(s.startIndex,4))

let range = advance(s.endIndex,-6) ..< s.endIndex
s.removeRange(range)
</code></pre>

#### Optionals
<pre><code>let someString = “hello"
var possibleNum : Int?
possibleNum = Int(someString)
let x = possibleNum! // will blow up at runtime if possibleNum isn’t an Int
var possibleNum : Int! //definitely will have Int (auto unwrapped, can’t be nil)
</code></pre>

nil is not a legit value, so if something returns nil we get a runtime error.


####If let syntax:

<pre><code>if let a = optionalValue {
}

if someValue > 42 && otherValue < 19, 
    let a = getOptionalThing()
        where a > someValue {
}
</code></pre>

#### Arrays:

<pre><code>var someArray : [String] = [“a”,”b”,”c”]

// 2D array (really array of arrays)
var twoD : [[String]] = [[],[]]

// inserting to array
someArray.insert(“f”, atIndex:4)
someArray += [“e”,”f”]
someArray.append(“d”)

// removing from array
someArray.removeAtIndex(index)
someArray.removeLast()

// replacing values, 
someArray [1…2] = [“B”,”C”] // can even replace 1…2 with more than 2 values.
</code></pre>

#### Sets
Sets cannot have 2 of the same element.

<pre><code>var mySet : Set<String> = [“A”,”B”,”C”]

if let oldValue = a.remove(“A”) // remove may not return valid result.

a.isSubsetOf(b) // true if all elements in a are in b.
a.isStrictSubsetOf(b) //true if all elements are in b and a smaller than b.

/* these return a new set */
a.exclusiveOr(b)
a.intersect(b)
a.subtract(b)
a.union(b)

/* modify the set on the left to hold result */
a.exclusiveOrInPlace(b)
</code></pre>

#### Dictionaries
<pre><code>
var httpStatus: [Int:String] = [:]

if let old = httpStatus.updateValue(“PageNotFound”, forKey:404 {
	/* */
}
// iterates over all dict. entries
for(code, message) in httpStatus { } 

let allKeys = httpStatus.keys

// removes key and value
httpStatus[404] = nil

// extracts old value before removing
if let old = httpStatus.removeValueForKey(404) {
    }

</code></pre>

##Structs & Classes
classes = reference objects </br>
structs = value objects. </br>
behavior differs!! </br>
if assign a var to another class var, both are references. </br>
classes & structs may have classes & structs nested inside.

### Classes

<pre><code>
class Circle {
	var center = Point ()
	var radius = 0.0
	init(c:Point, r:Point) { center = c; radius = r}
	deinit { }
	
/* final means subclass cannot overwrite it. */
final func moveTo (center: Point) {
		self.center = center
	}

/* lazy defers init of field until its actually used. */
lazy var offset = getDefault()

/* static = all class instances have same offset2 */
static var offset2 = getDefault()

}
</code></pre>

Two ways to initialize: </br>

* either init
* explicity call init

can also have deinitializer, called when its destroyed by runtime
</br>
static field lazy by default. </br>



#### Class Method vs. Static Method
<pre><code>class func offset(here:Point) { … } // subclass can overwrite
static func offset(here:Point) { … } // subclass <b>cannot</b> overwrite
</code></pre>
Class level methods and fields are accessed by Class. prefix, as its part of the class, not an object.

### Structs
No deinit method.
<pre><code>struct Circle {
var center = Point ()
var radius = 0.0
init(c:Point, r:Point) { center = c; radius = r}

mutating func moveTo (center: Point) {
self.center = center
}

mutating func reset() { self = Circle() }

lazy var offset = getDefault()
static var offset2 = getDefault()
}
</code></pre>

Structs are constants by default. </br>
<b>Must explicit declare method as mutating if it modifies the struct!!!</b>

### Optional Chaining

<pre><code>class Node {
	var i = 9
	var optDict : [String:String]?
	var next : Node?
	func successor() ->Node?{return next}
}

let obj = Node()

//optional chain. — if obj.next not nil, continue.
if let a = obj.next?.next.i { }
if let a = obj.next?.optDict?[“k”]?.isEmpty { }

let obj = Node()
let optObj = obj.next
optObj!.successor() -> fails when optObj is nil
optObj?.successor() -> optional chaining!
</code></pre>

### Tuples

List of 2 or more things (don’t have to be same type)</br>
Treated as single variable or const. </br>
Tuples are first class in Swift.

<pre><code>let http404Error(404, “Not Found")

http404Error.0 -> 404
http404Error.1 -> “Not Found"

let (status , desc) = http404Error
print(“\(status)”)
</code></pre>
if you only want to access one value of tuple, use:
<pre><code>let (status, _) = http404Error //_ is a “wildcard”</code></pre>


tuple can also have names for fields
<pre><code>let http404Error = (code: 404, desc: “Not Found”)

http404Error.code -> 404

func fetch() -> (code:Int, description:String) {
	return (200, “Okay”)
}

let (error, description) = fetch()</code></pre>

###Enum
Actual type in swift.
<pre><code> enum CompassPoint {
	case North,
	case South,
	case East, West
}

var direction = CompassPoint.North
direction = .East

switch direction {
	case .East: print(“East”)
	default:	print(“Not East”)
}

enum PostalCode {
	case US(Int,Int)
	case UK(String)
	case CA(code:String)
}

var somewhere = PostalCode.US(11111,1111)
var somewhereElse = PostalCode.UK(“Hiya”)
var somewhere2 = PostalCode.CA(code:”Hehehe”)

switch somewhere {
	case .UK (let s): print (“\(s)”)
	case .US (let loc, var route):
		print(“\(loc)-\(route)”)
	case .CA: break;
}

enum ASCIIControls : Character {
	case NewLine = “\n”
	case Carriage = “\r"
}
</code></pre>
When every element of enum carries piece of data thats the SAME TYPE of all other carried elements, we call that a <b>raw element</b>.
<pre><code>enum Planet : Int {
	case Mercury = 1, Venus, Earth, Mars, Saturn, Uranus, Neptune
}
</code></pre>
here the compiler automatically gives Venus—>Neptune their raw values of 2—>8
<pre><code>let x = Planet.Earth.rawValue —> 3

enum Dimension {
	case DISTANCE ( Int )
	fun value() —> Int {
		switch self {
			case .DISTANCE ( let value ): return value
		}
	}
}
</code></pre>
now add the init to above enum:
<pre><code>init ( distance: Int ) { self = DISTANCE(height + 100)}</code></pre>

enum initializers must assign to self.
assign to self -> override current enum values with different one.

<pre><code>let aDistance = Dimension.DISTANCE(10)
aDistance.value() —> 10

let anotherDistance = Dimension(distance:10)
anotherDistance.value() —> 110
</code></pre>
so initializing standard way vs. with initializer gives you two different results…
<pre><code>
enum ConnectionState {
	case closed, opening, open, closing
	mutating func next() {
		switch self {
			case closed: self = opening
			case opening: self = open
			case open : self = closing
			case closing: self = closed
		}
	}
}

//essentially a state machine!

var state = ConnectionState.closed
state.next() —> opening
state.next() —> open
state.next() —> closing
state.next() —> closed
</code></pre>

## Control Flow, Patterns, & Error Handling

### Basic Control Flows, Patterns
<pre><code>let list = [0,1,2,3]

for element in list {
	print (“\(element)”)
}
</code></pre>
if you need indexes:
<pre><code>for i in 0 .. < list.count {
	print(“\(list[i])”)  —> i->list.count-1 times
}

for _ in 1..5 {
	print(“hello”) —> 5 times
}

for ;; {
	print(“hello”) —> forever
}

repeat {

} while condition —> (do while)

// braces required.
if {
} else {
}</code></pre>

you can specify break label to break out of nested statements.
<pre><code>outerLabel: if someCondition {
	innerLabel: if otherCondition {
		if someOtherCondition { break outerLabel }
		if yetAnotherCondition { break innerLabel }
	}
}</code></pre>

#### Switches
Break is default, not needed. Use fallthrough if you want that to occur.
<pre><code>let someItem : Character = “e”
switch someItem {
	case “a”, “e”, “i”, “o”, “u” :
		print(“vowel”)
	case “a”…”z”:
		fallthrough
	default:
		print(“consonant”)
}
</code></pre>
default is <b>mandated</b>.

<pre><code>let aPoint = (1.0, 2.0)

switch aPoint {
	case (let x, 2.0): print (“\(x)”)
	case (1.0, let y): print (“\(y)”)
	case let(x,y) where x>0.0 && y>0.0:
		print(“\(x), \(y)”)
	case let(x,y): print(“\(x), \(y)”)
}
</code></pre>
the last case acts as default but lets us unpack x,y</br>
Also, tuple could be in the switch, not outside.
</br>
<pre><code>// optionals are like enum
enum Status {
	case Okay(status:Int)
	case Error (code: Int, message:String)
	case NA
}

let myStatus = Status.Okay(status:0)
switch myStatus {
	case .NA:				/* */
	case .Okay(0):			/* */
	case .Error(0, _):		/* */
	case .Error(1..<100, _): /* */
	case .Error(let code, let msg):
		print("ERROR \(code): \(msg)")
	
}
</code></pre>

### Error Handling
<pre><code>assert(condition, "Message")
assertionFailure("Message")
</code></pre>
Assert triggers when condition is <b>false</b>, causing app to crash.  Message is printed, exception tossed. </br>
Assert may or may not evaluate based on -O compiler command line switch.</br>
-Onone -> yes </br>
-O -> no </br></br>

<pre><code>precondition(condition, "Message")
preconditionFailure("Message")
fatalError("Message")</code></pre>
Precondition works with all -O flags.</br>
fatalError works similar to precondition. (Different exception is tossed when program terminated.)</br></br>


#### Exceptions
<pre><code>class MyFile {
	enum Error: ErrorType {case NoSuchFile(String), NotOpen}
	
	init( _ path:String ) throws {
		if !MyFile.exists(path) {
			throw Error.NoSuchFile(path)
		}
	}
	
	func readLine() throws -> String {
		if !isOpen { throw Error.NotOpen }
		return "A Line"
	}
	
	var isOpen = false
	class func exists(path:String) -> Bool {return true}
	func close() { /* */ }
	func length()->Int {return 0}
}
</code></pre>
<b>If a method can throw an excption, the call must be tagged with the try keyword!</b>
<pre><code>func doSomething(x: Int?) {
	assert(MyFile.exists("config")
	let aFile = try! MyFile("config")
	defer { aFile.close() }
}
</code></pre>
Code in <b>defer</b> is executed once the block holding the defer statement is closed.  So no matter how we leave the function, defer code will run.</br>
<code><pre>do {
	let theFile = try MyFile("config")
	defer { theFile.close() }
	try theFile.readLine()
	} catch let MyFile.Error.NoSuchFile(path) {
		print("\(path)")
	}
}</code></pre>
A do must have a catch. </br>
- Catches execute in order </br>
- Some catches will not hit if previous ones do.. </br>
- Catch arguement is a <b>pattern</b></br>
- List of catches has to handle <b>every</b> possible exception in a do block!

### Guard
guard -> an if flipped over. </br>
Guard executes else code if something goes wrong, <b>MUST</b> have an else.

<pre><code>guard let x=optX, max=optY where 0 < x && x < max
	else { return }

let optionalReturn = doSomething(x)
guard let o = optionalReturn else {return }
doSomething(o)
</code></pre>

## Functions and Closures

### Functions
<pre><code>func sayHello (first: String, var last: String) -> String {
	return "Hello \(first) \(last)
}</code></pre>
Arguments to functions are <b>constants</b> unless explicitly stated otherwise by var keyword.

<pre><code>func noReturn() { ... }
func noReturn() -> () {...} </code></pre>
Both of the following are valid functions that return nothing.

<pre><code>func takesOptionals( optionalArg:Int?) -> Int? { 
return nil }

if let returnValue = takeOptionals(nil) {
	...
}
</code></pre>
Functions may take optional arguments and return optional values. </br>
Using the if let syntax allows us to call the function and assign its return value to check for nil.

<pre><code>func printName ( first:String, last:String) {
	print ("\(first) \(last)")
}

printName("Wile E.", last: "Coyote")
</code></pre>

In the above call, the <b>last</b> param name is required.

<pre><code>func printName ( given first:String, family last:String) {
	print ("\(first) \(last)")
}

printName("Wile E.", last: "Coyote")
</code></pre>
Now, we have <b>external</b> and <b>internal</b> names for arguments.</br>
- Interal : used inside func </br>
- External : used outside func

If external names are used, they're required in func calls. </br>
By default, functions have <b>wildcards ( _ syntax )</b> for external names, so you don't need them.

#### Function Overloads
<pre><code>func myOverload(x: Int) { ... }
func myOverload(x: Int, y: Int) -> (Int, Int) { ... }
func myOverload(x: Double) -> Double { ... }
func myOverload(x: (Int, Int) ) -> Double { ... }
</code></pre>
Swift supports function overloads, so you may define the function many times.  Compiler decides which to run. </br></br>
Compiler can distinguish func overloads by external names.

#### Functions & Tuples

<pre><code>func findCenter(start:(y:Int,x:Int), _ end:(Int,Int)) -> (y:Int,x:Int) {
	let (xEnd, yEnd) = end;
	let xCenter = start.x + (xEnd - start.y)/2
	let yCenter = start.y + (yEnd-start.x)/2
	return (xCenter, yCenter)
}

let center = findCenter( (1,1), (5,5) )
doSomethingWith ( center.x, center.y )
</code></pre>

If we want to specify the above to be an optional:

<pre><code>func findCenter(start:(y:Int,x:Int), _ end:(Int,Int)) -> (y:Int,x:Int)? {
	let (xEnd, yEnd) = end;
	let xCenter = start.x + (xEnd - start.y)/2
	let yCenter = start.y + (yEnd-start.x)/2
	return (xCenter, yCenter)
}

if let center = findCenter( (1,1), (5,5) ) {
	doSomethingWith ( center.x, center.y )
}

if let (x,y) = findCenter( (1,1), (5,5) ) {
	doSomethingWith ( x, y )
}
</code></pre>
We then use if let syntax to unwrap the value and test for nil. </br></br>
We can also define own variable names in the let.

#### Default Arguments
<pre><code>func concatenate( strings:[String], delimitedBy:String = ", ") -> String {
	var result = ""
	for word in strings {
		result += (word + withSep)
	}
	return result
}

concatenate(["a","b","c"], delimitedBy:"\n")
concatenate(["a","b","c"])</code></pre>
Given the default argument of delimitedBy, we don't have to supply one when calling the function.</br>
<pre><code>func sub( a a:Int = 0, b:Int = 0) -> Int { return b - a }

sub() // 0
sub(a:10) // -10
sub(b:10) // 10
sub(a:20, b:10) // -10
sub(b:10, a:20)</code></pre>
Given explicit names (b is implicit as it is the last argument, touched upon earlier) we can flip the arguments in the func call.

#### Variadic Arguments
<pre><code>func sum (numbers: Int...)->Int {
	var total = 0
	for number in numbers {
		total += number
	}
	return total
}

sum(1,2,3,4)
</code></pre>
sum may have 1+ arguments.
<pre><code>func sum (var total = 0, _ numbers: Int...)->Int {
	var total = 0
	for number in numbers {
		total += number
	}
	return total
}

sum(1, numbers: 2,3,4)	// total = 1, numbers = [2,3,4]
sum( numbers: 2,3,4)	// total = 0, numbers = [2,3,4]
sum( 1,2,3,4)			// total = 1, numbers = [2,3,4]
</code></pre>

#### Inout argument
<pre><code>func swap( inout a:Int, inout _ b: Int) {
	let t = a
	a = b
	b = t
}

var left = "L"
var right = "R"
swap(&left, &right)	// ampersand <b>required</b></code></pre>
<b>& does not mean address operator as it would in C, C++ !!! </b>
It is a tag telling the reader that after swap returns, the values supplied may be changed.
<pre><code>enum Status { case success, failure }

func doSomething( inout result: String) -> Status {
	result = "new value"
	return .success;
}

func doSomething() -> (Status:status, result:String) {
	return (.success, "newValue");
}</code></pre>
Which is better? Call 2. If you want to return two things, <b>return two things</b>.

#### Wrapping Up Function Basics
<pre><code>func sayHello() { print ("hello") }
var talk = sayHello				// implicit type declaration
var talk : ()->() = sayHello	// explicit type declaration
talk()

func speak( talk:()->() ){
	talk()
}
speak( sayHello )
</code></pre>
Functions are <b>first-class objects</b>, just like an Int or a long or an object are! </br>
In the <b>explicit</b> type declaration, we're saying talk is a function that retusn nothing. (Just like the implicit!)</br>
So, <b>names are optional with respect to functions in Swift.</b></br></br>
<b>Speak</b> may seem confusing at first.  It is a function, which rakes in as its argument a function that returns nothing.  Inside, it calls the passed in function, named talk internally (and externally, implicitly)
So calling it, passing in sayHello, prints "hello"!

<pre><code>func moveTowardsZero (value : Int ) -> (Int)->(Int) {
	func up (input: Int ) -> Int { return input + 1 }
	func down (input: Int ) -> Int { return input - 1 }
	return (value < 0 ? up : down)
}

var i = 3
let mover = movetowardsZero(i)

for _ in 1...3 {
	i = mover(i) // 3, 2, 1
}</code></pre>

## Closures and Functional Programming
Object Oriented:	heavyweight, wordy, domain modeling, message passing</br>
Functional: lightweight, powerful, easy to read, easy to maintain, less duplication </br>
<pre><code>func toDouble (x:Int)->Double { return Double ( x) }
let ref = toDouble

//or...declare function and variable at same time!
//Since we have a reference to our function in the below declaration, 
//  we can ditch the function name completely.

// Closure, or Lambda func
let ref = { (x:Int)->Double in return Double( x) }

//can simplify the above with some tricks:
let ref : { ( Int)->Double Double($0) }
</code></pre>

In Swift, you can access func arguments by <b>position</b>: </br>
- $0 : first arg </br>
- $1 : second arg </br>
- and so on...

Can't remove "return" keyword if there's more than one statement in a closure.

<pre><code>func sort ( (String, String)->Bool )
var names = [ "Fred", "Wilma", "Barney", "Betty" ]
names.sort (
	{ (s1:String, s2:String) -> Bool in return s1 < s2 }
)

// since compiler recognizes sort signature, we can simplify the above:
- it knows arg types, arg positions, return type.
names.sort( { $0 < $1 } )
</code></pre>

If the only arg to a function is a <b>closure</b>, we can move the closure outside the argument list entirely:
<pre><code>names.sort() { $0 < $1 }	// trailing closure</code></pre>

<pre><code>func adder(increment : Int) ->(Int)->Int {
	return { increment + $0 }
}

var add = adder(10)
add(20)	// returns 30</code></pre>
Adder returns a closure, which has an argument. Then adds the incremement amount passed into adder to the first (and only) int argument to the closure.</br></br>
So calling adder, we pass the increment value of 10 to the closure and storing it in add.  Then we <b>execute the closure</b> by calling add(20). </br></br>
You would <b>think</b> that after calling adder, the 10 would disappear. However, when adder is called (the factory function), everything visible to the closure is put into a <b>capture object</b>.  That capture object is carried along with the closure when the closure is returned.
<pre><code>class Adder {
	var increment: Int
	
	init(_ increment: Int ) {
		self.increment = increment
	}
	
	func add(value: Int) -> Int {
		return increment + value
	}
}

var theAdder = Adder(10)
theAdder.add(20)	// returns 30
</code></pre>
The above is the object oriented version of the closure example, it makes everything visible.  The adder class is effectively defining a capture.</br>
In both cases, we have an object that contains the increment:</br>
- Objcet Oriented Version - declared object explicitly</br>
- Functional Version - implicitly, but exists nontheless.

<pre><code>func getIncrementers(amount:Int) -> (increment:()->Int,
									 decrement:()->Int) {
	var total = 0
	return ( {total += amount; return total},
			 {total -= amount; return total} )
}

let (up5, down5) = getIncrementers(5)
up5()	// == 5
up5()	// == 10
down5()	// == 5
down5()	// == 0

let (up1,down1) = getIncrementers(1)
up5()	// 5
up1()	// 1
up5()	// 10
up1()	// 2
</code></pre>
As you see above, we create two different calls of getIncrementers. This creates <b>two</b> different capture objects. So, the closures returned from the first call reference the first capture object, and the closures from the second call reference the second capture object.
<pre><code>func getValueFromConfigFile
				(key:String) -> String { ... }

class SomeClass {
	let configItem: String = {
		getValueFromConfigFile("configKey")
	}()
}
</code></pre>
Here we define a closure and call it, and the return value from the call will initialize configItem.</br>
<b>Without the (), we would just be defining the closure and assigning it to configItem</b>

### Map, Filter, Reduce
Three functions so useful they are apart of almost every collection type in Swift.
<pre><code>let letters=["b","c","d"]
letters.map			{ $0.uppercaseString }	// [ "B","C","D"]
letters.filter		{ $0 <= "c" }			// [ "b", "c" ]
letters.reduce("a")	{ $0 + $1 }				// abcd
</code></pre>
#### Map
- Map takes a closure argument. Trailing closure syntax means no closing parenthesis, but they exist implicitly.
- Map calls closure multiple times, one for each array element ($0 arg).
- Returns values into the target array.

#### Filter
- Looks at each array element, decides if it should go into the target array.

#### Reduce
- Condenses the entire object into single object.
- Array elements passed one at a time as the $1 object.
- First call, $0 is 'a'. Second call, $0 is what was returned by first call. ("ab"). And so on.

<pre><code>var names = ["Fred Flintstone", "Wilma Flintstone", "Barney Rubble", "Betty Rubble"]

let result = 
names 	.filter		{ $0.hasSuffix(" Flintstone") }
		.map		{ $0.substringToIndex(advance($0.endIndex,-11)) }
		.reduce("")	{ let sep = $0.characters.count > 0 ? ", ":""
						return "\($0)\(sep)\($1)"
					}
</code></pre>
The above, explained:</br>
- Filter removes all elements that don't end in " Flintstone"</br>
- Map removes the " Flintstone" suffix </br>
- Reduce condenses the remaining into a string, adding a ", " seperator.

As seen above, functional programming gives us <b>power in simplicity</b>.

#### Currying
Haskell Curry: every func with multiple arguments could be represented as a series of func calls where each call has a single argument.
<pre><code>func add (a: Int, b: Int) -> Int {
	return a + b
}

func add2 (a: Int) -> ( b: Int) -> Int {
	return { (b:Int)->Int in return a + b }
}

add2(1)(b:2)	// == 3</code></pre>
Add2 has a single arg, a. It returns a function that has a single arg, b. That func returns the Int.</br></br>
Now, we can clean up add2 by removing things the compiler can infer.</br>Swift also provides a syntactic mechanism to simplify currying even further: </br>
- Remove the arrow between the initial func definition and returned object definition </br>
- Get rid of syntax for inner closure. </br>
- Curried syntax: <b>compiler assumes contents of function is closure that first function returns.</b> </br></br>
So, we are left with the following:
<pre><code>func add2 (a: Int) ( b: Int) -> Int {
	return a + b
}</code></pre>
<pre><code>func appender( delimiter: String ) -> ( String ) -> String {
	var buffer = ""
	return { buffer += $0 + delimiter
				return buffer
			}
}

let append = appender(" ")
append("Hello")	// "Hello"
append("world")	// "Hello world"
append("!")		// "Hello world !"
print ( append("") )</code></pre>
The above doesn't use swift's closure syntax here, because if we did, we can't define the local variable "buffer". This is because, closure syntax means what's in the function definition is the closure that the factory function returns. No way to specify a local variable in the factory function that way. </br></br>
However, we can fix this!
<pre><code>func appender( delimiter: String, var buffer: String = "") ->
										( suffix: String ) -> String {
	buffer += suffix + delimiter
	return buffer
}</code></pre>
By giving the buffer a default value, and allowing it to be an argument, we can remove it from the func definition. </br>
Next, we can remove the clutter urrounding the closure definition. </br>
Finally, we can give the return closure a name to give the $0 a readable name. </br></br>
<b>Swift: All you have is closures.</b> Closures can be assigned to a variable to give it a name. And when you define a function all you do is define the variable and doing the assignment at the same time. So, functions == closures. </br></br>
However, <b>defining a closure as a closure allows you to simplify code.</b>  You can encapsulate a small bit of code into what is a variable in a simple object. You can then pass it around to functions to get other work done.

## Classes
### Subclassing
Subclassing only makes sense when a subclass <b>is a superclass</b> in every sense of the word.
<pre><code>class Person {
	var firstName = "Fred", lastName = "Flintstone"
	var address = "Bedrock, CA"
	var email = "fred@bedrockTileAndQuary.io"
	
	func changeEmailAddress ( email: String ) {
		self.email = email
	}
	
	final func sendEmailTo (subject:String, body: String ) { ... }
}

class Employee: Person {
	let employeeID = 123456789
	
	override func changeEmailAddress(address:String) { ... }
	func changeEmailAddress(name:String, domain:String) {
		email = name + "@" + domain
	}
}</code></pre>

### Properties
Properties are <b>dangerous</b>. Objects in OOP are black boxes, no one using it should have any idea how it works. Makes maintenance a lot easier. </br>
You should be able to <b>completely change</b> a class's implementation without the clients noticing. Throw away everything but the public interface and nobody else in the system should notice.  This is why properties are problematic. </br>
<b>Use computed properties sparingly.</b>
<pre><code>class Person {
	var firstName = "Fred", lastName = "Flintstone"
	var address = "bedrock, CA"
	var fullName: String {
		set {
			var parts = split(newValue, isSeparator:{$0==" "})
			firstName = parts.count > 0 ? parts[0] : ""
			lastName = parts.count > 1 ? parts[1] : ""
		}
		get { precondition(lastName.characters.count > 0)
			return firstName + " " + lastName
		}
	}
	var mailingAddress:String {
		return fullName + "\n" + address
	}
}

var barney = Person()
barney.fullName = "Barney Rubble"
let name = barney.fullName
print("\(barney.mailingAddress)")
</code></pre>
<b>Read-only</b> if you don't specify a set. It will treat what exists as the get clause. </br>
If you provide a set method, <b>must</b> provide a get method as well. Can't have write-only property. </br> </br>
The precondiiton on fullName's getter will cause the program to crash if the last name is empty. <b>This is dangerous! We are violating the no surprises principle</b>.
<pre><code>class Person {
	var firstName = "Fred", lastName = "Flintstone"
	var address = "Bedrock, CA"
	var fullName: String { set { ... } get { ... } }
	var mailingAddress:String { ... }
}
class Employee : Person {
	override var fullName: String { get { ... } set { ... } }
	override var mailingAddress: String { ... }
	override var firstName: String { set { ... } get { ... } }
	override var lastName: String {
		willSet(newVal){ print("\(lastName) -> \(newVal)") }
		didSet(oldVal){ print("\(oldVal) is now \(lastName)") 
			lastName = lastName.uppercaseString
		}
	}
}</code></pre>
When overriding a property with get and set methods, you must provide both in subclass override. </br>
Can also override a simple field to a property.</br></br>
<b>Property observers</b>: Here we've provided an observer at the superclass level. willSet is passed the value just before that value goes into superclass version, didSet is passed the value that used to be there before it is overwritten.
</br></br>Swift documentation says <b>didSet</b> may modify property to change user input in some way. <b>HOWEVER, if you do this in a subclass you get an infinitely recursive loop.</b> It works fine in the superclass though.
<pre><code>class Person {
	var firstName = "Fred"
	var address = "bedrock, CA"
	var fullName: String { set { ... } get { ... } }
	var mailingAddress:String { ... }
	override var lastName: String = "Flintstone" {
		willSet(newVal){ print("\(lastName) -> \(newVal)") }
		didSet(oldVal){ print("\(oldVal) is now \(lastName)") 
			lastName = lastName.uppercaseString
		}
	}
}
</code></pre>
As you can see, you can give an initial value to a property.

### Initializers
<pre><code>class Myclass {
	var x:Int?
	let const:Int = 10
	init() { print("init()") }
}
</code></pre>
Optionals are always initialized to nil if not given an explicit value. </br>
Non-optionals will give a hard compiler error if you attempt to use before initializing. </br>
Constants:</br>
- Initialize in the class <b>OR</b> </br>
- Initialize in all initializers
<pre><code>class MyClass {
	var x:Int?
	let const:Int
	
	init (         ) { const = 10; print ("init()")   }
	init ( _  x:Int) { self.x = x; print("init(_)")   }
	init (ext x:Int) { self.x = x; print("init(ext)" )}
	init (    x:Int) { self.x = x; print("init(x)")   }
	init (    y:Int) { self.x = y; print("init(y)")   }
	deinit           { print("destroying Cls")        }
}

var c1 = MyClass(100)
var c2 = MyClass(ext:200)
var c3 = MyClass(x:300)
var c4 = MyClass(y:400)

var c1 = nil</code></pre>

Our second initializer has an Int argument. Given _ for external name so no label needed for the call. </br></br>
Initializers are different from normal methods: external names are <b>ALWAYS</b> required, even for the first one, unless you explicitly give it an _. Compiler will figure out which you want if you have one with and without external names.</br></br>
if you leave out both the _ and external name, internal name defaults to external. </br>
You can also overload an initializer that differs from another version only by external name. </br></br>
Deinitializers in swift == destuctors in other languages.</br>
Swift is reference counted.  When no active references to an object, deinit is called automatically.  So c1 = nil will call the deinit function. <b>Deinit might not ever be called.</b> So generally a bad idea to clean up an object in a deinitializer, becauses it might never be called. </br></br>

<b>Finally, all initializer must make sure all stored properties of the class are initialized to something.  So either in the declaration or the initializer.</b></br></br>
Common to have one initializer call another to avoid duplicate code.
<pre><code>class Super {
	var d: Double
	init(d: Double) {
		self.d = d
	}
	convenience init(i: Int) {
		self.init(d: Double)
	}
	convenience init() {
		self.init(i: 0)
	}
}

class Sub: Super {
	override init(d: Double) {
		super.init(d: d)
	}
}</code></pre>
<b>Designated Initialized</b>: An initializer with nothing to the left. <b>Cannot chain.</b> </br>
Otherwise, it is a <b>convenience initializer</b>, with keyword <b>convenience</b>.  Basic idea: convenience inits call designated inits. Convenience inits may chain to other convenience inits. Last in chain <b>must</b> chain to the designated init.

#### Subclassing Initializers
Do not have to override a superclass init. Could introduce init of it's own. </br>
<b>Designated init in a subclass must chain to a designated init in the superclass.</b> Convenience inits in a subclass can only chain at the current level. </br></br>

If the subclass has no inits, it inherits all designated inits at the superclass level.</br>
If the subclass overrides every superclass designated init, it inherits all convenience inits. </br>
As such, if a subclass has no inits, it inherits all superclass initializers.</br></br>

#### Initialization Phases
Subclass access is not safe unless superclass is fully initialized. Subclass init() must chain to superclass init() before it can use itself.</br></br>
Init in Swift occurs in phases:</br>
- phase 1: everything above point in which you <b>chain superclass init</b>.</br>
- phase 2: is everything below it.

<b>self is not valid until you've chained to the superclass!!!</b></br> Self may be implicit (property of superclass or subclass) or explicit (self.x)</br></br>
If no chaining call in subclass, for example, a superclass designated init, rule is you are in phase 1 until all fields have been initialized. <b>So, if you're writing a superclass init that wants to call a method and pass self, you must first init all fields.</b>

#### Circular References
<pre><code>class Company {
	var engineering: Department?
	init() {
		engineering = Department(ofCompany:self)
		engineering!.f(self)
	}
	func g() { /* Dangerous */ }
}
class Department {
	unowned let ofCompany : Company
	init( ofCompany: Company ){
		self.ofCompany = ofCompany }
		func f( c: Company ){
			ofCompany.g()
		}
	}
}</code></pre>
Before, we stated all superclass fields must be initialized before using self, but we use it in the init of <b>Company</b>. This is because the var is an <b>optional, which is auto initialized as nil.</b> </br></br>
This is dangerous though, because we init our Department variable in Company init, then call f().  In f, we call g() of Company.  But this occurs before the init() of Company is finished (there may be extra code below the call to f() ), so we may run into uninitialized issues with Company object.

#### Failable Initializers
Returns an optional object.
<pre><code>struct Failable {
	init?(_ x:String) {
		if x.isEmpty {
			return nil
		} // ...
	}
}

if let someF = Failable("hello") {
	/* worked! */
}</code></pre>
Enums implicitly have initializers.  So if the argument passed to the enum doesn't match a raw value, we have a failable init.
<pre><code>enum DistanceUnit: String {
	case Feet = "ft", Meters="m"
}

if let unit = DistanceUnit(rawValue:"ft")
</code></pre>

#### Required Inits
<pre><code>class Super {
	required init() {
		assert(false,"not implemented")
	}
}
class Sub: Super {
	required init() {
		// ...
	}
}
</code></pre>
If you require an initializer at the <b>super</b> level, it is required to override it at the <b>subclass</b> level. </br><b>Required keyword means override keyword isn't necessary</b>

### Access Control
Access associated with <b>files</b>.</br>
> public - anyone can access</br>
> internal - anyone in module/framework/app can access (default)</br>
> private - accessible only from file

Best way to control access: one class per file</br>
> Exception: one class uses an auxiliary class, but no other project members use this auxiliary class.

<b>All fields private!</b></br>
<b>All helper methods private!</b></br></br>
Subclass overrides must be as accessible as superclass versions.</br></br>

An example of a auxiliary class follows:
<pre><code>public class MyClass {
	public func doSomething(){
		let worker = Helper(owner:self)
		worker.helpMe()
	}

	private func access() { /* ... */ }
	private( set )
	public var x: Int {set{ ... } get{return 0} }

	private class Helper {
		private let owner : MyClass
		private init( owner:MyClass ){self.owner = owner}
		private func helpMe() {
			owner.access()
			owner.x = 0
		}
	}
}
</code></pre>
Note the private var above, it has a <b>private</b> setter, declared as such.  Getter is still public.

### Type Coercion, Casting
A superclass reference can access a subclass object, as a subclass object <b>is</b> a superclass object.</br></br>
There are situations, however, where you are passed a subclass object through a superclass reference, and you have to access capabilities defined at subclass level.  We need to <b>cast</b> in this case.
<pre><code>class Super { ... }
class Sub: Super { ... }
var p :Super = Sub()

if p is Sub {
	var s:Sub = p as! Sub
}

if    let s2 = p as? Sub { /* use s2 here */ }
guard let s3 = p as? Sub else { fatalError() }</code></pre>
To make it easy to use the subclass object, we want to access it as a subclass reference.</br>
<b>p as! Sub</b> converts superclass reference -> subclass reference (bang! not needed.)</br>
<b>p as? Sub</b> evals to nil if conversion impossible. if let accesses this. Guard can do same thing, preferred, scope of return reference is accessible outside of the block.

#### AnyObject and Any
Most C-derived languages have void pointers or a reference to a class called Object.  <b>Swift has AnyObject and Any.</b> </br>
AnyObject is more limited, but accessible by Obj-C code.
<pre><code>import Foundation
var obj:Anyobject = Sub()
let a0:[AnyObject] = ["a", [0,1], Sub()]

/* despite all being AnyObjects, we don't know how to handle each type.
  Must unpack accordingly 
 */ 
for x in a0 {
	if let a = x as? String {print("\ (a)")}
	if let b = x as? [Int]  {print("\ (b[0])")}
	if let c = x as? Sub    {print ("Sub")}
}

/* here the !bang treats all of a1 as a String */
let a1:[AnyObject] = ["a", "b", "c"]
for s in a1 as! [String] {
	print(s)
}</pre></code>
Whereas <b>AnyObject</b> must be an object, <b>Any</b> can be anything.
<pre><code>class Customer { var name = "Moe" }
var things: [Any] = [
	0, 42, 0.0, 3.14, "xyz",
	(1,2), Cusstomer(),
	{ (x:Int)->Int in return x }
]

for thing in things {
	switch thing {
		case 0.0		as Double:				print("Double 0.0")
		case			is Double:				print("some double")
		case 0			as Int:					print("Int 0")
		case let i		as Int:					print("\ (i)")			// 42
		case let s		as String:				print("\ (s)")			// xyz
		case let d		as Double where d>0:	print("\ (d)")			// 3.14
		case let (x,y)	as (Int, Int):			print("(\ (x),\ (y))")	// (1, 2)
		case let p		as Customer:			print("\(p.name)")		// Moe
		case let f		as (Int)->Int:			print("\(f(0))")		// abc
		default:								print("???")
	}
}</code></pre>
Here we use the switch to cover all the cases we might expect.  As usual, default is necessary because we do not cover every potential.

### Generics
Useful for defining one version of a method or class that we can use for any type.
<pre><code>func mySwap< T >(inout a:T, inout _ b:T) {
	let tmp=a; a=b; b = tmp
}

var a:Int = 10, b:Int = 20
mySwap( &a, &b )</code></pre>
The below shows a PriorityQueue class with generics for arguments.</br>
When we declare it later with < Person, Int > the compiler handles it automatically.
<pre><code>class Person {}
class Employee : Person {
	func daysSinceLastVacation() -> Int { ... }
}

class PriorityQueue<ItemT, LevelT> {
	func add( item: ItemT, priorityLevel: LevelT ) { ... }
	func getHighestPriorityItem() -> ItemT? { ... }
}

var nextVacation = PriorityQueue<Person,Int>()
func waitForVacation( p: Employee ) {
	nextVacation.add( p, priorityLevel: p.daysSinceLastVacation())
}</code></pre>
Restriction: <b>a generic class cannot contain definitions for other classes or enums or structs!</b> In other words, can't nest a class or struct or enum definition inside a generic class.
<pre><code>enum Bounds <T> {
	case MIN(T)
	case MID(T)
	case MAX(T)
}

let min: Bounds = .MIN(0)	// explicit type declaration
let min = Bounds.MIN(0)		// implicit type declaration
</code></pre>
The compiler can figure out Bounds is an < Int >, so we can leave it out.
### Extensions
Add to an existing class without having to modify existing class.
<pre><code>extension String {
	var length: Int { return self.characters.count }
}

let me = "Allen"
me.length</code></pre>
Extensions don't have to be a class, like subclasses do. See below:
<pre><code>extension Double {
	var m:	Double	{ return self }
	var km:	Double	{ return self * 1000 }
	var mm:	Double	{ return self/1000.0 }
	var ft:	Double	{ return self/3.2808 }
}

let oneMeter 	= 1.0			// 1.0
let oneInch 	= 25.4.mm		// 0.0254
let threeFeet	= 3.ft			// 0.91439
let marathon	= 42.km + 195.m	// 42,195.0
</code></pre>
Here we extend Array so that if the element at index doesn't exist, we return a default value.
<pre><code>extension Array {
	func elementAt(i: Int, defaultsTo:T) ->T {
		if( 0.. < count ~= i ) {
			return self[i]
		}
		return defaultsTo
	}
}
let x = [0, 1, 2]
let y = x.elementAt(3, defaultsTo: 0)</code></pre>
<b>Don't need source for original class/method/value to extend !!! </b>
<pre><code>extension Int {
	func times ( task: ()->() ) {
		for i in 0 .. < self {
			task()
		}
	}
}
3.times { print("hello") }</code></pre>
Restrictions </br>
+ Cannot override method in an extension </br>
+ No desinated initializers. </br>
+ No new cases on an enum. (Can add methods, initializers)

#### === Operator
<pre><code>class MyClass {
var contents = ""
/* ... */
func isEqual( other: MyClass? ) -> Bool {
	guard let 	compareTo =		other else	{ return false } // other is nil
	if			compareTo ===	self		{ return true  } // x.isEqual(x)
	return contents == compareTo.contents
}</code></pre>
argument in isEqual is either MyClass or a subclass of MyClass. Might be nil.

## Memory Management
Swift's memory management system is adopted from Obj-C.
#### Reference Counting
Keep track of objects as they are used. When count gets to 0, object is destroyed.
<pre><code>private class Node<T> {
	var val:	T
	var next:	Node? = nil
	var prev:	Node? = nil
	init(_ val: T){self.val = val}
}

public class List<T> {
	private var head: Node<T>?
	public func clear(){ head = nil }
	public func insert(val: T) {
		let new = Node(val)
		new.next = head		
		head = new
		
		// code added in step 2
		
		var last = head!.next //find last
		while( last != nil ){
			last = last!.next
		}
		last!.next = head
		
	}
}

func test() {
	let list = List<String>()
	list.insert("a")
	list.insert("b")
	list.insert("c")
	list.clear
}
</code></pre>
In a regular linked list, all Nodes have a reference count of 1. If we clear the list, the reference to "a" is decrememented to 0, and then "b", and then "c". </br></br>
However, consider the code above added in step 2. It links the last Node to the first.  <b>Now the first element has 2 references!</b>  So if the head element is discarded, the first element has a reference count of 1.  Since all 3 elements have reference counts of 1, <b>none will be discarded.</b></br></br>  <b>THIS IS A MEMORY LEAK.</b>
<pre><code>public class List<T> {
	private var head: Node<T>?
	public func clear(){ head = nil }
	public func insert(val: T) {
		let new = Node(val)
		new.next = head
		new.previous = nil
		if let first = head {
			first.previous = new
			new.next = first
		}		
		head = new		
	}
}
</code></pre>
In the above doubly linked list, Nodes point to previous and next Nodes. So when we nil out the head pointer, "a" is decremented to 1, and we have another memory leak.
<pre><code>class Committee {
	var members: [Person]=[]
	func join (newMember: Person) {
		members.append(newMember)
	}
}
class Person {
	<b>weak</b> var myCommittee: Committee?
	func join( committee: Committee ){
		myCommittee = committee
		committee.join( self )
	}
}
</code></pre>
<b>The keyword weak here means it will not keep the object it references alive.</b> (It doesn't incremement/decrement the reference counter.)</br>
To use a weak reference:</br>
- Both objects have independent lifetimes </br>
- The reference must be an optional
<pre><code>class Order {
	unowned var placedBy: Customer
	init( placedBy: Customer ) {
		self.placedBy = placedBy
	}
	func asString()->String {
		return "Placed by:\(placedBy)"
	}
}
class Customer {
	var myOrders: [Order] = []
	//...
}</code></pre>
<b>Unowned</b> reference is like a weak reference, in that it will not keep the referenced thing alive. </br></br>
It differs, however: </br>
- Unowned doesn't require objects to have independent lifetimes.</br>
- nil is not a reasonable value for an unowned object.
</br></br>
So, use unowned to handle circular references where the objects have the same lifetime.
<pre><code>class HTMLElement {
	let tag: String
	let content: String?
	init(_ tag:String, content:String) {
		self.tag		= tag
		self.content	= content
	}
	lazy var asHTML: ()->String = {
		[unowned self] in
		return self.content == nil
		? "<\(self.tag) />"
		: "<\(self.tag) >"\(self.content!)"< / \(self.tag) />"

	}
}
let title = HTMLElement("title", content: "Hello")
print( title.asHTML() )</code></pre>
<b>asHTML must be lazy, or you can't use self in the closure body.</b> When initializing a refernece to a closure as part of the declaration, it's as if you did the same thing in an initializer. As we saw in initializers, you can't use <b>self</b> until phase 2.</br></br>
The <b>asHTML</b> property is a reference to a closure. A closure is an object and that object has references in it.  And here, the asHTML function references self, which references the asHTML closure. </br></br>
Enter <b>capture lists</b>. The [unknown self] is a capture list, so the compiler treats the self reference as an unowned reference. <b>So, self can't be nil, and the closure's lifetime is the same as the HTMLElement that creates it.</b> </br></br>
<b>Everytime you have a closure that uses a self reference, you HAVE to have a capture list or you have a memory leak.</b>

## Protocols
Called interfaces in other languages.</br>
A protocol specifies a way in which an adopting class must be implemented.</br>
Can't put enums, classes, or structs in a protocol. </br></br>
If you adopt a protocol, you must provide the method's declared in the protocol.</br>
This includes initializers!
If you do include an init in your protocol, a class that adopts the init must use the keyword <b>required</b>.
<pre><code>enum Format { case XML, JSON }
protocol Representable {
	func representation( asType: Format ) -> String
	init(asType: Format, contents: String )
}

class Employee : Representable {
	private var name: String = "Fred"
	func representation( asType: Format ) -> String {
		switch( asType ) {
			case .XML return	"< employee name=\"\(name)\"/>"
			case .JSON return	"\"employee\":{\"name\":\(name)}"
		}
	}
	
	required init(asType: Format, contents: String) {
		// ...
	}
	init( name: String ){ self.name = name }
}

func doSomething( x: Representable ){
	print("\(x.representation(.XML))")
}

doSomething( Employee("Fred") )</code></pre>
In the above, since we know x is of type Representable, we can use the function declared in the Representable protocol.
<pre><code>protocol Cacheable {
	func flush()
}

class CacheableEmployee: Employee, Cacheable {
	func flush() -> String {
		// ...
	}
}

func doSomething( x: protocol< Representable, Cacheable>){
	print("\ (x.representation(.XML))")
	x.flush()
}
</code></pre>
Now doSomething requires x must adopt both Representable and Cacheable protocols. </br></br>
Notice the class above is a subclass of Employee and implemenets the Cacheable protocol. Some rules: </br>
- Only one superclass allowed </br>
- Class must come before protocols, if it's there </br>
- Can include as many protocols as you'd like.

<pre><code>protocol Cacheable : Representable {
	static var		versionID:	Double { get set }
	var				objectID:	String { get }
	init()
	func			flush		() -> String
	mutating func	load		(flushId: String)
	static func		setTargets(to: NSOutputStream, from:NSInputStream)
}
</code></pre>
Here our protocol extends another protocol. Perfectly valid.  So if something adopts Cacheable, it must also adopt Representable. </br>
Also, we have a static var in Cacheable. So all adopting classes will have their own unique versionID, shared by all instances of the class.</br>
> <b>Mutating</b> is important in the above function definition. If a struct method modifies the struct, it is required.  So by using mutating, we allow structs to adopt the protocol.

<pre><code>class CacheableEmployee: Employee, Cacheable {
	static var versionID 	= 1.2
	static var idPool 		= 0
	let myID 				= ++idPool
	var objectID: String {return "CacheableEmployee" 
							"-\(CacheableEmployee.versionID)"+"-\(myId)" }
	required init() {
		super.init(asType:Format.JSON, contents:"")
	}
	required init(asType: Format.JSON, contents: String) {
		super.init(asType:asType, contents:contents)
	}
	
	func load (flushID: String) { ... }
	func flush ()->String { ... return objectID }
	static func setTargets(to: NSOutputStream, from: NSInputStream) {}
}</code></pre>
So our init is <b>required</b> due to the protocol, and must chain to the superclass initializer. </br>
Also, CacheableEmployee must provide a version of the initializer defined in the superclass, Employee.
> Rules for inheritance with respect to initializers: you only inherit designated initializers if your class doesn't define any initializers at all. 

Notice mutating is missing for the load definition, this is because mutating is not needed in a class.

### Generics and Protocols
Here, T must be an instance of a class that adopts the Cloneable protocol.
<pre><code>class SomeClass<T: Cloneable> {
}</code></pre>
We can also define T to require two protocols.
<pre><code>class SomeOtherClass< T where T: Cloneable, T:Representable> {
}</code></pre>

<pre><code>import Foundation

protocol MyProtocol { func f() }
class AdoptingClass : MyProtocol { func f(){} }
let protocolRef :MyProtocol = AdoptingClass()
let protocolRef = AdoptingClass() as MyProtocol
let anything:Any = AdoptingClass()
if( anything is MyProtocol) {
	...
}

if let implementsProtocol = anything as? MyProtocol {
	...
}

let myProtocolObject = anything as! MyProtocol</code></pre>
As a protocol is, for all intents and purposes, a superclass, the above is valid. </br>  
- The first let means AdoptingClass() must implement MyProtocol at compile time.</br>
- The second let means it happens at runtime. <b>as</b> keyword is a downcast. So the type of protocolRef is MyProtocol. </br>
We could use <b>Any</b> but it is way too flexible.  We'd have to check for the MyProtocol type, as seen above. </br></br></br>

<b>Self</b> in a protocol, is the adopting class.
<pre><code>protocol SupportsReplace {
	func replaceWith(other: Self)
}

class ReplaceableEmployee : Employee, SupportsReplace {
	func replaceWith( other: ReplaceableEmployee ) {
		name = other.name
	}
}

func overwrite(original:ReplaceableEmployee, with:ReplaceablyEmployee){
	original.replaceWith( with )
}</code></pre>
If you attempt to define overwrite as follows:
<pre><code>func overwrite(original: SupportsReplace, with: SupportsReplace) {
	original.replaceWith( with )
}</code></pre>
...you'll get a compiler error.  There is no way to know both arguments are instances of the <b>same</b> class.
<pre><code>func overwrite< T:SupportsReplace>(original: T, with: T) {
	original.replaceWith( with )
}</code></pre>
The above is valid though, as both arguments are guarenteed to have the same type. So, <b>if you want to use a protocol as an argument, you need a generic function.</b>

<pre><code>protocol Cloneable: class {
	func clone() -> Self
}

final class CloneableEmployee: Employee, Cloneable {
	// no inits specified, so we inherit all of them
	
	// valid, but will return the object that receives the message.
	func clone() -> Self {
		return self
	}
	
	// to do this, class <b>must be final</b>
	func clone() -> CloneableEmployee {
		return CloneableEmployee("Fred")
	}
}</code></pre>
The keyword <b>class</b> means the protocol can only be adopted by classes.</br>
To use the 2nd clone, we <b>must declare ClonableEmployee to be final</b>.  We must guarantee the clone method actually returns an instance of the AdoptingClass. Without final, it might return a subclass.

### Generic Protocols
Not supported, but can achieve the same effect.

<pre><code>protocol Container {
	typealias T
	mutating func append(item: T)
}

class Queue : Container {
	typealias T = String
	var data: [String] = []
	func append( item:String ){ data.append(item) }
}

extension Array: Container {}

func allItemsMatch
	< C1:Container, C2:Container where c1.T==C2.T, C1.T:Equatable>
	(first: C1, second: C2) -> Bool {
	/* ... */
}</code></pre>
<b>Typealias T is optional in the adopting class.</b> Compiler understands String in Queue, used in append, substitutes for T. It then substitutes String for T everywhere else T appears.

### Obj-C Protocol
Swift supports Obj-C protocols. Everything in an Obj-C protocol (methods, etc.) must be able to be passed to Obj-C

<pre><code>import Foundation

enum		SwiftEnum		{ ... }
@objc enum	ObjcEnum: Int 	{case X, Y}

protocol	SwiftProtocol	{ ... }
@objc protocol ObjcProtocol	{
	func f (x: Int)
}

class ObjcSubclass: ObjcProtocol {
	@objc func f( x: Int ){}
}

class ObjcSubclass: NSObject, ObjcProtocol {
	func f( x: Int ){}
}
</code></pre>

> Obj-C enums must have an Int rawValue. Can't leave it out, must be Int.

All overrides of Obj-C protocols must be @objc functions.  Annoying, but a workaround exists: </br></br>
If the subclass does not extend another class, use NSObject as the superclass. <b>If NSObject is the superclass, you don't need @objc</b>.
All Obj-C classes extend NSObject (which is available in Swift when importing foundation, which we must do anyway to use @objc tag). </br></br>
Swift protocol can adopt an Obj-C protocol, but not the other way around.</br></br>
What can we put in an Obj-C protocol?

<pre><code>@objc protocol ObjcProtocol {
	func f ( x: Int )					// String, etc.
	func f ( x: AnyObject )				// NO ANY
	func f ( x: ObjcEnum )
	func f ( x: [Int] )					//arrays of Obj-c supported types
	func f ( x: ObjcProtocol )			// pass objects polymorphically, 
										//   (must be obj-c protocol)
	
	func f ( x: ()->() )				// closure (will be obj-c block)
	func f () -> (Int) -> Int			// must have obj-c supported args.
	func >= (left:Int,right:Int)->Bool	// operator overload
	
}</code></pre>

Now, what can we <b>not</b> pass in an Obj-C protocol, but use in Swift?

<pre><code>protocol MyProtocol : ObjcProtocol {
	typealias T					// typealias
	func f ( x: Any )			// Any
	func f ( x: SwiftEnum )		// Swift Enums
	func f ( genericT: T )		// generics
	func f ( optional: Int? )	// optionals
	func f ( x: SwiftProtocol )	// instances of classes that implement Swift protocols
	func f ( inout x: Int )		// inout
	func f ( tuple:(Int,Int) )	// tuples
	func f ( x: Self )			// Self
}</code></pre>
The above rules apply to any function marked with Obj-C tag. Marking a protocol with the tag effectively marks all functions inside with it as well.

#### Swift and Obj-C Protocols: Optional Member
Using Obj-C protocols in Swift allows optional members.

<pre><code>import Foundation
@objc protocol HasOptionalMembers {
	optional var optVar: Int { get }
	optional func optMethod()->Int
	func doSomething()
}

class MyClass: NSObject, HasOptionalMembers {
	func doSomething()->()	{}
}

let opt:HasOptionalMembers = MyClass()
if let result1	= opt.optMethod?()	{ ... }
if let v1 		= opt.optVar			{ ... }
let v2: Int1!	= opt.optVar</code></pre>

As you can see above, the <b>optional</b> keyword allows us to leave them out of a class that adopts the protocol. </br></br>
We then define opt as a reference to the Obj-C protocol, not the actual class.</br>
Similar to optional chaining, we use a <b>?</b> for optMethod, as if it is not implemented it will return nil. </br>
We can use if let syntax to get the optVar, if it was implemented.</br>
Finally, v2 will cause the program to blow up if optVar was not implemented.

### Protocol Extensions

<pre><code>protocol TextRepresentable {
	func asText() -> String
}

class Person {
	...
}

extension Person: TextRepresentable {
	func asText -> String { return "Allen" }
}
</code></pre>
The extension: you can now treat all Persons as if they adopted TextRepresentable.

<pre><code>public protocol MyCollection {
	typealias T
	init( _ args: T... )
	func elements() -> [T]
}
public class IntCollection : MyCollection {
	private var contents : [Int] = []
	public required init( _ args: Int... ){
		for i in args{ 
			contents.append(i) 
		}
	}
	
	public func elements() -> [Int] {
		return contents
	}
}

let obj = IntCollection(1,2,3)
public extension MyCollection where T: SignedIntegerType {
	public func sum() -> T {
		var total: T = 0
		for i in elements() { total += i }
		return total
	}
}</code></pre>
Extending the above protocol gets interesting: many classes may adopt MyCollection and <b>not</b> have a sum method.  Swift allows us to specify a <b>default implementation</b> in the extension.  If the adopting class implements it's own version of sum, it will override the default implementation. </br></br>
Protocol extensions are extremely important: </br>
- Don't need to implement things you don't need on initial implementation. </br>
- No longer add methods in protocols beacuse they might be needed later. </br>
- Don't need fake stub implementations to satisfy protocol requirements. </br>
- Build only what's required.

## Customizing Swift

### Operator Overloads
When the func name is an operator, that func is defining how that operator works given the left and right hand side args to the operator function.
<b>Operator overloads have to be implemented at the global level.</b> So if you extend an operator overload protocol, you implement outside adopting class/extension.

<pre><code>extension Employee: Equatable {}

public func == (lhs:Employee, rhs:Employee) -> Bool {
   return lhs.name == rhs.name
}
</code></pre>

> Equatable is a protocol which requires you to define the == operator function if used.
> If you do use it, Swift creates a != automatically based on the == func overload.

<pre><code>extension Employee: Comparable {}

public func < (lhs:Employee, rhs:Employee) -> Bool {
   return lhs.name < rhs.name
}
public func <= (lhs:Employee, rhs:Employee) -> Bool {
   return lhs.name <= rhs.name
}
public func > (lhs:Employee, rhs:Employee) -> Bool {
   return lhs.name > rhs.name
}
public func >= (lhs:Employee, rhs:Employee) -> Bool {
   return lhs.name >= rhs.name
}</code></pre>
Here we extend Employee with the Comparable protocol. Comparable <b>extends Equatable</b> so we need Equatable if we want to extend Comparable. </br></br>
So why adopt Comparable when we could've just created these funcs on our own? By adopting comparable we add extra functionality, such as sort arrays without added functionality.
<pre><code>var employees = [
      fred,
      barney,
      Employee ( name: "Wilma", payGrade: 3),
      Employee ( name: "Betty", payGrade: 4)
   ]
   
employees.sortInPlace()</code></pre>
The above will sort employees based on the Comparable operator overloads we defined. </br></br>

Now let's create a dictionary where Employees are keys.
To use things as keys, they must be hashable, and they have to adopt Equitable (which we already have above). </br></br>
To adopt Hashable, it requires you define a hashValue Integer. That's all.
<pre><code>extension Employee: Hashable {
   public var hashValue:Int { return name.hashValue }
}</code></pre>

### Extending String
Another class you'll use a lot is String.  Some extensions make sense here:

<pre><code>public extension String {
   public var count : Int { return characters.count }
}

extension String : IntegerLiteralConvertible {
   public init(integerLiteral value: Int) {
      self = "\(value)"
   }
}</code></pre>
Any class that adopts <b>IntegerLiteralConvertible</b> can be initialized by an equal sign followed by an integer. Plenty of other "LiteralConvertible" protocols.

Now, lets make it so we can grab substrings characters from our string with logical ranges:

<pre><code>public extension String {
   public subscript( index: Int ) -> String {
      get {
         return self.substringWithRange(
            Range(start:  self.startIndex.advancedBy(index),
                  end:    self.startIndex.advancedBy(index+1))
         )
      }
   }
   
   public subscript(r:Range<Int>) -> String {
      get {
         return self.substringWithRange(
            Range(start:   self.startIndex.advancedBy(r.startIndex),
                  end:     self.startIndex.advancedBy(r.endIndex))
         )
      }
   }
}</code></pre>
If we want to allow make replacing characters in strings easy, just add set methods to the above like so:

<pre><code> // setter for replacing a character in a String
set {
	return self.replaceRange(
		Range(start:  self.startIndex.advancedBy(index),
       			end:    self.startIndex.advancedBy(index+1)),
      			with: newValue
      	)
}
</code></pre>

### More Class Extensions

If you want to initialize from a String literal, you must adopt StringLiteralConvertible in the class.</br>To do so, we adopt the following 3 initializers in our class, tagged with required convenience:

<pre><code>public class Regex : StringLiteralConvertible {
   private let pattern : String
   private let expression : NSRegularExpression
   private let noOptions = NSRegularExpressionOptions( rawValue:0 )
   
   public required convenience init(
            stringLiteral v: StringLiteralType) {
         try! self.init(v)
   }
   
   public required convenience init(
            extendedGraphemeClusterLiteral v: String) {
         try! self.init(v)
   }
   
   public required convenience init(
            unicodeScalarLiteral v: String) {
         try! self.init(v)
   }
   
   public init(_ pattern: String) throws {
      self.pattern = pattern
      try! expression =
         NSRegularExpression(pattern: pattern, options: noOptions)
   }
   
   public func matches(input: String) -> Bool {
      let result = expression.matchesInString(
         input,
         options: NSMatchingOptions(rawValue: 0),
         range: NSMakeRange(0, input.count)
      )
      
      return result.count > 0
   }
}</code></pre>

The added convenience initializers satisfy the protocol and it's underlying requirements, but are not convenience initializers in those original definitions.  This makes it easy to chain through to our original initializer of the Regex class.</br></br>
If you'd like to use your Class in a switch/case statement, add the following operator overload:
<pre><code>public func ~= (inCase: Regex, inSwitch: String) -> Bool {
   return inCase.matches(inSwitch)
}</code></pre>
Swift uses the ~= under the covers to compare switch arguments to case statements.</br></br>
Now, we can test with the following:

<pre><code>assert( switchTest("012") == .NUM )
assert( switchTest("abc") == .LET )
assert( switchTest("!@*") == .OTHER )

enum MatchingType {
   case NUM, LET, OTHER
}

func switchTest ( template: String ) -> MatchingType {
   switch template {
   case try! Regex("[0-9]+"): return .NUM
   case try! Regex("[a-z]+"): return .LET
   default:
      return .OTHER
   }
}</code></pre>

#### Inventing Operators
> When inventing prefix / postfix operators, can use just about any character except . and =

The following allows us to use ~ as a prefix operator to initialize a Regex.

<pre><code>prefix operator ~ {}

public prefix func ~ ( operand: String) -> Regex {
   do { return try Regex(operand) }
   catch {
      preconditionFailure( "Malformed expression: \(operand)")
   }
}</code></pre>
First, we tell the compiler we introduce a new operator. </br>
Next, we introduce the operator overload function that implements the operation. </br></br>

Now that we have a <b>unary</b> tilda, lets create a <b>binary</b> tilda operator that we can use to match strings against Regex.
<pre><code>infix operator ~ { associativity left precedence 130 }
infix operator !~ { associativity left precedence 130 }</code></pre>
You'll notice a few differences with declaring our prefix operator: </br>
- Associativity left: the operator sits to the left of what it associates with</br>
- Precedence level: All operands have precedence level, as touched upon earlier. ( 130 is the same level as == and != ) </br></br>

Now, lets define the operator overloads.  </br>
> This time, we need not use "infix" in the func header as it is the default.

<pre><code>public func ~ (lhs: Regex, rhs: String) -> Bool {
   return lhs ~= rhs
}

public func ~ (lhs: String, rhs: Regex) -> Bool {
   return rhs ~= lhs
}

public func !~ (lhs: Regex, rhs: String) -> Bool {
   return !(lhs ~= rhs)
}

public func !~ (lhs: String, rhs: Regex) -> Bool {
   return !(rhs ~= lhs)
}</code></pre>
