# Swift: Final Project
* Name: Nam Pham
* Email: nam.pham@uoit.net

## About the language
### History <br />
Swift was developed by **Chris Lattner** in 2010, in cooperation with other programmers at Apple Inc. The idea of the language was taken from Rust, Objective-C, Ruby, Haskell, C#, CLU, Python and other programming languages. 

Swift was first introduced to the community on September 9, 2014 in Apple Worldwide Developers Conference. The version 1.0 was released on the same day, along with Gold Master of Xcode 6.0 for iOS. Swift 1.1 was introduced October 22, 2014. Since then, Swift has received a lot of considerations among the developer community and perceived as one of the most advanced languages to develop nowadays. 

Though being a latest programming language, Swift was voted as the _Most Loved Programming Language_ according to _Stack Overflow Developer Survey 2015_. The success of the language has also drawn the attention from Google that they consider to deploy to language to develop their Android devices. <br /> 

### Some interesting features <br />
Similar to C, Swift uses variables to store and refer to values by an identifying name. Howeverr, Swift manipulates it better. Swift makes extensive use of constants compared to C or Objective-C. Constants are used throughout Swift to make code safer and clearer. <br />

Even thought it is based on C and Objective-C, Swift does not require a semicolon at the end of a command (as long as there is no other commands following) <br/>
```swift
print("test!");
print("test!")
// both print: test!
```
Swift also introduces ``optional types``, which handle the absence of a value. Using this functions 
is similar to using ``nil`` with pointers in Objective-C, but it is applicable for any type in Swift. <br />

Swift is a type-safe language, which means the language is clear in indicating which type of value you are working with. 
If part of the code requires a _String_, type-safety prevents you from passing it an _Int_. Type safety helps you catch and fix errors as early as possible in the developement process.  <br />

## About the syntax
### Variable and types 
Using _let_ and _var_ to declare a constant and a variable repsectively. <br />
```swift
let <name> = <value>
var <name> = <value>
```
_let_ must be assigned with a value while _var_ needs not. Unicode can also be used.
```swift 
let π = 3.14159
var red, green, blue: Double
```
Automatically the type of the variable will be inferred. However, it can be declared when initializing. The syntax is: <br /> 
``var <name>:<type>``
```swift
var red = 10 // Int 
var red: Double //Double 
```
Syntax for a comment is: ``//``, ``/* ... */`` <br />
Swift a case sensitive language. Therefore, variable ``Man`` and ``man`` are different. <br />
### Whitespaces <br />
Whitespaces are not required, however, they are must be equal if applied.
```swift
int fruit = apples +oranges    //is a wrong statement
int fruit = apples + oranges   //is a Correct statement
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
Swift also supports **tuples**
```swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```
A tuple can be decomposed, and part of the tubple can be omitted (by using an underscore _ ):
```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"

let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404"
```
It can also be accessed by using index:
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
func greet(person: String) 
    {
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
Syntax to label parameter: ``func <name>(label <paratmeter>: <type>) {}`` <br />
Syntax to omit parameter: ``func <name>(_ <paratmeter>: <type>) {}``<br />
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
In order to create a Swift project, __XCode__ and __the REPL__ are required. More information on how to install _repl_ and _create a project_ can be retrieved [here](http://www.aidanf.net/learn-swift/running_code).

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
__Shorthand Arguments__ used to refer to the values of closures' arguments by the names `$0, $1, $2` and so on. <br />
```swift
reversedNames = names.sorted(by: { $0 > $1 } )
//easier to read and understand
```
Notice that the `in` keyword can also be omitted when using shorthand arguments, because closure expression is made up entirely of its body. <br />
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
__Regular Expression (regex)__: Swift supports regex by applying method [NSRegularExpression](https://developer.apple.com/documentation/foundation/nsregularexpression). <br />
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
var value: NSMutableString = "We are big now #1#**lot of sales#/1#* the money and cards #2#Rober Langdon and Ambra Vidal#/2#**."

let allMatches = matches(for: regex, in: value as String)
// Will print
//- 0 : "#1#**"
//- 1 : "#/1#*"
//- 2 : "#2#"
//- 3 : "#/2#**"
```
