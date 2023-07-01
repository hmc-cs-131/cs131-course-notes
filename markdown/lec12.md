### CS 131: Programming Languages

# Functional Abstractions

In this lecture, we will explore functional abstractions in Haskell. We'll cover important concepts such as typeclasses, functors, monads, and the do notation. These concepts provide powerful tools for writing reusable and composable code. So let's dive in!

## Typeclasses

Typeclasses in Haskell allow us to define common behavior for different types. They provide a way to generalize functions and operations that can work with various data types. We can think of typeclasses as interfaces or contracts that specify the behavior expected from types that are instances of the typeclass.

### Examples of Typeclasses

Let's explore some commonly used typeclasses in Haskell:

#### Eq Typeclass

The `Eq` typeclass defines equality and inequality operations. Instances of this typeclass can be compared for equality using the `==` operator.

#### Show Typeclass

The `Show` typeclass provides a way to convert values to strings. Instances of this typeclass can be converted to strings using the `show` function.

#### Read Typeclass

The `Read` typeclass enables conversion from strings to values. Instances of this typeclass can be created from strings using the `readsPrec` function.

#### Ord Typeclass

The `Ord` typeclass is used for types that can be compared. Instances of this typeclass can be compared using operators like `<=`, `<`, `>=`, `>`.

#### Num Typeclass

The `Num` typeclass represents numeric types and provides operations like addition (`+`), subtraction (`-`), multiplication (`*`), and more.

#### Fractional Typeclass

The `Fractional` typeclass is used for fractional numbers and provides division (`/`) and other related operations.

### Defining Data Types with Typeclasses

When defining our own data types, typeclasses can be useful in specifying the behavior and operations associated with those types.

#### Abstract Syntax Tree (AST) Example

Let's consider an example using an Abstract Syntax Tree (AST) for mathematical expressions. We define a data type called `Exp`, which can have two forms: `Num` for representing a number and `BinOp` for representing a binary operation. Additionally, we define a data type called `Op` to represent different operations.

```haskell
data Exp = Num Int | BinOp Op Exp Exp
data Op = Plus | Minus | Times | Divide

deriving (Show, Eq)
```

In the code snippet above, we use the `deriving` keyword to automatically derive instances of the `Show` and `Eq` typeclasses for our data types. This allows us to display and compare instances of these data types, similar to other built-in Haskell data types.

### Displaying and Comparing Data Types

Using the derived instances of the `Show` and `Eq` typeclasses, we can display and compare instances of our defined data types. For example, if we create an expression `Num 1`, Haskell can display it in the REPL. We can also compare two instances of `Num 1` and see that they are the same.

```haskell
-- Displaying instances
Num 1 -- Result: 1

-- Comparing instances
Num 1 == Num 1 -- Result: True
```

However, if we remove the `Show` typeclass from our data types, we will encounter an error when trying to display an expression. This error occurs because Haskell doesn't know how to display instances of our data type without the `Show` instance.

To overcome this issue, we can either derive the `Show` instance again or define our own instance of the `Show` typeclass. Defining our own instance allows us to customize how the data type is displayed. Here's an example of how we can define our own `Show` instance for the `Exp` data type:

```haskell
instance Show Exp where
  show (Num n) = show n
  show (BinOp op e1 e2)

 = "(" ++ show op ++ " " ++ show e1 ++ " " ++ show e2 ++ ")"
```

With this definition, constructing an expression like `Num 1` will display just the number `1`. Similarly, constructing a binary operation expression like `BinOp Plus (Num 1) (Num 2)` will display as "Plus 1 2".

### Implementing Typeclasses

In addition to deriving instances, we can implement our own typeclasses to define behavior for our data types. Let's consider the example of implementing the `Show` typeclass for our data types. Instead of deriving it, we can define our own `show` function.

```haskell
class Show a where
  show :: a -> String
```

To make `Exp` an instance of the `Show` typeclass, we need to define the `show` function for `Exp`. We can achieve this by defining instances for each form of the `Exp` data type.

```haskell
instance Show Exp where
  show (Num n) = show n
  show (BinOp op e1 e2) = "(" ++ show op ++ " " ++ show e1 ++ " " ++ show e2 ++ ")"

instance Show Op where
  show Plus = "+"
  show Minus = "-"
  show Times = "*"
  show Divide = "/"
```

With this implementation, constructing an expression like `Num 1` or `BinOp Plus (Num 1) (Num 2)` will use our defined `show` function to display the expressions.


## Functors

Functors in Haskell represent data structures that can be mapped over. They define the `fmap` function, which allows us to apply a function to each element within the structure while preserving the structure itself. The `fmap` function has the following type signature:

```haskell
fmap :: Functor f => (a -> b) -> f a -> f b
```

This type signature states that for a type constructor `f` to be a functor, it must implement the `fmap` function that takes a function from type `a` to type `b`, and a functorial value of type `f a`, and returns a functorial value of type `f b`.

One example of a functor is lists. We can use the `fmap` function to apply a function to each element of a list, effectively mapping over the list. The `fmap` function for lists would have the following signature:

```haskell
fmap :: (a -> b) -> [a] -> [b]
```

Using the `fmap` function on a list allows us to apply a transformation to each element without having to manually unwrap and rewrap the list. Functors provide a convenient way to perform common transformations on data structures.

Functors also provide a way to perform common transformations on other data structures without unwrapping and rewrapping them. For example, `Maybe` is a functor that represents an optional value. The `fmap` function for `Maybe` would have the following signature:

```haskell
fmap :: (a -> b) -> Maybe a -> Maybe b
```

This allows us to apply a function to the wrapped value inside a `Maybe` without worrying about the possibility of a `Nothing` value.

In addition to lists and `Maybe`, many other types in Haskell can be made instances of the `Functor` type class. By defining the `fmap` function for a particular type, we enable it to be used with functions that work on functors more generally. This abstraction provides a powerful tool for working with different types of data structures in a uniform way.

## Monads

Monads are a powerful abstraction in functional programming that enable the sequencing of computations. They encapsulate computations within a context and provide operations to compose these computations in a structured manner.

### Introduction to Monads

Monads provide a way to handle effects, such as IO, error handling, and non-determinism, in a controlled and modular way. They allow us to sequence actions, handle failures, and manage state effectively.

The key operation in monads is the bind operator `(>>=)`, pronounced as "bind," which allows us to chain computations together. It takes a monadic value, extracts the value inside it, and applies a function that produces a new monadic value.

Monads also provide the `return` function, which takes a value and wraps it in a monad. This function allows us to lift pure values into the monadic context, enabling composition with other monadic operations.

### Monadic Structure

The essence of a monad lies in its structure, which consists of two fundamental operations: `return` and `(>>=)`. By providing these operations, a data type becomes an instance of the `Monad` type class.

#### The `(>>=)` Operator

The `(>>=)` operator, also known as "bind," is the primary operation in monads. It takes a monadic value and a function that transforms the underlying value. The result is a new monadic value that encapsulates the transformed value.

```haskell
(>>=) :: Monad m => m a -> (a -> m b) -> m b
```

The `(>>=)` operator allows us to chain computations by passing the result of one computation to the next, preserving the monadic context throughout the sequence.

#### The `return` Function

The `return` function lifts a value into the monadic context. It takes a pure value and wraps it in the corresponding monad.

```haskell
return :: Monad m => a -> m a
```

The `return` function allows us to introduce pure values into the monadic world, enabling composition with other monadic operations.

### Monadic Effects

Monads provide a structured way to handle various effects in functional programming. Some common monadic effects include IO, error handling, and non-determinism. By leveraging the power of monads, we can handle these effects in a controlled and modular manner.

#### IO Monad

The IO monad in Haskell allows us to perform input/output operations while maintaining referential transparency. It ensures that IO actions are performed in a controlled and predictable manner. By using the IO monad, we can sequence IO actions using the `(>>=)` operator and handle IO-related effects effectively.

#### Error Handling Monad

Monads can also handle error handling in a structured way. By using a custom monad, we can propagate and handle errors gracefully, avoiding unexpected program crashes. The bind operator `(>>=)` plays a crucial role in sequencing computations while managing potential errors.

#### Non-determinism Monad

Monads can handle non-determinism, where a computation can have multiple possible outcomes. By utilizing a non-determinism monad, we can represent and combine these possibilities in a structured manner. The `(>>=)` operator allows us to chain non-deterministic computations and collect all possible results.

## Do Notation

The do notation is a powerful feature in Haskell that simplifies the expression of monadic computations. It provides a convenient syntax for working with monads and allows us to write imperative-style code in a monadic context, making it easier to understand and reason about sequential operations.

### Understanding Do Notation

In the do notation, we can use the `<-` symbol to bind the result of a monadic computation to a variable. This variable can then be used in subsequent computations within the same do block. The do notation takes care of automatically unwrapping and rewrapping monadic values, providing a more seamless programming experience.

### Advantages of Do Notation

The do notation is particularly useful when working with IO operations. It provides a clear and concise way to express sequences of input/output actions. By using the do notation, we can write IO code that resembles imperative programming, which can be more intuitive and easier to follow.

### Example: Reversing Input

Let's consider an example of using the do notation with the IO monad to reverse user input:

```haskell
reverseInput :: IO ()
reverseInput = do
  putStr "Enter a string: "
  input <- getLine
  let reversed = reverse input
  putStrLn ("Reversed string: " ++ reversed)
```

In this example, we define a function `reverseInput` that prompts the user for a string, reads the input using `getLine`, reverses the string using `reverse`, and finally prints the reversed string using `putStrLn`. The do notation allows us to express this sequential flow of IO actions in a readable and intuitive way, making the code easier to understand.

By using the do notation, we can break down complex IO operations into smaller, sequential steps, improving the clarity and maintainability of our code.

### Generalizing Do Notation

The do notation is not limited to IO operations but can be used with any monad. It provides a convenient way to sequence monadic operations and make our code more concise and readable.

For example, we can use the do notation with the `Maybe` monad. Suppose we have the following code that doubles a value within the `Maybe` monad:

```haskell
doubleMaybe :: Int -> Maybe Int
doubleMaybe n = Just (2 * n)
```

We can rewrite this code using the do notation as follows:

```haskell
doubleMaybeDo :: Int -> Maybe Int
doubleMaybeDo n = do
  let doubled = 2 * n
  return doubled
```

In this example, we bind the result of the computation `2 * n` to the variable `doubled` and then use `return` to wrap the value in the `Maybe` monad. The do notation provides a more concise and readable way to express monadic computations.

By understanding the relationship between do notation and monads, we can leverage this feature to write more expressive and understandable code, regardless of the specific monad being used.

## IO in Haskell

In this lecture, we will explore the concepts of input and output (I/O) in Haskell. Haskell is a purely functional programming language, which means it focuses on evaluating expressions without side effects. However, input and output operations, such as reading input from the user and printing to the screen, involve side effects. Therefore, we need to understand how I/O works in Haskell.

### Understanding I/O in Haskell

In Haskell, I/O operations are handled through the IO type and the IO monad. The IO type represents I/O actions and encapsulates the side effects associated with them. The IO monad is a mechanism that allows sequencing and composition of I/O actions.

### Printing to the Screen

To print a string to the screen, we can use the `putStrLn` function. This function takes a string as an argument and prints it out. The type of `putStrLn` is `String -> IO ()`, where `IO ()` represents an I/O action that produces no result.

```haskell
putStrLn :: String -> IO ()
```

Alternatively, we can use the `print` function, which automatically converts values to strings before printing them.

```haskell
print :: Show a => a -> IO ()
```

### Input from the User

To read input from the user, we can use the `getLine` function. This function waits for the user to enter input and returns it as a string. The type of `getLine` is `IO String`.

```haskell
getLine :: IO String
```

### Sequencing I/O Operations

In Haskell, we can sequence multiple I/O operations using the `do` notation. The `do` notation allows us to write a block of code where each line represents an I/O operation. The I/O operations are executed in the order they appear in the block.

```haskell
do
  -- I/O operation 1
  -- I/O operation 2
  -- ...
```

### Example: Printing and Input

Let's look at an example that combines printing and input. We can use the `do` notation to sequence the I/O operations.

```haskell
do
  putStr "Enter your name: "
  name <- getLine
  putStrLn ("Hello, " ++ name ++ "!")
```

In this example, we first print a prompt asking the user to enter their name. Then we use the `getLine` function to read the input and bind it to the variable `name`. Finally, we use `putStrLn` to print a personalized greeting.

### Example: Checking for Palindromes

Let's explore another example that demonstrates more advanced I/O operations. In this example, we will check if a given input string is a palindrome.

```haskell
do
  putStr "Enter a word: "
  input <- getLine
  let qualifier = if input == reverse input then "is" else "is not"
  putStrLn (input ++ " " ++ qualifier ++ " a palindrome.")
```

In this example, we prompt the user to enter a word and store the input in the variable `input`. We then use a `let` expression to define the variable `qualifier`, which determines whether the input is a palindrome or not. Finally, we print the result using `putStrLn`.


## Monadic Parsers

### Refactoring Combinators

As we deepen our understanding of parsing, it becomes clear that our existing combinator library has several overlapping patterns. These patterns often involve applying a parser to an input, followed by some computation based on the parser's success or failure. Refactoring these patterns allows us to streamline our code and remove duplications, thus making our library easier to manage and modify.

### Parser Combinator Refactoring

#### Identifying the Common Structure

On inspection of our combinators, we can see that many of them share a common structure. They apply a parser to the input, then perform actions based on whether the parsing was successful or not. This pattern hints at a possible abstraction, allowing us to factor out the shared functionality.

#### Abstracting the Next Step

This common pattern can be abstracted into a function that handles the next step after parsing. The function takes the elements of the parse state (the parse result and remaining input) and produces a new parse state. By employing type variables, we can make this function work for any types `A` and `B`, taking an `A` and producing a `Parser B`.

#### The Bind Operator

To encapsulate this abstraction, we introduce a new operator called the "bind" operator, `>>=`. The bind operator takes a parser `A` and a function from `A` to `Parser B`, returning a `Parser B`. This allows us to automatically pass the successful parse state to the next step, simplifying our implementation.

### Usage of the Bind Operator

Now that we've introduced the bind operator, let's look at how we can use it to define new parsing operations. For example, given a parser `letter` that parses lowercase letters, we might want to transform the parsed letter to uppercase. We can do this by binding the `letter` parser to a function that converts the parsed letter to uppercase and wraps it in a parser using the `return` function. This can be simplified even further using the `>>=:` operator, which combines the bind operator with function composition, giving us a convenient way to transform parsed results without having to explicitly use `return`.

The bind operator can also be used to sequence parsers. For instance, we might want to parse a digit followed by a letter, combining their results into a pair. Using the bind operator, we can sequence these parsers and capture their results without having to perform explicit error checking, simplifying our combinator implementations like `<:>` and `<++>`.

### Parser Combinator Core

Our parser combinator library centers around a few core elements. The `Parser` interface comprises a type that is parameterized by the type of its parse result. The `parse` function applies a parser to an input string, returning either a successful parse result or an error if parsing fails.

#### Core Functions and Combinators

Our library provides several basic parsing functions and combinators:

1. `get`: A parser that retrieves the next character from the input.
2. `return`: A function that takes a value and returns a parser that always produces that value.
3. `pfail`: A parser that always fails.
4. `<|>`: A combinator that combines two parsers, producing a parser that tries the first parser and, if it fails, then tries the second parser.
5. `<:>`: A combinator that combines a parser for a single value with a parser for a list of values, producing a parser for a list of values that starts with the single value.
6. `<++>`: A combinator that combines two parsers for lists of values, producing a parser for a list of values that is the concatenation of the two lists.

### Refactoring Our Parser Library

With these core elements

 in place, we can start refactoring our parser library using a monadic approach. This involves redefining our combinators and functions in terms of the bind operator and other monadic operations.

#### The `<+>` Combinator

The `<+>` combinator sequences two parsers, producing a parser that parses an `a` and a `b` in sequence and returns a pair of the parsed values. Its type is:

```haskell
(<+>) :: Parser a -> Parser b -> Parser (a, b)
```

An example of using `<+>` is `digit <+> letter`, which parses a digit followed by a letter and returns a pair of the parsed digit and letter.

Here's how we can redefine `<+>` using the bind operator and `return`:

```haskell
p1 <+> p2 = p1 >>= \a -> p2 >>= \b -> return (a, b)
```

#### The `<:>` Combinator

The `<:>` combinator combines a parser for a single value with a parser for a list of values. It applies the first parser and then the second parser, producing a parser that returns a list of values that starts with the parsed single value. Its type is:

```haskell
(<:>) :: Parser a -> Parser [a] -> Parser [a]
```

An example of using `<:>` is `digit <:> digits`, which parses a digit followed by any number of digits and returns a list of the parsed digits.

We can redefine `<:>` using the bind operator and `return` as follows:

```haskell
p1 <:> p2 = p1 >>= \a -> p2 >>= \as -> return (a:as)
```

#### The `<++>` Combinator

The `<++>` combinator concatenates the results of two list parsers. It applies the first parser and then the second parser, producing a parser that returns a list of values that is the concatenation of the two lists. Its type is:

```haskell
(<++>) :: Parser [a] -> Parser [a] -> Parser [a]
```

An example of using `<++>` is `digits <++> letters`, which parses a sequence of digits followed by a sequence of letters, returning a list of the parsed digits and letters.

Here's how we can redefine `<++>` using the bind operator and `return`:

```haskell
p1 <++> p2 = p1 >>= \as -> p2 >>= \bs -> return (as ++ bs)
```
