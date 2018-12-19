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
    * Example: doesn’t print optional(3), just 3
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
    * Example: ‘var isFaceUp’ is a value stored on an individual card, whereas ‘static var identifierFactory’ is only within the struct

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Static%20Example.png" width="375" height="250">

#### Lazy Vars
* Doesn’t initialize until you try to use it
* Used when you’re stuck needing a class or struct loop that’s not initialized

#### Dictionary
* Just an array with a custom identifier
    * Example 1: ‘var emoji = Dictionary<Int,String>()’
    * Example 2: 'var emoji = [Int:String]()'
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
    * 'Stride()'

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
    
<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Closure%20Capture.png" width="725" height="150">



## Lecture 5
**Drawing**

#### Throwing an Error
* Some methods can throw errors
* Can also use optional errors ‘try?’ and it will create an optional of the return value if it is not set (where it fails and says nil)

#### Any and AnyObject
* Special types (it can be any type) – for compatibility with old Objective-C
* Sometimes it’s in a faction’s argument
* You have to convert it to a known type
    * Use ‘as?’ to cast it (usually along with ‘if let’ at the beginning)

#### Casting
* Use ‘as?’ to cast 
* Usually done by casting an object from one of its superclasses down to a subclass (downcasting)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Downcasting.png" width="600" height="250">

#### Interesting Classes
* NSObject
    * The root class of all classes from Objective-C
* NSNumber
    * Generic number-holding class (reference type)
* Date
    * Value type used to find out the date (See also Calendar, DateFormatter, DateComponents, etc.)
* Data
    * Value type (basically a bag of bits)
    * Can be used for json and converting stuff
    
#### Coordinate System 
* CGFloat – always use this for anything UIView coordinates (no doubles/floats)
    * Use conversions ‘let cgf = CGFloat(anExampleDouble)’
* CGPoint
    * X and y
* CGSize
    * Width and height
* Can combine CGPoint and CGSize to make a CGRect

#### Views
* Represents a rectangular area for drawing using coordinates
* It is hierarchical
    * The order of subviews matter since the most recent added thing is on top
    * Usually built in storyboard, but can also be done in code
* Avoid using inits in views, but there are two if needed
    * ‘init(frame:CGRect)’ if the UIView is created in code
    * ‘init(coder:NSCoder)’ if the UIView comes out of a storyboard
* If you need an init, use both inits

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/View%20Init.png" width="600" height="250">

* ‘awakeFromNib()’ is only called if a view is from a storyboard
* Origin is in upper left 
* Units are points, not pixels
    * Depending on the device, a point could be 1, 2 or 3 pixels worth
* Different views have their own coordinate system 
* ‘var bounds: CGRect’ is a views drawing space
* Use frame or center to position a view (never used to draw)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/View%20Rotation.png" width="600" height="250">

* Simple views are usually made in storyboard 
    * After you drag out a generic UIView, go to identity inspector and change it to your custom subclass
* For more complex views, you can create them in code for more flexibility and control

#### Drawing (Core Graphics)
* Only way to draw is using ‘override func draw(_ rect: CGRect)’
* Never call ‘draw(CGRect)’
    * If a view needs to be redrawn, use ‘setNeedsDisplay(_ rect: CGRect)’
* Steps to draw
    * Use ‘UIGraphicsGetCurrentContext’ to get a context to draw into (UIBezierPath does this automatically)
    * Create paths using lines, arcs, jumps, etc.
    * Set attributes like colors, fonts, linewidths, etc.
    * Stroke or fill the created paths
* UIBezierPath uses all the necessary drawing functions
* Example: Draw a triangle (put this code in the 'override func draw' function)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Drawing%20UIBezierPath.png" width="550" height="250">

* Check out documentation for UIBezierPath to use ovals, clipping, hit detection, etc.
* Use UIColor or color literals to set colors
    * To get transparency, use ‘.withAlphaComponent(0.someNumber)’ and let the system know with ‘var opaque = false’
* Use preferred fonts to implement text accessibility options (smaller/larger text in iPhone settings)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Preferred%20Fonts.png" width="450" height="150">

* Init images using ‘let exampleImageName: UIImage? = (UIImage(named: “foo”)’ and draw them using ‘draw.exampleImageName()’ with a bunch of function options
    * Then add foo.jpg to the assets.xcassets file 
* Bounds can change
    * There is a property ‘var contentMode: UIViewContentMode’
        * Check documentation for properties (such as ‘.scaleToFill’ or ‘.redraw’)
    * When not using auto layout, use ‘override func layoutSubviews()’ to manually reposition views (don’t forget super)

## Lecture 6
**Multitouch - Card Game Project Example**

#### Centering Text and implementing text accessibility (generic function)
* Use preferred font and scale function with UIFontMetrics
* Use paragraphStyle to center all the text
* Use ‘traitCollectionDidChange’ to redraw the size of the accessibility text
    * Call 'setNeedsDisplay()' and 'setNeedsLayout'
* This is used to help format the rank and suit text in the corners of the card

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Text%20Accessibility%20Example.png" width="500" height="150">

#### Public vars
* Always use ‘didSet{}’ and call ‘setNeedsDisplay()’ when you need to update (redraw) the view, along with ‘setNeedsLayout()’ if you need subviews to be redrawn too

#### Constants 
* You usually want to segregate constants from the main code
* You can usually create an extension struct to set constants, and computed properties to take any other values and implement the constants

#### Labels
* Every time the bounds change, create the corner labels
* ‘label.numberOfLines = 0’ means to use as many lines needed
* LayoutSubviews redraws the subviews (labels)
* CGAffineTransform can rotate and translate views to make the bottom label upside down

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Labels%20and%20Transform%20Examples.png" width="600" height="250">

#### Auto Layout
* Drag and drop cursor to select views and pick constraints from the menu
* Change layout priority (if you have conflicting constraints)
    * You can change from max (1000) to high (750) or low (250) and the layout will try to satisfy all the restraints to the best of its ability 
        * Example: Trying to make a playing card as big as possible without going off the screen
* Put ‘@IBDesignable’ a line above the class/struct so you can see it displayed in the storyboard (without pressing run)
    * Attach the ‘in: Bundle…’ section of code for compatibility to show images in storyboard and during runtime

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Autolayout%20Card%20Example.png" width="400" height="150">

* Put ‘@IBInspectable’ above a var to have them show up in the storyboard attributes inspector

#### Gestures
* Two steps to use a gesture recognizer
    * Adding a gesture recognizer to a UIView (asking the view to recognize that gesture)
    * Providing a method to handle that gesture
* Every time the recognizer state changes, the handler is called
    * For continuous gestures (e.g. panning), it moves from ‘.began’ through repeated ‘.changed’ to ‘.ended’ states
    * For discrete (e.g. a swipe), it goes strait to ‘.ended’ or ‘.recognized’, but also could go to ‘.failed’ or ‘.cancelled’
* Types of recognizers (Pinch/Rotation/Swipe/Tap/LongPress)

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Recognizers%201.png" width="600" height="250">

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Recognizers%202.png" width="600" height="250">

* Always switch on a state in the handler function
* Example: Swipe through random playing cards
    * Use ‘nextCard’ method to get a rank and suit when swiped left or right
    * Any method that is the action has to be marked ‘@objc’

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/Recognizer%20Example.png" width="400" height="150">

* You can also drag and drop a recognizer from the object library onto a view and link that to code (When someone taps the card it will flip over)
* For scaling the card (pinch gesture), the view must handle it with the appropriate vars and scaling equations
* Reset the scale to 1.0 for reference because pinch is a continuous gesture (lots of small increments)
* Example: Create pinch recognizer

<img src="https://github.com/DennisOrszulak/Stanford-CS193P-Notes/blob/master/Standford%20CS193%20Slide%20Screenshots/VC%20Swipe%20and%20Pinch.png" width="575" height="150">



















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


