# Swift: Final Project
* Name: Nam Pham
* Email: nam.pham@uoit.net

## About the language
### History <br />
Swift was developed by **Chris Lattner** in 2010, in cooperation with other programmers at Apple Inc. The idea of the language was taken from Rust, Objective-C, Ruby, Haskell, C#, CLU, Python and other programming languages. 

Swift was first introduced to the community on September 9, 2014 in Apple Worldwide Developers Conference. The version 1.0 was released on the same day, along with Gold Master of Xcode 6.0 for iOS. Swift 1.1 was introduced October 22, 2014. Since then, Swift has received a lot of considerations among the developer community and perceived as one of the most advanced languages to develop nowadays. 

In spite of being new, Swift was voted as the _Most Loved Programming Language_ according to _Stack Overflow Developer Survey 2015_. <br /> 

### Some interesting features <br />
Similar to C, Swift uses variables to store and refers to values by an identifying name. However, Swift manipulates it better. Swift makes extensive use of constants compared to C or Objective-C. Constants are used throughout Swift to make code safer and clearer. <br />

The difference from Objective-C is that Swift does not require a semicolon at the end of a command (as long as there is no other commands following) <br/>
```swift
print("test!");
print("test!")
// both print: test!
```
Swift also introduces ``optional types``, which handles the absence of a value. Using this functions 
is similar to using ``nil`` with pointers in Objective-C, but it is applicable for any type in Swift. <br />

Swift is a type-safe language, meaning the language is clear at indicating the type of value. If part of the code requires a _String_, type-safety prevents programmer from passing it an _Int_. Type safety helps to catch and fix errors as early as possible in the developement process.  <br />

## About the syntax
### Variable and types 
Using `let` and `var` to declare a constant and a variable repsectively. <br />
```swift
let <name> = <value>
var <name> = <value>
```
While `let`  must be assigned with a value, `var` needs not. Besides, unicode can also be assigned with a value.
```swift 
let π = 3.14159 
let 🐶🐮 = "dogcow"
var red, green, blue: Double
```
Automatically the type of the variable will be inferred. However, it can also be declared when initializing. <br />

The syntax is: ``var <name>: <type>``
```swift
var red = 10 // Int 
var red: Double //Double 
```
Syntax for a comment is: ``//``, ``/* ... */`` <br />

Swift a case sensitive language. Therefore, variables ``Man`` and ``man`` are different. <br />
### Whitespaces 
Whitespaces are not required, however, they are must be equal if applied.
```swift
int fruit = apples +oranges    // wrong statement
int fruit = apples + oranges   // correct statement
```
### Optionals
When a value may be absent, **optionals** is used: ``var <name>: <type>?``
```swift
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
```
### Tuples
Swift also supports **tuples**.
```swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```
A tuple can be decomposed, and part of the tubple can be omitted (by using an underscore _ ):
```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"

let (statusCode, _) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
```
Tuple's components can also be accessed by using index:
```swift
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
```
### Ranges
A range in Swift is defined as: ``(a...b)``, ``(a..<b)`` or ``[..a]``, ``[a..]``<br />
### Functions
Swift requires programmer to be clear about the return type when declaring a function. <br /> 

Syntax: ``func <name>(*parameter*) -> <return type> {*body*}``
```swift
func sayHelloWorld() -> String {
    return "hello, world"
}
print(sayHelloWorld())
// Prints "hello, world"
```
Function is quite dynamic in Swift. A function can take another function as a parameter, have multiple return types (or zero). _Optinals_ can be used as a return type <br />
```swift
// A function with no return value
func greet(person: String) {
        print("Hello, \(person)!")
    }

// A function takes another function as parameter
func printAndCount(string: String) -> Int {
    print(string)
    return string.count
}
func printWithoutCounting(string: String) {
    let _ = printAndCount(string: string)
}

// A function has multiple return types
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}

// A function with optonals return type
func minMax(array: [Int]) -> (min: Int, max: Int)? { *same as above* } 
// This will return nil when the array is empty
```
Arguments of function in Swift can be labeled or omitted. <br />

Syntax to label a parameter: ``func <name>(label <paratmeter>: <type>) {}`` <br />
Syntax to omit parameter: ``func <name>(_ <paratmeter>: <type>) {}``<br />
```swift
func greet(person: String, hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}

//normal call
greet(person: "John", hometown: "Canada") 

//label 
func greet(who person: String, from hometown: String) -> String { (same as above) }

greet(who: "John", from: "Canada")

//omit
func greet(_ person: String, _ hometown: String) -> String { (same as above) }

greet("John", "Canada")
```
## About the tools
### Compiler
Swift complier contains these phases: <br />
#### Frontend Compiler
* __Parser__: ([lib/Parse](https://github.com/apple/swift/tree/master/lib/Parse)) takes the products from _Lexical Anlysis_ phase (convert everything into words and tokens). Parser is responsible for generating an _Abstract Syntax Tree (AST)_, then identifying the roles, group such products together so that the codes make sense. 
* __Semantic Analyser__: ([lib/Sema](https://github.com/apple/swift/tree/master/lib/Sema)) is responsible for taking the parsed AST and transforming it into a well-formed, fully-type-checked form of the AST. It can also do some programme bindings. 
* __Clang importer__: ([lib/ClangImporter](https://github.com/apple/swift/tree/master/lib/ClangImporter)) imports [Clang modules](http://clang.llvm.org/docs/Modules.html) and maps the C or Objective-C APIs they export into their corresponding Swift APIs. The resulting imported ASTs can be reffered to by semantic analysis.
#### Backend Compiler
* __SIL generation__: The Swift Intermediate Language (SIL) is a high-level, Swift-specific intermediate language suitable for further analysis and optimization of Swift code. The phase (implemented in [lib/SILGen](https://github.com/apple/swift/tree/master/lib/SILGen)) lowers the type-checked AST into so-called "raw" SIL. The design of SIL is described in [docs/SIL.rst](https://github.com/apple/swift/blob/master/docs/SIL.rst).
* __SIL guaranteed transformation__: ([lib/SILOptimizer/Mandatory](https://github.com/apple/swift/tree/master/lib/SILOptimizer/Mandatory)) perform additional dataflow diagnostics that affect the correctness of a program (such as a use of uninitialized variables). The end result of these transformations is “canonical” SIL. 
* __SIL Optimizations__: ([lib/Analysis](https://github.com/apple/swift/tree/master/lib/SILOptimizer/Analysis), [lib/ARC](https://github.com/apple/swift/tree/master/lib/SILOptimizer/ARC), [lib/LoopTransforms](https://github.com/apple/swift/tree/master/lib/SILOptimizer/LoopTransforms) and [lib/Transforms](https://github.com/apple/swift/tree/master/lib/SILOptimizer/Transforms)) perform additional high-level, Swift-specific optimizations to the program, including (for example) Automatic Reference Counting optimizations, devirtualization, and generic specialization.
* __LLVM IR Generation__: Intermediate Representation (IR) generation ([lib/IRGen](https://github.com/apple/swift/tree/master/lib/IRGen)) lowers SIL to LLVM IR, at which point LLVM can continue to optimize it and generate machine code.
### Create a project 
In order to create a Swift project, __XCode__ and __the REPL__ are required. Example on how to install _repl_ and _create a project_ can be retrieved [here](http://www.aidanf.net/learn-swift/running_code).

## About standard library
Standard library of Swift can be devided into:
* __Standard library core__: ([stdlib/public/core](https://github.com/apple/swift/tree/master/stdlib/public/core)) includes the definitions of all of the data types, protocols, functions, etc.
* __Runtime__: ([stdlib/public/runtime](https://github.com/apple/swift/tree/master/stdlib/public/runtime)) is a layer between the copmiler and the core standard library. It is reponsible for implementing many of the dynamic features of the language, such as casting (such as _as!_ and _as?_ operators), type metadata (to support generics and reflection), and memory management (object allocation, reference counting, etc.). The runtime is written mostly in C++ or (where needed for interoperability) Objective-C.
* __SDK Overlays__: ([stdlib/public/SDK](https://github.com/apple/swift/tree/master/stdlib/public/SDK)) provide Swift-specific additions and modifications to existing Objective-C frameworks to improve their mapping into Swift. In particular, the _Foundation_ overlay provides additional support for interoperability with Objective-C code.
### Examples about Standard Library Core
#### Closure Expression
__Closure Expression__ is a shorter version of function-like constructs without a full declaration and name. This is a way to write inline closures in a brief, focused syntax. Closure expressions provide several syntax optimizations for writing closures in a shortened form without loss or clarity or intent. <br /> 

Syntax: ``{ (parameters) -> (return type) in (statements) }`` <br />

Example below illustrates Closure Expression by breaking down the function using `sorted(by:)` method:  
```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

//normal thinking
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}

var reversedNames = names.sorted(by: backward)
//return [Ewa, Daniella, Chris, Barry, Alex]

//Closure expression
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
//also return [Ewa, Daniella, Chris, Barry, Alex]
```
__Shorthand Arguments__ used to refer to the values of closures' arguments by the signatures `$0, $1, $2` and so on. <br />
```swift
reversedNames = names.sorted(by: { $0 > $1 } )
//easier to read and understand
```
Notice that the `in` keyword can also be omitted when using shorthand arguments. <br />
Example: 
```swift
var add = { (arg1: Int, arg2: Int) -> Int in
    return arg1 + arg2
}
add = { (arg1, arg2) -> Int in
    return arg1 + arg2
}
add = { arg1, arg2 in
    arg1 + arg2
}
add = {
    $0 + $1
}

let result = add(20, 20) // 40
```
_Shorthand closure expression_ is very useful in terms of readibility and efficiency. <br />
#### Filter, Reduce, Map, Regular Expression

__Filter__: loops over a collection and returns the value that matches the condition(s).
```swift
let digits = [1,4,10,15]
let even = digits.filter { $0 % 2 == 0 }
// [4, 10]
```
__Map__: loops over a collection and appies the function on each element. Map returns an array containing the results.
```swift
let peopleArray = [ Person(name:"Santosh", address: "Pune, India", age:34, income: 100000.0, cars:["i20","Swift VXI"]),
             Person(name: "John", address:"New York, US", age: 23, income: 150000.0, cars:["Crita", "Swift VXI"]),
             Person(name:"Amit", address:"Nagpure, India", age:17, income: 200000.0, cars:Array())]

var name: [String] = Array()
let cars = peopleArray.map({ $0.cars })
print(cars)
// Result: [["i20", "Swift VXI"], ["Crita", "Swift VXI"], []]
```
__flatMap__: same as _map_ but returns only one array contaning the concatenated results and will ignore _nil_ values (pay attention to the difference in the result).
```swift
let flatCars = peopleArray.flatMap({ $0.cars })
print("Flatmap: \(flatCars)")
// Result: Flatmap: ["i20", "Swift VXI", "Crita", "Swift VXI"]
```
__reduce(initialResult, nextPartialRestul)__: returns the result of combining the elements of the sequence using the given closure.
```swift
let numbers = [1, 2, 3, 4]
let numberSum = numbers.reduce(0, { $0 + $1 })
// numberSum == 10
```
__Regular Expression (regex)__: Swift supports regex by applying method [NSRegularExpression](https://developer.apple.com/documentation/foundation/nsregularexpression), and it is a bit complicated to use. <br />
Example:
```swift
func matches(for regex: String, in text: String) -> [String] {
    do {
        let regex = try NSRegularExpression(pattern: regex)
        let results = regex.matches(in: text,
                                range: NSRange(text.startIndex..., in: text))
        let finalResult = results.map {
            String(text[Range($0.range, in: text)!])
        }
        return finalResult
    } catch let error {
        print("invalid regex: \(error.localizedDescription)")
        return []
       }
    }
    
    
let regex = "(#/{0,1}\\d{1,}#\\*{0,2})"
// Mutable string because replaceMatches method on regex takes NSMutableString as an input
var value: NSMutableString = "#1#**lot of sales#/1#* the money and cards #2#Rober Ambra#/2#**."

let allMatches = matches(for: regex, in: value as String)
// Will print
//- 0 : "#1#**"
//- 1 : "#/1#*"
//- 2 : "#2#"
//- 3 : "#/2#**"
```
### About open source library
Swift is welcome any contribution from the community through the [open discussion site](https://forums.swift.org/c/evolution/discuss). <br /> 

There is a [proposal site](https://forums.swift.org/c/evolution/proposal-reviews) where every proposal will be evaluated by both the inventers and the programmer community. <br />

One of the latest contributions to the Standard Library is by _Ben Cohen_ in _Remove Some Customization Points from the Standard Library's Collection Hierarchy_ (retrieved [here](https://github.com/apple/swift-evolution/blob/master/proposals/0232-remove-customization-points.md)). 

### Specialized library

There are tens of useful libraries for programmers to work with Swift: from working with UI to manipulate the dataset (retrieved [here](https://github.com/Wolg/awesome-swift))<br />

One of which is the library to work with JSON named SwiftyJSON: https://github.com/SwiftyJSON/SwiftyJSON <br />

## Analysis of the language
### Programming Style
As discussed above about what features the **Standard Library** supports, Swift is a __functional__ programming language. Function is highly recommended when programming in Swift in order to avoid mutability and divide the task into readable and traceable blocks. 
* __Immutability__: Swift allows programmers to create a constant. This helps a function whose parameters are constant will be **free of side-effect**. The function, therefore, would not alter any elements outside its scope. 
* __Value type__: pretty much everything within the Standard Library is struct. This means whenever a value is passed to struct, and when struct is used to set other objects, the value is affected directly inside that struct/object instead of reference types. Example:
```swift
var box = CGRect.zero
var square = box.size
box.size.height = 10
// square: width: 0, height: 0
// box.size: width: 0, height: 10
```
If _CGRect_ and _CGSize_ are reference types:
```swift
box.size.height = 10
// square: width: 0, height: 10
// box.size: width: 0, height: 10
```
* __Function__: This includes:
__Pure function__: a function that its return value is only determined by the input without any observable side-effects. It does only one thing: compute the return value. 
```swift
func sum(_ a: Int, _ b: Int) -> Int { 
    return a + b 
}
```
**First-class function**: functions can be assigned to variables.
```swift
func sayHello() {
    print("Hi!")
}
let greeting = sayHello
greeting() //print "Hi!"
```
**High-order function**: a function that satisfies either one of two conditions: 
* _Use a function as an argument._
* _Return another function._
```swift
func inside() -> Void { 
    print("Yo!")
}
func outside(inner: () -> Void) { 
    inner()
}
outside(inside)
//prints: Yo!
```
### Meta-programming
Swift supports meta-programming with [**Sourcery**](https://github.com/krzysztofzablocki/Sourcery)<br />

Syntax: `$ ./sourcery <source> <templates> <output>`

One of the recognizable features of meta-programming is the ability to copy and paste code scientifically. <br />

Here are some basic examples available on GitHub: 
```swift
struct Car {
  
  let model: String
  let numberOfSeats: Int
  let color: UIColor
  
}
```
We may want to compare our `Car` struct in various places, therefore, we extent it to conform the _Equatable_ protocol:
```swift
extension Car : Equatable {
  
  func ==(lhs: Car, rhs: Car) -> Bool {
    return lhs.model == rhs.model &&
        lhs.numberOfSeats == rhs.numberOfSeats &&
        lhs.color == rhs.color
  } 
}
```
Finally, we can write a template with [Stencil](https://github.com/stencilproject/Stencil): 
```swift
{% for type in types.structs %}
extension {{ type.name }} : Equatable {}
func ==(lhs: {{ type.name }}, rhs: {{ type.name }}) -> Bool
{
	{% for var in type.variables %}
	guard lhs.{{ var.name }} == rhs.{{ var.name }} else { return false }
	{% endfor %}
	return true
}

{% endfor %}
```
It is time now to use `sourcery` to apply the _template_ created on the file _Car.swift_. This is the result: 
```swift
extension Car : Equatable {}
func ==(lhs: Car, rhs: Car) -> Bool
{
	guard lhs.model == rhs.model else { return false }
	guard lhs.numberOfSeats == rhs.numberOfSeats else { return false }
	guard lhs.color == rhs.color else { return false }
	return true
}
```
### Symbol Resolution and Closure
As mentioned above, Swift is quite flexible regarding symbol resolution (**Syntax** examples) and closure (**Standard Library** examples). <br />

Besides allowing programmers to apply Unicode when naming a vairable or constant, Swift also allows programmers to do the same with reserved keyword by surrounding the variable/constant with backticks (\`). However, it is recommended to not use such names unless there is an absolute reason to do so. <br />

### Scoping rules
There are two types of scopes in Swift: _top-level scope_ or _global scope_ and _local or nested scope_. <br />
* __Global scope__: By default, any variable declaration (including constants etc.) will be positioned at the _top-level scope_. This means it is accessible from code in any source file within the same module. Using _global scope_ is considered bad practice, because any change in the _global scope_ can lead to unexpected effects in an unrelated part of an application. This is the resouce of bugs that is hard to find and fix. 
* __Local/nested scope__: Local scope are subsets of global scope with boundaries. Any object, function or method etc. will form a local scope, so does code block. This means any declaration within the local scope can only be accessed from the that scope. 
<br /> 

Example: 
```swift
let three = 3 // global scope by default
print(three) 
func outerFunction() { 
    var two = 2 // local declaration inside outerFunction
    print(two) // works because inside the scope
    print(three) // accessible as of global variable
    if true {
        var one = 1 // local declaration in the code block if-statement
        print(one) // works 
        print(two) // nested scope of outerFunction
        print(three) // the top-level declaration
    }
    // print(one) - Error. "one" is not accessible from outer if-statement's scope. 
}
// print(two) - Error. "two" is not accessible from outside of outerFunction's scope.

outerFunction()
```
In a simple word, it can be understood as: "three" is the 1st-level scope, "two" is the 2nd-level scope inside outerFunction, and "one" is the innermost-scope inside if-statement in the outerFunction. 1st-level can be called from **anywhere**, 2nd-level can only be called anywhere **inside** the outerFunction, and 3rd-level can only be called inside its if-statement block code. <br />

Another example: 
```swift
let x = 10
print("x outside myFunc equals \(x)") 
func myFunc() {
   let x = 20
   print("x within myFunc equals: \(x)")
}

myFunc()
print("x outside myFunc equals:\(x)")

//result
//10
//20
//10
```
This is called **shadowing**. The same declaration for variable x can have two differents value because they belong to different scopes. While the first `let x = 10` is a global variable, `let x = 20` belongs to `myFunc()`'s scope and only functions under the value of 20 inside `myFunc()`. Once the scope is terminated, `x` goes back to its default value (= 10). <br />

**Namespace** plays an important role in differing scopes. Two items with same name but different values will cause en error if they are located in the same namespace. 
```swift
var x = 4
var x = 6 // error
```
An error is thrown because the variable `x = 4` has been declared by default in the top-level scope, _user_ namespace, and has been reserved a place in the memory. Declaring another variable `x = 6` with the same name, in the same namespace and scope, will "confuse" the compiler to decide which value to choose. 
### System type: Static and Dynamic
Swift is believed static because Compiler has the ability to detect error at the _compile time_. <br />

Furthermore, as shown in many examples before, Swift is a strongly, statically typed language. This means Swift does not accept coercion on the fly, as well as all variables, constants, functions etc. must be declared in advance, or memory is not accessible after it is deallocated, etc. This is for the sake of memory safety that Swift wants to prevent unsafe behviors which could happen in the code.
```swift
let label = "The width is "
let x = 4
let width = label + x // error because label is of String type and x is of Integer type.
let width = label + String(x) // The width is 4 -> Because both constants have the same String type.
```
An example of _namespace_ in the previous section is a clear proof of this trait: `var x = 4` and `var x = 6` will raise an error because the memory has been allocated for `x = 4`.  <br />

However, there are moments Swift performs as a dynamically typed language, for example, when assigning a value for a variable. It is not required to scecify the type of the variable, and the compiler will infer its type automatically later. Example: `var x = 4`, x will be referred to Int type. <br />

Briefly, since Swift is functional programming language, and declaring types of arguments is strictly required, Swift is considered to be "more" static than dynamic. 

### Strengths and Weaknesses
#### Strengths:
1. **Readibility**: even though being developed on the Objective-C platform, Swift offers programmers a cleaner syntax. This includes dropping semicolon at the end of lines or parantheses.
2. **Fast**: speed must be borne in mind as one of the most important keys of Swift. As [tested by Apple](https://www.apple.com/swift/) Swift is 2.6x faster than Objective-C and 8.4x than Python. 
3. **Safety and Performance**: In order for the code to be readable, Swift requires programmers to follow its strongly typed format. This means, since everything must be declared in advance, Swift can minimalize a number of unexpected errors. Besides, Swift's error handling helps prevent code crashes and errors in production. Moreoever, Swift has a shorter feedback loop, which allows programmers to see the errors in the code instantly and fix them on the fly.
4. **Open source**: Acknowledging the imperfect of the language, Swift developers welcome contributions from the community and an abundance of third-party tools to make it complete. This means programmers are flexible to decide either **static** or **dynamic** libraries to choose when coding. Such combination helps decrease the memory storage and boost up the speed. 
5. **Automatic Memory Counting (ARC)**: ARC is the techonology aimed to add a garbage collector function. This keeps track of information such as relationship between the code, instances, then dealloactes those stored memories if they are no longer in use. This both decreases the memory footprint and adds up to 20% to CPU. 
6. **Interoperability**: Since developed on the Objective-C platform, Swift is perfectly compatible with Objective-C and can be used interchangeably within the same project.  
5. **Full stack potential**: Voted as the most loved programming language (2015), the potential of Swift at full stack developing is huge. [IBM has also successfully pushed](https://developer.ibm.com/swift/) the language into cloud-server. Moreover, Swift has expanded its support to not only iOS devices but also Linux-based system. 
#### Weaknesses:
1. **Age**: The language is quite young, therefore, issues are unavoidable. It takes time for developers to complete it. Additionally, the amount of "native" libraries and tools are limited compared to other well-known languages, because many of them got outdated when there is a new release. 
2. **Unstability**: As mentioned, once a new release is launched, old tools become useless. This makes Swift unstable in terms of determining its target. Even though the problems have been configured in Swift 4.0, some third-libraries still have not been updated yet. This means these changes must be fixed manually. It will cause a big problem if a project is (too) large. 
3. **Community**: Swift is not having as many talents devoting in it as in other languages, such as C, Java, Python etc. ([StackOverFlow developer survey](https://insights.stackoverflow.com/survey/2018)).
4. **Poor interoperability and third-party Integrated Development Environment (IDE)**: As mentioned above, it is hard to find the right tools to work with the certain tasks at the moment. In addition to that, the official Apple IDE, XCode, is often reported with issues such as syntax highlighting, autocomplete, refactoring tools, and compilers. 
5. **Lack of support for earlier iOS version**: Because the language was announced in 2014, and despite its interoperabilbity with Objective-C, Swift only supports iOS version 7.0 and later. However, this will not be serious problem since only less than 5% of Apple devices running on iOS 6. or earlier (source: [david-smith](https://david-smith.org/iosversionstats/)).
![image](https://www.altexsoft.com/media/2017/06/ios-versions.png)
