# Stanford CS193P Notes
Quick notes taken for Stanford's CS193P iTunes U Course (Fall 2017)

## Table of Contents
* [Lecture 1](#lecture-1)
    * Intro to iOS 11, Xcode 9, and Swift 4
* [Lecture 2](#lecture-2)
    * MVC
* [Lecture 3 and 4](#lecture-3-and-4)
    * The Swift Programming Language
* [Lecture 5](#lecture-5)
    * Drawing
* [Lecture 6](#lecture-6)
    * Multitouch
* [Lecture 7](#lecture-7)
    * Multiple MVC's, Timer, and Animation
* [Lecture 9](#lecture-9)
    * View Controller Lifecycle and Scroll View
* [Lecture 10](#lecture-10)
    * Multithreading
* [Lecture 11](#lecture-11)
    * Drag and Drop, UITableView, and UICollectionView
* [Lecture 15](#lecture-11)
    * Alerts, Notifications, Application Lifecycle      

## Lecture 1
**Intro to iOS 1, Xcode 9, and Swift 4**

#### Basic Xcode controls and using properties/Interface
* Split Screen (Storyboard and swift file)
* Identity and attributes inspector
* Compiler errors and warnings
    
#### Interface builder
* Drag and drop objects in storyboard and ctrl-drag to link to code (creates @IBAction/@IBOutlet/@OutletCollection)
* Outlet Collection is an array of a UI object (such as buttons)
* Watch out for copy pasting objects – It keeps existing links to functions in swift file
* Hover over circles on the line numbers for functions to see where it’s linked on storyboard
* Command-Click -> rename to rename things in code and storyboard (or it will be disconnected)
    
#### Documentation
* Hold option and click on code to see apple documentation (Recommended to read overviews to help understand common classes)
    
#### Initializing
* All instance variables (properties in Swift) have to be initialized
* Use init to set variables or set it equal to something
    
#### Swift Type Inference
* Swift is strongly typed, but Swift can guess which type (except UI objects)
    
#### Property Observer
* Every time some variable changes, execute code in ‘didSet{}’ (such as updating text in a label)
    
#### Optionals?
* Can be in a set or not set state
* When set, it will have an associated value (such as int, string, bool, etc.)
* Nil means an optional is not set
* ! is assuming the optional is set and grab the associated value 
* Ex: doesn’t print optional(3), just 3
* If the optional is nil, the app crashes
* Find bugs easily by using ! on optionals (if you want to)
    
## Lecture 2
**MVC**

#### Basics of MVC
* Model = What the application is (but not how it is displayed)
* Controller = How the model is presented to the user (UI logic)	
* View = The controller’s generic minions (UILabels, UIButtons, etc.)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/MVC.png" width="425" height="250">


#### Struct vs Class
* Almost the same, but structs have no inheritance 
* Structs are value types = It gets copied when used (pass it as an argument, assign it to a variable, put it in array)
* Classes are reference types = Lives in the heap, has pointers. When passing around a class, it just assigns a pointer to the class (can have multiple pointers to the same class)

#### Model to Controller
* Use model in the controller by basically creating the green arrow (from MVC picture)
* One way: Create a new var in view controller and assign it to the model class

#### Class Initializers 
* Classes can get a free init with no arguments as long as all their vars in that class are initialized
* Structs – the free init initializes all of its vars, but can have a huge list of arguments to initialize
* Use ‘self.’ to use distinguish between the same internal and external name on the initializer (or any other method, but usually on inits)

#### Statics
* Vars or funcs are stored with the type, not individual instances of the struct
* Ex: ‘var isFaceUp’ is a value stored on an individual card, whereas ‘static var identifierFactory’ is only within the struct

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Static%20Example.png" width="375" height="250">

#### Lazy Vars
* Doesn’t initialize until you try to use it
* Used when you’re stuck needing a class or struct loop that’s not initialized

#### Dictionary
* Just an array with a custom identifier
* Example: ‘var emoji = Dictionary<Int,String>()’
* Example 2 (Same thing): var emoji = [Int:String]()
* An empty dictionary that maps an int to a string
* Looking up something in a dictionary returns an optional (since it might not be in the dictionary)

#### Checking an optional - If statement simplification
* Check if the optional is set and do something, if not, do something else
* Example: The if statement in the picture is the same as the last return statement

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Optional%20Example.png" width="300" height="150">

#### Random Numbers
* Only works with unsigned int and returns UInt32 (usually needs to be converted)
* Arc4random_uniform(upperbound limit)

#### Converting Types
* Create a new thing and pass the number using the specific initializer 
* Example: UInt32(something.count)
* Converts the int .count to a UInt32 value




## Lecture 3 and 4
**Swift Programming Language**

#### Stack view
* Grouped in horizontal or vertical (can be stacked multiple times to make a grid or something similar)
* Use standard spacing when possible
* Ctrl-drag object to top/bottom/sides of the view to select constraint relationship

#### Countable Range
* Create a countable range with floats/doubles 
* Stride()

#### Tuples
* Group values together
* Example: Let x: (Name1: String, Name2: Int, Name3: Double) = (“Hello”, 5, 0.85)
* Can rename these or change values also
* A function can return the tuple as a group of values (such as height and weight)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Tuples.png" width="650" height="150">

#### Computed Properties
* A value can be computed rather than stored
* If you only want a read only property – just use get
* Usually these are used when you want to keep values in sync or when something is derived from a state in the program

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Computed%20Properties.png" width="450" height="150">

#### Access Control
* Usually for large programming projects (multiple files and developers)
* Keywords (put in front of vars and funcs)
    * Internal – default, usable by anything in my app or framework
    * Private – only callable from within the object
    * Private(set) – setting a var is private, but getting a var is possible outside the object
    * Fileprivate – usable by any code in the source file
    * Public (frameworks only) – can be used by objects outside my framework
    * Open (frameworks only) – public and they can subclass/override it
* It’s suggested to make things private until you know what vars and funcs that other things can call and use

#### Asserts
* Lets app crash and displays a message if there is an error
* Example: If something calls a method at index 100 but there are only 12 indices

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Asserts%20Example.png" width="575" height="150">

#### Extensions
* Ability to add vars and funcs to other any other classes (even if you don’t have a source
* Restriction - No storage (but can use computed)
* Problems
    * Easily abused – don’t add a var or func that doesn’t make sense for that class (obfuscation)
    * Requires architectural commitment to organize code
* Best used (for beginners) for small, well-contained helper functions
* Good semantics – don’t let it crash when called
* When in doubt, don’t do it
* Example: Extend int to give a random number when called

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Extension%20Example.png" width="575" height="250">

#### Enums
* Value type (like a struct) – copied as it is passed around
* Only uses discrete values
* Simple data structure
* Each case can have associated data or values (kind of like tuples)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Enums.png" width="600" height="250">

* Can use type inference on one side of the equals sign while setting the value of an enum
* Can use a switch statement to check the enum state
* Must handle all possible cases in the switch statement
    * Use ‘break’ instead of print (in the example) to skip that case
    * Use ‘default:’ to handle all the other cases if you don’t want to write them out
* Can use multiple lines of code, and doesn’t move on to the next case - no fall through by default (use the ‘fallthrough’ keyword)
* Associated data is accessed through a switch using the ‘let’ syntax
    * Can also rename the local variables to print
* Can have methods and computed properties but no stored values
* If you want to reassign ‘self’ to another value in a func, you must have ‘mutating’ because enum is a value type (all value types need to know when a value can change, such as struct)

#### Optionals
* An optional is just a special enum with 2 cases (nil, and some associated data of a certain type)
* ? declares an optional
* ! force unwraps the associated data (could crash app if its nil)
    * Safe way is using ‘if let’ to check if it is set
* ?? defaults to a value if an optional is not set
* ? can also be used for optional chaining
    * If anything is nil, it just bails out of the sequence and returns nil
    * Example: If x, foo(), and bar are optionals

#### Memory Management
* Automatic Reference Counting (Not garbage collection)
* Reference types are stored in the heap
* Every time you create a pointer to a reference type, Swift keeps track of it, and when there are zero references, they get tossed out
* Strong
    * Default, not typed out in the code
* Weak 
    * If nothing is interested in it, set it to nil
    * Will never keep an object in the heap
    * Only works with optional pointers to reference types
    * Usually on outlets (since those are optionals like UILabel!) and delegates
* Unowned
    * Very rare, because it’s like trying to outsmart the ARC
    * The programmer has to know not to access it when it’s not in the heap
    * Use it to avoid a memory cycle – 2 pointers linked only to each other in the heap, so they both stay in the heap for no reason

#### Data Structures
* Essential building concepts – class, struct, enum, protocol
* Class
    * Reference type
    * Single inheritance of both functionality and data (instance variables)
    * The heap is automatically kept clean by Swift
* Struct
    * Value type (structs don’t live in the heap and are passed around by copying them)
    * “Copy on write” behavior, so it requires you to mark ‘mutating’ methods
    * No inheritance of data
    * Examples of common structs: Array, Dictionary, String, Character, Int, Double
* Enum
    * Value type
    * Used for variables that have one of a discrete set of values
    * Each option can have associated data with it
    * Can have methods and computed properties
* Protocol
    * A protocol is a type (just like class, struct, enum)
    * Just a list of vars and funcs – no data storage
    * A way to express an API better
        * More flexible and expressive
        * Better blind and structured communication between view and controller
        * Mandating behavior
        * Sharing functionality between types
    * Basically provides multiple inheritance of functionality (not storage)
    * Aspects to a protocol
        * Declaration (which properties and methods are in it)
        * A class, struct, or enum declaration that makes the claim to implement the protocol
        * The code in said class, struct or enum that implements the protocol
    * Normally, the implementer must implement all the methods/properties, but marking a protocol ‘@objc’ and using ‘optional’ methods, you can use the old objective C code that allows you to skip some implementation (not to be confused with the type Optional)
    * Any number of protocols can be implemented by a given class, struct or enum
    * In a class, inits must be marked ‘required’ (or the subclass might not conform) 
    * Can add protocol conformance via an extension too
    
<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Protocol%20Declaration.png" width="600" height="150">

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Protocol%20Implementation.png" width="750" height="150">
    
<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Protocol%20Example.png" width="550" height="250">

#### Delegation
* Very important use of protocols
* Multiple Inheritance functionality
    * Example: Arrays, Dictionaries, CountableRanges (for loops), and Strings implement the protocols Sequence and Collection, because they are sequences and therefore a collection of things – that’s why you can use ‘index(of:)’
    
<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Delegation.png" width="725" height="250">

#### Strings
* Value type (it’s a struct)
* Collection of characters (more specifically Unicodes)
* The index of a string cannot be an int
    * The problem: The string “café” might have 4 Unicodes (with é) or 5 Unicodes (with a regular e and another to put an accent on it)
* Simplest ways to get an index are ‘startIndex’, ‘endIndex’, and ‘index(of:)’
* To move to another index, use ‘index(String.Index, offsetBy: Int)’
* Use ‘.insert’ or ‘+’ to modify or add on to strings

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Strings.png" width="675" height="250">


#### NSAttributedString
* Not a string, it’s a class (reference type)
* Uses a dictionary of attributes attached each character or a whole string (such as UIColor or UIFont)
* Can put NSAttributedString on UILabels, UIButtons, or drawing on screen
* Look up dictionary keys to set different values in the Apple documentation

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Attributed%20Strings.png" width="600" height="250">


#### Function Types
* Functions are types
* You can declare a variable, parameters to a method, etc. to be a type “function”

#### Closures
* Reference type
* Use a closure (an in-line function) to be as simple as possible

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Closure%20Example.png" width="400" height="100">

* Using ‘.map’ (takes a function as an argument and applies it to each element) with a closure

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Closure%20Map.png" width="600" height="150">

* You can execute a closure to do initialization of a property
* Useful with ‘lazy’ because the last () means it will execute the initialized right when it gets called

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Closure%20Init.png" width="375" height="100">

* Using a closure that captures variables from surrounding code could create a memory cycle
    * If you capture a class that arrayOfOperations is in, this closure is pointing to the class, and that class is pointing to the closure (use unowned to break it)
    
<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Closure%20Capture.png" width="700" height="150">



## Lecture 5
**Drawing**

## Lecture 6
**Multitouch**

## Lecture 7
**Multiple MVC's, Timer, and Animation

## Lecture 8
**View Controller Lifecycle and Scroll View**

## Lecture 9
**View Controller Lifecycle and Scroll View**

## Lecture 10
**Multithreading**

## Lecture 11
**Drag and Drop, UITableView, and UICollectionView**

## Lecture 15
**Alerts, Notifications, Application Lifecycle** 


