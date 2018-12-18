# Stanford CS193P Notes
Quick notes taken for Stanford's CS193P iTunes U Course

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

#### Random Numbers
* Only works with unsigned int and returns UInt32 (usually needs to be converted)
* Arc4random_uniform(upperbound limit)

#### Converting Types
* Create a new thing and pass the number using the specific initializer 
* Example: UInt32(something.count)
* Converts the int .count to a UInt32 value




## Lecture 3 and 4
**Swift Programming Language**

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


