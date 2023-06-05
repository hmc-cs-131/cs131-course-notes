### CS 131: Programming Languages

# Lists, Tuples, Pattern Matching, and Parameterized Types

## Why Lists?

Lists are an essential data structure in programming languages. They allow us to combine related data into a single structure, providing convenience and clarity in code organization.

### Practical Reason: Data Organization

Collecting data together in a single data structure is convenient in programming languages. For instance:

- **Java**: Arrays are commonly used to group related data elements.
- **C++**: Linked lists provide a way to organize data dynamically.
- **Python**: Lists offer a flexible and versatile data structure.

### Pedagogical Reason: Recursion and Functional Languages

Lists are a recursive data structure, which makes them ideal for demonstrating recursion in functional languages like Haskell. In Haskell, a list can be defined recursively as follows:

- An empty list is represented as `[]`.
- A non-empty list consists of an element (`x`) followed by another list (`xs`), written as `x:xs`.

This recursive definition of lists, combined with the functional programming paradigm and the powerful pattern matching feature, enables us to write concise and expressive code.

```haskell
-- Recursive definition of a list in Haskell
data List a = Empty | Cons a (List a)

-- Example list in Haskell
myList = 1 : 2 : 3 : []

-- Pattern matching on lists in Haskell
sumList :: [Int] -> Int
sumList [] = 0
sumList (x:xs) = x + sumList xs
```

The recursive nature of lists, functional programming techniques, and pattern matching provide a powerful trio that allows for elegant and efficient code solutions.

## Lists in Haskell 

### Haskell Syntax for Lists

In Haskell, lists are defined using square brackets `[]` and can contain elements separated by commas. Here are some examples:
- `[4, 9, -13, 5, 1]`
- `[False, True, False, False]`
- `[3.1, 3.14, 3.141, 3.1419, 3.14159, 3.141592]`
- `[]` (an empty list)
- `[[1,2,3], [4,5,6,7], [8,9]]` (a list of lists)

One important characteristic of Haskell lists is that they are **homogeneous**, meaning all elements in a list must have the same type. Mixing elements of different types in a list will result in a type error.

### Building Lists in Haskell

#### The Cons Operator `(:)`
The cons operator `(:)` is used to construct lists in Haskell. It combines an element with an existing list to create a new list. Here's an example:
- `3 : [7, 15, 4]` creates the list `[3, 7, 15, 4]`

The cons operator is right-associative, meaning it associates to the right. This means that rightmost colons have higher precedence. For example:
- `3 : 7 : [15, 4]` is equivalent to `3 : (7 : [15, 4])`

To create an empty list, you can use the empty list literal `[]`.

#### Parentheses and Associativity
When building lists using the cons operator, parentheses can be used to clarify the associativity. For example:
- `(3 : (7 : (15 : (4 : []))))` ensures the elements are consed from left to right.

### Useful List Functions

#### `length`
The `length` function in Haskell returns the number of elements in a list. It has the following type signature:
```
length :: [a] -> Int
```
Examples:
- `length ["Hello", " world", "!"]` evaluates to `3`
- `length "Hello"` evaluates to `5`

#### `head` and `tail`
The `head` function returns the first element of a list, while the `tail` function returns everything after the first element. These functions have the following type signatures:
```
head :: [a] -> a
tail :: [a] -> [a]
```
Examples:
- `head ["Hello", ",", "world", "!"]` evaluates to `"Hello"`
- `tail ["Hello", ",", "world", "!"]` evaluates to `["world", "!"]`

#### `take` and `drop`
The `take` function takes a specified number of elements from the beginning of a list, while the `drop` function removes a specified number of elements from the beginning of a list.

 They have the following type signatures:
```
take :: Int -> [a] -> [a]
drop :: Int -> [a] -> [a]
```
Examples:
- `take 3 [5, 8, 9, 1, 13, 20, 3, 2]` evaluates to `[5, 8, 9]`
- `drop 2 [5, 8, 9, 1, 13, 20, 3, 2]` evaluates to `[9, 1, 13, 20, 3, 2]`

#### `null`
The `null` function checks if a list is empty. It returns `True` if the list is empty and `False` otherwise. Its type signature is as follows:
```
null :: [a] -> Bool
```
Examples:
- `null []` evaluates to `True`
- `null [3, -7]` evaluates to `False`

#### `elem`
The `elem` function checks if an element is present in a list. It returns `True` if the element is found and `False` otherwise. It has the following type signature:
```
elem :: Eq a => a -> [a] -> Bool
```
Examples:
- `elem 10 [30, 33, 37]` evaluates to `False`
- `elem '3' "CS131"` evaluates to `True`

#### `map`
The `map` function applies a given function to each element of a list and returns a new list containing the results. It has the following type signature:
```
map :: (a -> b) -> [a] -> [b]
```
Examples:
- `map (\x -> x * 2) [4, 5, 6]` evaluates to `[8, 10, 12]`
- `map (< 3) [10, 1, 8]` evaluates to `[False, True, False]`

#### `filter`
The `filter` function selects elements from a list that satisfy a given predicate (a function returning a Boolean value). It has the following type signature:
```
filter :: (a -> Bool) -> [a] -> [a]
```
Examples:
- `filter even [8, -13, 25, 16, 0, 2]` evaluates to `[8, 16, 0, 2]`
- `filter (< 3) [10, 1, 0, 6]` evaluates to `[1, 0]`

#### Other Useful List Functions
There are several other useful functions for working with lists in Haskell:

minimum: Returns the minimum element in a list.
maximum: Returns the maximum element in a list.
sum: Calculates the sum of all elements in a list.
product: Computes the product of all elements in a list.
These functions operate as expected based on their names. You can experiment with them to confirm their behavior.

#### Leveraging Built-in Functions
Haskell provides a rich set of built-in functions, especially for common operations on lists. If you come across a task that you think might already have a function to accomplish it, it's worth checking the Haskell documentation or searching online. For example, if you need to perform a specific operation on lists, there's a good chance that there is a built-in function for it.

By leveraging these built-in functions, you can simplify your code and take advantage of efficient and optimized implementations. However, please note that in some cases, we may ask you to implement specific functions on your own to enhance your learning experience, as we did earlier with the map function and the function that checks if an element is contained in a list.

Feel free to explore and utilize any functions you find useful, unless explicitly instructed otherwise. Asking questions on platforms like Piazza is always encouraged, as it can provide valuable insights and assistance in your learning journey.



### Pattern Matching for Lists

Pattern matching allows us to destructure lists and access their individual elements.

#### Case Expressions
Case expressions provide a way to pattern match on a value and execute different branches of code based on the matched pattern. Here's an example using case expressions to implement `myLength` and `myFilter` functions:
```haskell
myLength lst = case lst of
  [] -> 0
  (x:xs) -> 1 + myLength xs

myFilter test lst = case lst of
  [] -> []
  (x:xs) -> if test x then x : myFilter test xs else myFilter test xs
```

#### Pattern Matching Syntax
Pattern matching using function definitions can be more concise and expressive. Let's incorporate the notes from the previous section into the existing notes:

Pattern matching allows us to deconstruct lists and extract their individual elements. It provides a more concise and readable approach to handle different cases of input lists.

##### Implementing the `length` function

The `length` function can be implemented using pattern matching. Here's an example:

```haskell
myLength :: [a] -> Int
myLength [] = 0   -- base case: empty list
myLength (_:xs) = 1 + myLength xs   -- recursive case: ignore the head and compute length of the tail
```
In this implementation, we define two cases using pattern matching:
1. If the input list is empty (`[]`), we return 0.
2. If the input list has at least one element (`_:xs`), we ignore the head and recursively compute the length of the tail.

##### Implementing the `filter` function

The `filter` function can also be implemented using pattern matching. Here's an example:

```haskell
myFilter :: (a -> Bool) -> [a] -> [a]
myFilter _ [] = []   -- base case: empty list
myFilter p (x:xs)
  | p x = x : myFilter p xs   -- include the head if it satisfies the predicate
  | otherwise = myFilter p xs   -- exclude the head and recursively filter the tail
```
In this implementation, we define two cases using pattern matching:
1. If the input list is empty (`[]`), we return an empty list.
2. If the input list has at least one element (`x:xs`), we use guards (denoted by `|`) to check if the head (`x`) satisfies the given predicate (`p`). If it does, we include it in the filtered list; otherwise, we exclude it and recursively filter the tail.

By utilizing pattern matching, we can simplify the implementation of `length` and `filter` functions and improve their clarity.

With pattern matching, we can handle different cases of input lists concisely, resulting in more readable and expressive code.

## Tuples and Pattern Matching

### Tuples

Tuples are used to combine different types of data into a single structure. They have a fixed number of elements and are created using parentheses and commas to separate the elements. In Haskell, tuples provide a convenient way to group related data.

#### Example: Professor Tuples
Let's consider an example where we want to represent information about professors. We can use tuples with the following elements:
- Name of the professor (String)
- Course they are teaching (Int)
- Whether they have acted in a Shakespeare play (Bool)

```haskell
prof1 = ("Lucas Bang", 131, False)
prof2 = ("Ben Wiedermann", 131, True)
```

We have defined `prof1` and `prof2` as tuples representing two professors, where `prof1` contains the information for Lucas Bang and `prof2` contains the information for Ben Wiedermann.

### Pattern Matching with Tuples

Pattern matching allows us to destructure tuples and access their individual components. By using pattern matching, we can conveniently bind variables to the elements of a tuple.

#### Example: Pattern Matching on Professor Tuples
```haskell
prof1 = ("Lucas Bang", 131, False)
(name, course, acted) = prof1
```
After pattern matching, `name` will be assigned the value `"Lucas Bang"`, `course` will be assigned `131`, and `acted` will be assigned `False`.

Pattern matching on tuples provides a way to extract and work with specific elements of a tuple. It allows us to access and manipulate the data contained within tuples effectively.

#### Example: Applying Pattern Matching in Expressions
Pattern matching can also be used within expressions. Let's take an example where we have a tuple representing three numbers `a`, `b`, and `c`. We want to check if these numbers form a Pythagorean triple, where `a^2 + b^2 = c^2`.

```haskell
isRightTriangle :: (Int, Int, Int) -> Bool
isRightTriangle (a, b, c) = a^2 + b^2 == c^2
```

In the `isRightTriangle` function, we define a pattern matching on the tuple `(a, b, c)`. If the condition `a^2 + b^2 == c^2` is true, it returns `True`, indicating that the numbers form a Pythagorean triple. Otherwise, it returns `False`.

By using tuples and pattern matching, Haskell allows us to create and manipulate structured data, enabling us to solve a wide range of problems efficiently. Understanding how to work with tuples and apply pattern matching techniques opens up possibilities for elegant and powerful solutions in Haskell programming.

## Parameterized Types

### Recap: Building Lists in Haskell
When constructing lists, the cons operator `(:)` allows us to create lists that can hold values of any type. The type signature of `(:)` is as follows:
```
(:) :: a -> [a] -> [a]
```
The left side of `(:)` has type `a`, representing an individual element, while the right side has type `[a]`, representing the rest of the list.

### Examining Types with `type` Command

To check the type of an expression in GHCi, we use the `type` command followed by the expression. Here are some examples:

```haskell
type True         -- Result: Bool
type [True, False]  -- Result: [Bool]
type ["hello", "world"]  -- Result: [String]
```

We can also use the `type` command on functions. For example, if we have a function `timesTwo`:

```haskell
timesTwo :: Int -> Int
timesTwo x = x * 2
```

We can check its type:

```haskell
type timesTwo  -- Result: Int -> Int
```

Note: Instead of writing out the whole word "type," we can use `:t` as a shorthand in GHCi.

Now, let's delve into the concept of parameterized types. We'll start by examining the type of the cons operator (`:`) and other operators like `(++)`, `map`, and `filter`.

### The Type of Cons Operator (`:`)

The cons operator has the following type signature:

```haskell
(:) :: a -> [a] -> [a]
```

- The first argument has type `a`.
- The second argument is a list of type `[a]`.
- The result is a list of type `[a]`.

For example, when we cons the number `3` onto the list `[1, 2]`, we get `[3, 1, 2]`. The type `a` can be inferred from the type of the argument (`3`) as `Int`.

### The Type of Concatenation Operator (`++`)

The concatenation operator has the following type signature:

```haskell
(++) :: [a] -> [a] -> [a]
```

- The first argument is a list of type `[a]`.
- The second argument is also a list of type `[a]`.
- The result is a list of type `[a]`.

For example, when we concatenate the lists `[3, 2]` and `[7, 10, 5]`, we get `[3, 2, 7, 10, 5]`. The type `a` is inferred as `Int` based on the types of the input lists.

### The Type of Map Function

The `map` function has the following type signature:

```haskell
map :: (a -> b) -> [a] -> [b]
```

- The first argument is a function that takes a value of type `a` and returns a value of type `b`.
- The second argument is a list of type `[a]`.
- The result is a list of type `[b]`.

For example, when we apply the `timesTwo` function to the list `[3, 5, 7]`, we get `[6, 10, 14]`. In this case, `a` is inferred as `Int` and `b` is also inferred as `Int`.

### The Type of Filter Function

The `filter` function has the following type signature:

```haskell
filter :: (a -> Bool) -> [a] -> [a]
```

- The first argument is a function that takes a value of type `a` and returns a `Bool` value.
