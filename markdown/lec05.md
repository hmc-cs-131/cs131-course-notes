### CS 131: Programming Languages

# Haskell Data Types, Pattern Matching, Type Classes


## Warm-up Problem: Working with Shapes
In this warm-up problem, we aim to write a program that can manipulate different shapes, such as circles, squares, and right triangles. To achieve this, we need to establish a way to encode these shapes. Each shape will require a base point, which represents the X and Y coordinates on the plane (e.g., the center of a circle or the bottom-left corner of other shapes). Additionally, we will need specific dimensions to define each shape, such as the radius of a circle, the side lengths of a square, or the height and width of a right triangle.

### Goals
Our program should be able to accomplish the following tasks for each shape:
1. Compute the **area** of the shape.
2. **Shift** the shape's position in the plane by providing a delta X and delta Y.

### Object-Oriented Approach
Consider the problem from an object-oriented perspective. How would you represent or encode a circle, square, and right triangle using object-oriented thinking? Furthermore, how would you implement the methods for shifting and computing the area of these shapes? Take a moment to sketch a solution.

### Discussion: Share Your Thoughts
Now that you've had some time to think about the object-oriented approach to working with shapes, I encourage you to discuss your ideas with others. Once you've finished discussing shapes, take a moment to share how your weekend went. Let us know how you're doing!

## Warm-up Problem Solution

### Object-Oriented Approach
In the warm-up problem, we explored how to work with shapes using an object-oriented approach. Let's recap the solution and highlight the important components.

#### Shape Class
The base class, `Shape`, represents the common attributes and behaviors of all shapes. It includes the X and Y coordinates to define the position of the shape. The class provides two essential methods:
```java
public abstract double area();
public void shift(double deltaX, double deltaY);
```
The `area` method is declared as abstract since it needs to be implemented in each shape subclass. The `shift` method adjusts the X and Y coordinates by a given delta X and delta Y.

```java
abstract class Shape {
  double x, y;
  
  public abstract double area();
  
  public void shift(double deltaX, double deltaY) {
    x += deltaX;
    y += deltaY;
  }
}
```

#### Circle Class
The `Circle` class extends the `Shape` class and introduces a `radius` attribute. It overrides the `area` method to calculate the area specific to circles.

```java
class Circle extends Shape {
  double radius;
  
  public double area() {
    return Math.PI * radius * radius;
  }
}
```

#### Square Class
Similar to the `Circle` class, the `Square` class inherits from `Shape` and adds a `side length` attribute. It overrides the `area` method to calculate the area of squares.

```java
class Square extends Shape {
  double side;
  
  public double area() {
    return side * side;
  }
}
```

#### Right Triangle Class
The `RightTriangle` class also extends `Shape` and includes side lengths for the triangle. It overrides the `area` method to compute the area of right triangles.

```java
class RightTriangle extends Shape {
  double base, height;
  
  public double area() {
    return base * height / 2;
  }
}
```

### Functional Approach in Haskell
Now, let's explore the functional approach to solving the shape manipulation problem using Haskell. Although we won't delve into the specific syntax at this moment, we'll give you a high-level overview of the solution.

In Haskell, we can define shapes using the `data` keyword, which allows us to create custom data types. Here's an example of how we can encode shapes in Haskell:
```haskell
data Shape = Circle Double | Square Double | RightTriangle Double Double
```
In this representation:
- `Circle`, `Square`, and `RightTriangle` are *constructors* that create instances of the `Shape` data type.
- Each constructor is associated with specific values, such as the radius for circles, side length for squares, and side lengths for right triangles.

To perform computations on these shapes, we can define functions that pattern match on the shape constructors. Here's an example of the `area` function in Haskell:
```haskell
area :: Shape -> Double
area (Circle radius) = pi * radius * radius
area (Square sideLength) = sideLength * sideLength
area (RightTriangle baseHeight height) = 0.5 * baseHeight * height
```
In this function:
- The `area` function takes a `Shape` as input and returns a `Double`.
- Using pattern matching, we differentiate between the different shape constructors and calculate the respective areas accordingly.

Similarly, we can define the `shift` function in Haskell:
```haskell
shift :: Shape -> Double -> Double -> Shape


shift (Circle radius) deltaX deltaY = Circle (radius + deltaX) (radius + deltaY)
shift (Square sideLength) deltaX deltaY = Square (sideLength + deltaX) (sideLength + deltaY)
shift (RightTriangle baseHeight height) deltaX deltaY = RightTriangle (baseHeight + deltaX) (height + deltaY)
```
The `shift` function takes a `Shape`, along with delta X and delta Y values, and returns a modified shape with the shifted position.

### Functional Programming vs. Object-Oriented Programming
It's important to note the differences between the object-oriented and functional approaches to solving problems. While the object-oriented approach relies on classes and inheritance to model objects and their behaviors, the functional approach focuses on using data types and functions that operate on those types.

In object-oriented programming, shapes are objects that know how to perform different operations on themselves. In functional programming, functions know how to compute over different data types. The shift function in Haskell knows how to compute a shifted shape (circle, square, or right triangle), while the area function knows how to compute the area for each shape.

## Simple Data Types

In Haskell, we can create our own custom data types to represent values and define their types. Let's explore how to create and work with data types in Haskell.

### Data Types

Data types are used to define categories of values and provide a way to organize and structure data in a program. By creating our own data types, we can represent and manipulate domain-specific concepts in a more expressive and meaningful way.

### Type Names in Haskell

Before we dive into creating custom types, let's recall an important point we discussed earlier. In Haskell, all type names are written in uppercase letters. Although not everything written in uppercase is a type name, it's essential to follow this convention when defining our own types.

### Creating a New Type

To create a new type, we use the `data` keyword followed by the type name and its possible values. Each value is separated by the pipe character (`|`). Let's look at an example:

```haskell
data CoinFlip = Heads | Tails
```

In this example:
- `CoinFlip` is the type name, written in uppercase.
- `Heads` and `Tails` are the possible values of the `CoinFlip` type.

### Working with Values of Custom Types

To interact with values of a custom type, we can assign them to variables and examine their types. For example, with the `CoinFlip` type:

```haskell
data CoinFlip = Heads | Tails

:t Heads
-- Output: Heads :: CoinFlip

x = Tails
:t x
-- Output: x :: CoinFlip
```

The examples above demonstrate that `Heads` and `Tails` are both values of type `CoinFlip`.

### Creating Types with Multiple Values

We can create types with multiple values by extending the previous approach. Let's consider an example using playing card suits:

```haskell
data CardSuit = Clubs | Diamonds | Hearts | Spades
```

In this case, `Clubs`, `Diamonds`, `Hearts`, and `Spades` are all values of type `CardSuit`.

### Formatting and Syntax

The formatting and syntax for creating custom types may vary, but it's a matter of personal preference and code readability. For example, we can choose to put each value on a separate line:

```haskell
data CardSuit =
    Clubs
  | Diamonds
  | Hearts
  | Spades
```

The spacing and newlines are a matter of aesthetics and do not affect the semantics. The important aspect is using the `data` keyword followed by the type name and its possible values.

### Coin Flip and the `Bool` Type

The `CoinFlip` example we discussed earlier is similar to how Haskell defines the built-in `Bool` type. `Bool` has two values: `True` and `False`. Just like we created the `CoinFlip` type, Haskell already defines the `Bool` type with its values.

### Displaying Custom Type Values

When we try to display or print values of custom types, we may encounter an error in GHCi. For example, attempting to print `Heads` directly may result in an error message:

```
No instance for (Show CoinFlip) arising from a use of `print`
```

To resolve this issue, we need to derive the `Show` type class for our custom type. By adding `deriving Show` at the end of the type declaration, we enable printing and displaying values of the type.

Let's see an example with the `CoinFlip` type:

```haskell
data CoinFlip = Heads | Tails
  deriving Show
```

Now,

 we can display the values of `CoinFlip`:

```haskell
Heads
-- Output: Heads

x = Tails
x
-- Output: Tails
```

The `deriving Show` clause allows us to visualize the values of custom types when interacting with them in GHCi.

## Functions and Simple Data Types

In this lecture, we will explore functions and simple data types in Haskell. We will focus on a specific example of creating a data type called `thermostat setting`, which has three possibilities: `off`, `cooling`, and `heating`. Our goal is to create a function called `isRunning` that determines whether the system is running based on the given `thermostat setting`.

### Defining `isRunning` Function

#### Style 1: Pattern Matching on Function Arguments

One way to define the `isRunning` function is by using pattern matching on the function arguments. We can declare the function type and list the possibilities with corresponding evaluations:

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning Off = False
isRunning Cooling = True
isRunning Heating = True
```

This style demonstrates the functional approach, where the function knows how to handle different values of the `ThermostatSetting` data type.

#### Style 2: Pattern Matching inside a Case Expression

Another approach is to use pattern matching inside a case expression within the function body. The function type declaration remains the same, and we match the `setting` parameter against the possibilities:

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning setting = case setting of
  Off -> False
  Cooling -> True
  Heating -> True
```

This style achieves the same result as the previous one but organizes the code differently.

#### Style 3: Pattern Matching with a Wildcard

We can also use pattern matching with a wildcard to catch all cases except the explicitly defined ones. The wildcard is represented by an underscore (`_`):

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning Off = False
isRunning _ = True
```

Here, we specify the behavior for `Off`, and for any other value, we evaluate to `True`.

#### Style 4: Pattern Matching in a Case Expression with a Wildcard

A combination of the previous styles involves pattern matching in a case expression with a wildcard. We still have the `setting` parameter and match against cases:

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning setting = case setting of
  Off -> False
  _ -> True
```

This approach allows us to handle specific cases and catch any other value.

#### Style 5: If-Then-Else Expression

We can attempt to use an if-then-else expression in the function body, but it requires additional steps. However, it may not work directly without informing Haskell about the equality comparison for the `ThermostatSetting` type.

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning setting = if setting == Off then False else True
```

To make this work, we need to inform Haskell about the equality comparison, which we will cover in future videos.

#### Style 6: Simplifying with Inequality Comparison

Building upon the previous styles, we can simplify the code by using inequality comparison (`/=`) with the `Off` value:

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning setting = setting /= Off
```

This one-liner checks if the `setting` value is different from `Off` and evaluates to `True`. It covers all cases except `Off`.

#### Style 7: Using a Curried Function

Lastly, we can treat the inequality comparison as a curried function and define `isRunning` accordingly:

```haskell
isRunning :: ThermostatSetting -> Bool
isRunning = (/= Off)
```

Here, we directly assign the function without explicitly mentioning the `

setting` parameter. This style takes advantage of treating binary operators as functions and utilizing currying.

### Exploring Different Styles

Now that we have seen different styles of writing the `isRunning` function, let's delve into some questions to gain a better understanding:

1. **Preference and Applicability:** Is there a particular style you prefer for this problem? Are there situations where one style may be better or worse than another?

2. **Readability, Writability, and Maintainability:** How do these styles compare in terms of readability, writability (ease of writing), and maintainability (ease of maintaining and modifying code)? Do these factors depend on your level of experience with Haskell?

3. **Identifying Implementations:** If you were given the `isRunning` function without knowing the specific implementation, would you be able to distinguish between the different styles just by running the function?

Take some time to reflect on these questions and explore the similarities and differences between the styles. Understanding these nuances will help you become more comfortable and confident in writing functions for different data types in Haskell.

These various styles of writing the `isRunning` function demonstrate the flexibility and expressiveness of Haskell. By considering the design choices and trade-offs, you can make informed decisions while writing your own Haskell code.

## Data Types and Associated Values

Data types in programming languages allow us to define and work with structured data. In Haskell, we can create custom data types to represent entities and their associated values. Let's explore the concept of data types and associated values using examples.

### Simple Examples of Data Types

In simple examples, data types have a finite list of possible values. For instance:

- A coin flip can have two values: heads or tails.
- A card suit can have four values: clubs, diamonds, hearts, or spades.
- A thermostat setting can have three values: off, cooling, or heating.

However, these simple examples may not be sufficient to express more complex types that we might want to work with.

### Creating Data Types with Associated Values

To create data types with associated values in Haskell, we can define a new type and specify its possible values. Let's consider an example of a thermostat setting.

```haskell
data ThermostatSetting = Off | CoolTo Int | HeatTo Int | OutOfService String
  deriving (Show, Eq)
```

In this example, we have defined the `ThermostatSetting` data type, which can have the following values:

- `Off`: Represents the thermostat being turned off.
- `CoolTo Int`: Represents cooling the system to a particular temperature, indicated by an integer.
- `HeatTo Int`: Represents heating the system to a particular temperature, indicated by an integer.
- `OutOfService String`: Represents the system being out of service, with an associated message explaining the reason.

We have also derived the `Show` and `Eq` type classes for the `ThermostatSetting` data type, allowing us to print values and perform equality comparisons.

### Understanding the Associated Values

Let's take a closer look at the associated values of the `ThermostatSetting` data type.

- `Off` is a value of type `ThermostatSetting` and has no associated value.
- `CoolTo` is a function value that takes an integer (temperature) and returns a `ThermostatSetting` value.
- `HeatTo` is similar to `CoolTo`, but represents heating the system to a particular temperature.
- `OutOfService` is a function that takes a string (message) and returns a `ThermostatSetting` value.

### Working with Data Types and Associated Values

Now that we have defined the `ThermostatSetting` data type, let's explore how we can work with it.

```haskell
setting1 = Off
-- The type of `setting1` is `ThermostatSetting`.

setting2 = CoolTo 20
-- The type of `setting2` is `ThermostatSetting`.

-- Trying to print `CoolTo` without applying enough arguments will result in an error.
-- Haskell doesn't know how to print functions automatically.
-- We need to provide sufficient arguments to create a value.
```

By creating values of the `ThermostatSetting` data type, we can manipulate the associated values and observe their types. It is important to provide the necessary arguments to functions like `CoolTo` and `HeatTo` to create valid values.

### Syntax for Creating Data Types

The general syntax for creating data types in Haskell follows this pattern:

```haskell
data TypeName = Constructor1 [AssociatedType1] | Constructor2 [AssociatedType2] | ...
```

- `TypeName`: Represents the name of the data type.
- `Constructor1`, `Constructor2`, etc.: Represent the names of the constructors associated with the data type.
- `[AssociatedType1]`, `[AssociatedType2]`, etc.: Represent the associated types for each constructor (can be zero

 or more).

### Deriving Type Classes

We can optionally specify that a data type should derive certain type classes. Type classes define a set of behaviors that types can support. In the example, we derived the `Show` and `Eq` type classes for the `ThermostatSetting` data type.

### Connection to Formal Grammars

The syntax used to create data types in Haskell resembles the notation used in formal grammars. If you have studied formal grammars or taken a course like CS 81, you might find similarities in the syntax. This connection is not a coincidence and has meaningful implications, which we will explore later.

## Data Types, Associated Values, and Functions

### Pattern Matching on Function Arguments

Pattern matching is a powerful technique in Haskell that allows us to destructure data and perform computations based on its structure. We can use pattern matching on function arguments to handle different cases based on the values passed in. By pattern matching on data types with associated values, we can write functions that work specifically with those values.

### Example: The `isRunning` Function

Let's consider an example function called `isRunning` that takes in an integer (temperature) and a thermostat setting and returns a boolean value indicating whether the system is running or not. We will define the function using pattern matching on the thermostat setting.

```haskell
isRunning :: Int -> ThermostatSetting -> Bool
isRunning _ Off = False
isRunning _ (OutOfService _) = False
isRunning temp (CoolTo t) = temp > t
isRunning temp (HeatTo t) = temp < t
```

In this example, we have different cases defined for the pattern matching. Each case handles a specific value or constructor of the `ThermostatSetting` data type and performs the necessary computation based on the associated values.

- The first case `_ Off` matches when the thermostat setting is `Off`. In this case, the function returns `False` since the system is not running.
- The second case `OutOfService _` matches when the thermostat setting is `OutOfService` with any corresponding message. Again, the function returns `False`.
- The third case `CoolTo t` matches when the thermostat setting is `CoolTo` with a specific temperature value `t`. If the current temperature `temp` is greater than `t`, the system is not running, so the function returns `False`. Otherwise, it returns `True`.
- The fourth case `HeatTo t` is similar to the `CoolTo` case, but it checks if the current temperature `temp` is less than `t` to determine if the system is running.

### Understanding the Pattern Matching

In the `isRunning` function, we are pattern matching on the constructors of the `ThermostatSetting` data type as well as the integer parameter `temp`. The underscores `_` indicate that we are not using those values in the respective cases. We only need the `temp` value in the cases where we perform the temperature comparison.

### Simplifying the Function with Wildcards

We can simplify the `isRunning` function by using wildcards for the unused variables. In the first two cases, we don't need the `temp` variable, so we can replace it with an underscore `_`. Similarly, in the second case, we don't need the `message` variable.

```haskell
isRunning :: Int -> ThermostatSetting -> Bool
isRunning _ Off = False
isRunning _ (OutOfService _) = False
isRunning temp (CoolTo t) = temp > t
isRunning temp (HeatTo t) = temp < t
```

By using wildcards, we indicate that we are not interested in those particular values and can ignore them in the pattern matching.

### Exploring Alternative Function Syntax

There are different ways to write functions in Haskell, and you may explore other syntax options, such as using case expressions. However, in this lecture, we focused on using pattern matching on function arguments.

## Recursive Data Types with Lists

Recursive data types in Haskell allow us to define complex data structures that can include references to objects of the same type within themselves. One quintessential example of a recursive data type is a list. We can define a list in Haskell using the keyword `data` and the recursive structure of a list can be expressed as follows:

```haskell
data List a = Empty | Cons a (List a)
```

In this definition, a list is either an empty list (`Empty`) or a value `a` followed by another list (`Cons a (List a)`). The type parameter `a` allows us to create lists of any type.

For example, we can create lists of integers (`Int`) using this definition:

```haskell
type IntList = List Int
```

### Creating Lists

Once we have defined the recursive data type for lists, we can create lists using the constructors `Empty` and `Cons`. Here are some examples:

```haskell
let emptyList = Empty  -- An empty list
let list1 = Cons 10 emptyList  -- A list with a single element: 10
let list2 = Cons 5 (Cons 8 emptyList)  -- A list with two elements: 5, 8
let list3 = Cons 3 (Cons 6 (Cons 9 emptyList))  -- A list with three elements: 3, 6, 9
```

### Recursive Functions on Lists

Once we have defined a data type, we can write functions that operate on that data type using recursion. Recursive functions allow us to process lists efficiently and elegantly. Let's explore some recursive functions on lists.

#### Computing the Length of a List

To compute the length of a list, we can write a recursive function that counts the number of elements in the list. The length of an empty list is 0, and the length of a non-empty list is 1 plus the length of the rest of the list.

```haskell
listLength :: List a -> Int
listLength Empty = 0
listLength (Cons _ rest) = 1 + listLength rest
```

Here, we pattern match on the constructors of the `List` data type to handle the different cases. The function recursively computes the length of the rest of the list and adds 1 for the current element.

#### Accessing the Head and Tail of a List

We can also define functions to access the head (first element) and tail (remaining elements) of a list. The head of an empty list is undefined since there is no first element, and the head of a non-empty list is simply the value stored in the first element. The tail of an empty list is also undefined, and the tail of a non-empty list is the rest of the elements.

```haskell
listHead :: List a -> a
listHead Empty = undefined
listHead (Cons x _) = x

listTail :: List a -> List a
listTail Empty = undefined
listTail (Cons _ rest) = rest
```

In these functions, we pattern match on the constructors of the `List` data type to handle the different cases. The head function extracts the value stored in the first element, and the tail function returns the rest of the elements.

#### Mapping a Function to All Elements of a List

We can define a function that applies a given function to all elements of a list. This allows us to transform the values stored in the list while maintaining the list structure.

```haskell
listMap :: (a -> b) -> List a -> List b
listMap _ Empty = Empty
listMap f (Cons x rest) = Cons

 (f x) (listMap f rest)
```

The `listMap` function takes a function `f` that maps elements of type `a` to type `b` and a list of type `a`. It pattern matches on the constructors of the `List` data type to handle the different cases. When applied to an empty list, it returns an empty list. When applied to a non-empty list, it applies the function `f` to the current element and recursively maps `f` to the rest of the elements.

#### Computing the Sum of Elements in a List

Now, let's tackle an exercise. We want to write a function that takes a list of numbers and computes the sum of all the elements. We will call this function `listSum`.

To define the `listSum` function, we need to determine its type, base case, and recursive case.

#### Type

The `listSum` function should take in a list of numbers and return their sum. So its type can be:

```haskell
listSum :: List Int -> Int
```

#### Base Case

When the input list is empty, there are no elements to sum, so the base case should return 0.

```haskell
listSum Empty = 0
```

#### Recursive Case

For a non-empty list, we need to sum the first element with the sum of the rest of the elements. We can achieve this using recursion.

```haskell
listSum (Cons x rest) = x + listSum rest
```

In this case, we pattern match on the `Cons` constructor to extract the first element (`x`) and the rest of the list (`rest`). We recursively compute the sum of the rest of the list and add it to the current element.

Now, you can try implementing the `listSum` function and test it with different lists of numbers.


## Recursive Data Types with Trees

Recursive data types in Haskell allow us to define complex data structures that can include references to objects of the same type within themselves. Let's consider the example of a string binary tree.

### String Binary Tree

A string binary tree is a recursive data type that can be defined as follows:

```haskell
data StringBinaryTree = Leaf String | Node String StringBinaryTree StringBinaryTree
```

In this definition, a string binary tree is either a leaf containing a string or a node containing a string and two sub-trees that are also string binary trees. We can create trees by combining the leaf and node constructors.

#### Example: Creating String Binary Trees

Let's create some string binary trees using the leaf and node constructors:

```haskell
let leafA = Leaf "A"
let leafB = Leaf "B"
let leafC = Leaf "C"

let tree1 = Node "F" leafD leafE

let tree2 = Node "I" tree1 (Node "J" leafG leafH)
```

Here, we have created different trees by combining leaves and nodes using the constructors. The trees can be as simple or as complex as needed.

## Recursive Functions on Trees

Once we have defined a data type, we can write functions that operate on that data type using recursion. Recursive functions allow us to process complex data structures efficiently and elegantly. Let's explore some recursive functions on the string binary tree.

### Computing the Size of a Tree

To compute the size of a tree, we can write a recursive function that counts the number of nodes in the tree. The size of a leaf is considered to be 1, and the size of a tree is the sum of the sizes of its left and right sub-trees plus 1 for the current node.

```haskell
treeSize :: StringBinaryTree -> Int
treeSize (Leaf _) = 1
treeSize (Node _ left right) = 1 + treeSize left + treeSize right
```

Here, we pattern match on the constructors of the `StringBinaryTree` data type to handle the different cases. The function recursively computes the size of the left and right sub-trees and adds them together along with 1 for the current node.

### Computing the Height of a Tree

To compute the height of a tree, we can write a recursive function that determines the maximum number of levels or edges from the root to any leaf. The height of a leaf is considered to be 0, and the height of a tree is the maximum of the heights of its left and right sub-trees plus 1 for the current node.

```haskell
treeHeight :: StringBinaryTree -> Int
treeHeight (Leaf _) = 0
treeHeight (Node _ left right) = 1 + max (treeHeight left) (treeHeight right)
```

Similarly to the `treeSize` function, we pattern match on the constructors of the `StringBinaryTree` data type to handle the different cases. The function recursively computes the heights of the left and right sub-trees and selects the maximum value to add to 1 for the current node.

### Applying a Function to All Nodes of a Tree

We can also define a function that applies a given function to all nodes of a tree. This allows us to transform the values stored in the nodes while maintaining the tree structure.

```haskell
treeMap :: (String -> String) -> StringBinaryTree -> StringBinaryTree
treeMap _ (Leaf s) = Leaf (

f s)
treeMap f (Node s left right) = Node (f s) (treeMap f left) (treeMap f right)
```

In the `treeMap` function, we take in a function `f` that operates on strings and a `StringBinaryTree`. We pattern match on the constructors of the data type and apply the function to the values stored in the nodes. The function is recursively applied to the left and right sub-trees.

#### Example: Applying a Function to a Tree

Let's see an example of applying a function to a string binary tree:

```haskell
let exclamationTree = treeMap (++ "!") tree2
```

Here, we apply the function `(++ "!")` to all nodes in `tree2`, appending an exclamation mark to each string. The resulting tree is stored in the `exclamationTree` variable.

## Recursive Data Types: IntList
We can define recursive data types in Haskell. Let's consider a simple example of creating lists.

```haskell
data IntList
  = Empty
  | Cons Int IntList
  deriving Show
```

Here, an `IntList` is either an `Empty` list or a `Cons` cell containing an integer and another `IntList`.

### Recursive Data Types: Operations on IntList
We can define various operations on `IntList` using pattern matching.

```haskell
intListLength :: IntList -> Int
intListLength Empty = 0
intListLength (Cons _ xs) = 1 + intListLength xs

intListHead :: IntList -> Int
intListHead Empty = undefined
intListHead (Cons x _)

 = x

intListTail :: IntList -> IntList
intListTail Empty = undefined
intListTail (Cons _ xs) = xs

intListMap :: (Int -> Int) -> IntList -> IntList
intListMap _ Empty = Empty
intListMap f (Cons x xs) = Cons (f x) (intListMap f xs)
```

### Recursive Data Types: Example
Let's create some examples of `IntList`:

```haskell
list1 = Empty
list2 = Cons 6 Empty
list3 = Cons 10 (Cons 20 list2)
list4 = Cons (-4) list3
list5 = Cons 100 (Cons 13 list4)
list6 = Cons 100 (Cons 13 list5)
```

### Recursive Data Types: List Operations
We can define operations on lists, such as finding the length or sum.

```haskell
intListLength :: IntList -> Int
intListLength Empty = 0
intListLength (Cons _ xs) = 1 + intListLength xs

intListSum :: IntList -> Int
intListSum Empty = 0
intListSum (Cons x xs) = x + intListSum xs
```

## Combining Data Types
We can combine multiple data types to create more complex structures. Let's combine the `CardSuit` and `FaceValues` types to represent a deck of cards.

```haskell
data CardSuit = Clubs | Diamonds | Hearts | Spades
  deriving (Show, Eq, Ord)

data FaceValues
  = Two | Three | Four | Five | Six | Seven | Eight
  | Nine | Ten | Jack | Queen | King | Ace
  deriving (Show, Eq, Ord)

type Card = (FaceValues, CardSuit)

data CardList
  = Empty
  | Hand Card CardList
  deriving (Show, Eq, Ord)
```

Now we can create a deck of cards represented by `CardList` and perform operations on it.

## Type Classes
Type classes in Haskell define a set of functions that can operate on certain types. Some common type classes are `Eq`, `Ord`, `Show`, and `Read`.

For example, the `CardSuit` and `FaceValues` types can derive the `Show`, `Eq`, and `Ord` type classes, allowing us to print, compare, and order their values.

```haskell
data CardSuit = Clubs | Diamonds | Hearts | Spades
  deriving (Show, Eq, Ord)

data FaceValues
  = Two | Three | Four | Five | Six | Seven | Eight
  | Nine | Ten | Jack | Queen | King | Ace
  deriving (Show, Eq, Ord)
```
