### CS 131: Programming Languages

# Introduction to Haskell and Functional Programming

## Today's Topics
1. The Read-Eval-Print Loop (REPL)
2. A Tour of Haskell:
   - Basic values and types
   - Calling functions
   - Variables, bindings, and scope
   - Writing code in files
   - Defining functions
   - Types
3. Functional Programming: Definitions and Foundations
4. Abstraction: The Essence of CS 131

Learning a new programming language can be both exciting and frustrating. In this course, we will explore Haskell and delve into the world of functional programming.

## Haskell: Getting Started

### REPL: Read-Eval-Print Loop
When working with Haskell, we often use a tool called the REPL (Read-Eval-Print Loop) to interactively experiment with code. The REPL allows us to enter expressions, evaluates them, and prints the results. It provides a convenient way to explore Haskell's features and test code snippets.

You can access an online REPL for Haskell on platforms like `repl.it`.

### Haskell: Basic Values and Types
In Haskell, values represent specific instances of data, while types categorize these values. Let's take a look at some basic types in Haskell:

- Integer: Whole numbers like 1, 2, 100000000000, -42, etc.
- Double: Floating-point numbers like 3.14, 3.2831, -2.718, etc.
- Bool: Boolean values, either True or False.
- Char: Individual characters enclosed in single quotes, such as 'a', 'z', etc.
- String: Sequences of characters enclosed in double quotes, like "hello", "world", etc.

Haskell also supports lists and tuples, which are commonly used types. Lists are denoted by square brackets (`[ ]`), and tuples are denoted by parentheses (`( )`).

```haskell
-- Examples of basic values and types
1 :: Integer
3.14 :: Double
True :: Bool
'a' :: Char
"hello" :: String

-- List of integers
[1, 2, 3, 4] :: [Integer]

-- Tuple of boolean and double
(True, 0.5) :: (Bool, Double)
```

It's important to note that in Haskell, all type names start with an uppercase letter. However, not all uppercase names are types.

Operations can be performed on these values and types, such as arithmetic operations (`+`, `-`, `*`, `/`) and comparison operations (`==`, `/=`, `>`, `<`, `>=`, `<=`). Additionally, the `++` operator is used to concatenate strings and lists.

### Haskell: Calling Functions
Haskell is a functional programming language, which means that functions play a central role. Calling functions in Haskell is straightforward:

```haskell
-- Examples of function calls
sqrt 4        -- Calculates the square root of 4
show 42       -- Converts the number 42 into a string
min 0 42      -- Returns the minimum value between 0 and 42
max 100 (42 + 1)  -- Returns the maximum value between 100 and 42 + 1
not True      -- Negates the boolean value True
```

Functions in Haskell can also be used with infix operators, which require parentheses when used with other operators or expressions.

### Haskell: Variables, Bindings, and Scope
In Haskell, we can associate variable names with expressions through bindings. This process is similar to assignment in other programming languages. Let's explore some concepts related to variables, bindings, and scope in Haskell.

- Binding (noun) and bind (verb):

 Associates a variable name with an expression.


- Value (noun): The expression to which a name is bound.
- Reference (verb): Using a name in an expression. During evaluation, the name acts as an alias for the expression.
- Scope: The region of the program where a name can be referenced. A variable's scope depends on where it is bound.
- Lookup (verb) or resolve (verb): Evaluating a name and finding its value.

Here's some related vocabulary to keep in mind:

- Variable name: The name given to a variable. In Haskell, variable names are written in lowercase.
- Value: The expression to which a name is bound.
- Top-level bindings: Similar to global variables, these bindings have a scope that extends throughout the entire file or the rest of the GHCi session.
- Local bindings: These bindings have a limited scope within a function or a `let` expression.

```haskell
-- Top-level bindings (global variables)
x = 21
y = 2 * x

-- Local binding using a let expression
let x = 21 in x + x

-- Local binding using a where clause
f x = value + 1 / value
  where value = x * x
```

It's worth noting that in Haskell, the "let before use" rule applies, meaning that bindings must be defined before they are referenced.

#### Trick question: What's the value of x?

```haskell
x = 24
x = 41
x = x + 1
```

If we type this code into a file and try to run it, we will encounter an error:

```
main.hs:2:1: error:
    Multiple declarations of `x'
…
  |
2 | x = 41
  | ^
main.hs:3:1: error:
    Multiple declarations of `x'
…
  |
3 | x = x + 1
  | ^
```

In GHCi (Glasgow Haskell Compiler interactive environment), we can interact with the code as follows:

1. We can type the first line, `x = 24`, and get the value of x.
2. We can type the second line, `x = 41`, and get the value of x.
3. We can type the third line, `x = x + 1`,
   but when we try to get the value of x,
   GHCi goes into an infinite loop!
   
These results occur due to the nature of how Haskell handles variable assignments and evaluations. In Haskell, variables are immutable, meaning they cannot be changed once assigned. The line `x = x + 1` tries to assign a new value to x based on its current value, but this creates a circular dependency that results in an infinite loop when evaluated.

This example highlights the importance of understanding the language-specific behaviors and rules when writing and executing code. Haskell's immutability and strict evaluation strategy can lead to unexpected outcomes if not handled correctly.

### Haskell: Writing Code in Files
Haskell code is typically written in files with the `.hs` extension. Let's take a look at some additional aspects related to writing Haskell code in files:

- Comments: Single-line comments can be added using `--`, while multiline comments can be enclosed between `{--` and `--}`.
- Loading code in GHCi: Instead of clicking the "Run" button on `repl.it`, it's recommended to load the code into GHCi, the Haskell interpreter. You can do this using the `:load <file>` or `:l <file>` command. This allows you to interactively test your code.

If you modify a loaded file and want to reload its contents, you can use the `:reload` or `:r` command.



### Haskell: Defining Functions
Defining functions in Haskell is straightforward and follows a simple syntax. Let's explore some key concepts related to function definitions:

- Function definitions: Functions are defined by providing the function name, followed by the parameters and the function body.
- Function calls: Functions can be called by providing the function name followed by the arguments.
- Parameter scope: The scope of the parameters is limited to the function body.
- Local bindings within functions: Haskell provides two ways to define local bindings within a function: `let` expressions and `where` clauses.

Here's an example to illustrate these concepts:

```haskell
-- Function definitions
successor n = n + 1
average x y = (x + y) / 2

-- Function calls
successor 1
average 0 10

-- Local bindings in a function using let expressions
f x = let value = x * x
      in value + 1 / value

-- Local bindings in a function using where clauses
g x = value + 1 / value
  where value = x * x
```

Both `let` expressions and `where` clauses allow us to define local variables within a function. The scope of a `let` binding is limited to the body of the `let` expression, while the scope of a `where` clause extends to the entire function (including the `where` clause itself).

### Types in Haskell
Haskell is a statically typed language, meaning that types are checked during compilation. Let's explore some concepts related to types in Haskell:

- Type-safe: A program that has no type errors is considered type-safe.
- Type-check: The process of determining whether a program has type errors.
- Static typing: A property of a program that can be determined without running it. In statically typed languages, type checking is typically performed by the compiler. If a type error is found, the program won't compile.
- Dynamic typing: A property of a program that is determined by running it. In dynamically typed languages, type checking may be performed by the interpreter during runtime. If a program encounters a type error, it may crash.
- Type annotation: Information provided by the programmer about the type of a variable, function, etc.
- Type inference: A form of type checking that infers types without requiring extensive type annotations.

In Haskell, types are typically inferred by the compiler based on the expressions used. However, it's still good practice to provide type annotations for clarity and documentation.

You can check the type of an expression in GHCi using the `:type <expr>` or `:t <expr>` command.

```haskell
-- Function types
successor :: Integer -> Integer
average :: Double -> Double -> Double
```

By specifying type annotations, we can ensure that functions are used correctly and catch potential type errors early on.

## Functional Programming: Some Basic Concepts

### The Essence of CS 131: Abstraction
In CS 131, we emphasize the concept of abstraction. Abstraction involves refactoring code by eliminating repetition and extracting common operations into helper functions. This process improves code quality, reduces duplication, and enhances readability.

By identifying patterns and common operations, we can factor them out into separate functions, allowing us to write more concise and reusable code.

```haskell
-- Repeated code
2 * 2 + 1
3 * 2 + 1
4 * 2 + 1
5 * 2 + 1

-- Refactored code using a helper function
f :: Integer -> Integer
f n = n * 2 + 1

-- Function calls
f 2
f 3
f 4
f 5
```

In the refactored code above, we introduced a helper function `f` to eliminate the repetition. Now, instead of duplicating the same expression multiple times, we can simply call `f` with different arguments. This approach improves code maintainability and reduces the risk of introducing errors.

Abstraction is a fundamental concept in CS 131, allowing us to write clean and reusable code.

## Exercises

1. Write a function `circleArea` that calculates the area of a circle given its radius as a parameter. The formula for the area of a circle is `pi * r^2`, where `pi` is a constant (approximately 3.14159). Use the `Double` type for the radius and the result.

2. Implement a function `isPrime` that takes an integer as input and returns `True` if it is a prime number, and `False` otherwise. A prime number is a positive integer greater than 1 that has no positive divisors other than 1 and itself.

Try solving these exercises and test your functions in the Haskell REPL.
