### CS 131: Programming Languages

# Lists, Tuples, Pattern Matching, and Parameterized Types

## Why Lists?

#### Practical Reason
Collecting data together in a single data structure is convenient. In programming languages like Java, C++, and Python, we have arrays, linked lists, and lists, respectively, for such purposes.

#### Pedagogical Reason
Lists are a recursive data structure, making them ideal for demonstrating recursion in functional languages like Haskell. In Haskell, a list is either empty (`[]`) or an element followed by another list (`x:xs`). This combination of recursive data structures, functional languages, and pattern matching forms a powerful trio that enables concise and expressive code.

### Haskell Syntax for Lists

In Haskell, lists are defined using square brackets `[]` and can contain elements separated by commas. Here are some examples:
- `[4, 9, -13, 5, 1]`
- `[False, True, False, False]`
- `[3.1, 3.14, 3.141, 3.1419, 3.14159, 3.141592]`
- `[]` (an empty list)
- `[[1,2,3], [4,5,6,7], [8,9]]` (a list of lists)

One important characteristic of Haskell lists is that they are homogeneous, meaning all elements in a list must have the same type. Mixing elements of different types in a list will result in a type error.

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
Pattern matching using function definitions can be more concise and expressive. Here's an example of `myLength` and `myFilter` using pattern matching syntax:
```haskell
myLength [] = 0
myLength (_:xs) = 1 + myLength xs

myFilter _ [] = []
myFilter test (x:xs)
  | test x = x : myFilter test xs
  | otherwise

 = myFilter test xs
```

## Tuples and Pattern Matching

### Tuples
Tuples are used to combine different types of data into a single structure. They have a fixed number of elements. In Haskell, tuples are created using parentheses and commas to separate the elements. Here's an example:
```haskell
prof1 = ("Lucas Bang", 131, False)
prof2 = ("Ben Wiedermann", 131, True)
```

#### Pattern Matching with Tuples
Pattern matching can also be used with tuples to destructure them and access their individual components. Here's an example:
```haskell
prof1 = ("Lucas Bang", 131, False)
(name, course, acted) = prof1
```
After pattern matching, `name` will be assigned the value `"Lucas Bang"`, `course` will be assigned `131`, and `acted` will be assigned `False`.

### Parameterized Types

#### Building Lists in Haskell
When constructing lists, the cons operator `(:)` allows us to create lists that can hold values of any type. The type signature of `(:)` is as follows:
```
(:) :: a -> [a] -> [a]
```
The left side of `(:)` has type `a`, representing an individual element, while the right side has type `[a]`, representing the rest of the list.

#### Building Lists and Operations
Operations like `map`, `filter`, and `length` are defined using parameterized types. These functions can work on lists containing elements of any type. For example, `map` has the following type signature:
```
map :: (a -> b) -> [a] -> [b]
```
The type variables `a` and `b` represent any types. This allows `map` to work with lists of different element types.

#### Pattern Matching and Parameterized Types
Pattern matching and parameterized types work together seamlessly. When pattern matching on lists, the type variable `a` can represent any type, allowing us to handle different cases based on the elements' types.

## Summary
In this lecture, we explored the practical and pedagogical reasons for using lists in Haskell. We learned about building lists using the cons operator `(:)` and concatenation operator `(++)`. We discussed useful list functions such as `length`, `head`, `tail`, `take`, `drop`, `null`, `elem`, `map`, `filter`, and examined their type signatures. We also covered pattern matching for lists and tuples, as well as the concept of parameterized types, which allows functions to operate on lists containing elements of any type.