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

## Haskell: Getting Started

### REPL: Read-Eval-Print Loop
When working with Haskell, we often use a tool called the REPL (Read-Eval-Print Loop) to interactively experiment with code. The REPL allows us to enter expressions, evaluates them, and prints the results. It provides a convenient way to explore Haskell's features and test code snippets.

You can access an online REPL for Haskell on platforms like `repl.it`.

### Haskell: Basic Values and Types
In Haskell, values represent specific instances of data, while types categorize these values. Let's take a look at some basic types in Haskell:

- `Integer`: Whole numbers like 1, 2, 100000000000, -42, etc.
- `Double`: Floating-point numbers like 3.14, 3.2831, -2.718, etc.
- `Bool`: Boolean values, either True or False.
- `Char`: Individual characters enclosed in single quotes, such as 'a', 'z', etc.
- `String`: Sequences of characters enclosed in double quotes, like "hello", "world", etc.

Note that in Haskell, all type names are uppercase. 

Haskell also supports lists (`[ ]`) and tuples (`( )`) as commonly used types. Lists are homogeneous, meaning they can only store elements of the same type, and provide a flexible way to store ordered sequences of values. Tuples, on the other hand, are heterogeneous, meaning they can store elements of different types, and they have a fixed length. Lists are useful for representing ordered collections of the same type, while tuples allow combining different value types into a single structure.

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

### Type Error Example

Type errors in Haskell occur when there is a mismatch between the expected type and the actual type of a value or expression. Let's examine a specific type error and its components.

**Error Message:**
```
<interactive>:27:14: error:
    • Couldn't match expected type ‘Bool’ with actual type ‘Char’
    • In the expression: 'a'
      In the expression: [True, True, 'a']
      In an equation for ‘it’: it = [True, True, 'a']
```

**Location:** The error occurred at line 27, column 14 in the specified file.

**Description:** The error arises when assigning a value of type `Char` to a list that expects elements of type `Bool`. The problematic expression is `[True, True, 'a']`.

**Explanation:** In Haskell, lists are homogeneous, meaning they can only contain elements of the same type. However, the presence of the character `'a'` violates this rule by having a different type (`Char`) than the expected type (`Bool`).

**Solution:** To resolve the error, ensure that the list contains only elements of the expected type (`Bool`). Remove the character `'a'` or replace it with a `Bool` value to achieve type consistency and avoid type errors.

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

- Binding (noun) and bind (verb): Associates a variable name with an expression. This is similar to assignment (noun) and assign (verb), which we often see in imperative programming languages.
- Value (noun): The expression to which a name is bound.
- Reference (verb): Using a name in an expression. During evaluation, the name acts as an alias for the expression.
- Scope: The region of the program where a name can be referenced. A variable's scope depends on where it is bound. In Haskell, a scope can bind a name at most once. In other words, all "variables" are constants!
- Lookup (verb) or resolve (verb): Evaluate a name and finding its value.

Here's some related vocabulary to keep in mind:

- Variable name: The name given to a variable. In Haskell, variable names are written in lowercase.
- Top-level bindings: Similar to global variables, these bindings have a scope that extends throughout the entire file or the rest of the GHCi (Glasgow Haskell Compiler interactive environment) session. 
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

In GHCi, we can interact with the code as follows:

1. We can type the first line, `x = 24`, and get the value of x.
2. We can type the second line, `x = 41`, and get the value of x.
3. We can type the third line, `x = x + 1`,
   but when we try to get the value of x, GHCi goes into an infinite loop!
   
These results occur due to the nature of how Haskell handles variable assignments and evaluations. In Haskell, variables are immutable, meaning they cannot be changed once assigned. The line `x = x + 1` tries to assign a new value to x based on its current value, but this creates a circular dependency that results in an infinite loop when evaluated.

This example highlights the importance of understanding the language-specific behaviors and rules when writing and executing code. Haskell's immutability and strict evaluation strategy can lead to unexpected outcomes if not handled correctly.

#### `let` expressions and Local Binding 

**Local Bindings and Scopes in Haskell**

In Haskell, local bindings allow us to create temporary variables with a limited scope, similar to local variables in other programming languages. This is achieved using the `let` keyword or the `where` clause.

The `let` expression allows us to introduce local bindings within an expression. The syntax for a `let` expression is:
```haskell
let <binding> in <expression>
```
where `<binding>` represents the declaration of a variable and `<expression>` represents the body of the `let` expression.

For example:
```haskell
let x = 21 in x + x
```
In this case, the variable `x` is locally bound to the value 21. The scope of `x` is limited to the body of the `let` expression. The result of the `let` expression is the evaluation of the body, which in this case is `x + x`.

Scopes can be nested in Haskell, allowing for the creation of multiple levels of local bindings. Each nested `let` expression introduces its own scope. When resolving names, Haskell starts from the innermost scope and moves outward, ensuring that the correct binding is used.

Alternatively, Haskell also provides the `where` clause, which is used for local bindings at the end of a function definition. The syntax for a `where` clause is:
```haskell
function definition
where
  <binding>
```
where `<binding>` represents the declaration of a variable that is accessible within the function body.

For example:
```haskell
myFunction x = y + y
  where
    y = x * 2
```
In this case, the variable `y` is locally bound to the value `x * 2` within the `where` clause. The scope of `y` is limited to the function body of `myFunction`. The result of `myFunction` is the evaluation of `y + y`.

Both `let` expressions and `where` clauses are powerful constructs in Haskell for creating local bindings and managing variable visibility within specific code blocks. They provide a way to define variables with limited scope and promote modular and readable code.

### Haskell: Writing Code in Files

Haskell files typically have the `.hs` extension. When writing Haskell code in files, there are a few additional aspects to consider. Let's explore them:

**Comments:** Comments in Haskell can improve code readability and provide explanations. Single-line comments start with `--`, while multiline comments are enclosed between `{--` and `--}`.

```haskell
-- This is a single-line comment

{--
   This is a
   multiline comment
--}
```

**Loading Code in GHCi:** GHCi (Glasgow Haskell Compiler interactive) is the Haskell interpreter that allows interactive testing and evaluation of code. Instead of using the "Run" button on `repl.it`, it's recommended to load your code into GHCi. This can be done using the `:load <file>` or `:l <file>` command.

```haskell
-- Load a file into GHCi
:load MyCode.hs
```

This enables you to interactively test your code and experiment with different expressions and functions. If you make changes to the loaded file and want to reload its contents, you can use the `:reload` or `:r` command in GHCi.

```haskell
-- Reload the contents of a file in GHCi
:reload
```

By using GHCi, you can have a more interactive development experience and easily iterate on your code by loading and reloading files as needed.

### Haskell: Defining functions

In Haskell, defining and calling functions follows a simple syntax. Let's explore the two key aspects of function usage:

#### Function Definitions
Functions in Haskell are defined by specifying the function name, parameters, and the function body. Here are the key concepts related to function definitions:

- **Name**: A function is identified by its name, which is used to refer to and call the function.
- **Parameters**: Parameters are placeholders that represent the input values to the function. They are listed after the function name and separated by spaces.
- **Function Body**: The function body contains the actual code that specifies the computation to be performed. It is executed when the function is called.

#### Function Calls
To use a defined function, you can call it by providing the function name followed by the arguments. Here are the related terms:

- **Arguments**: Arguments are the actual values passed to a function when it is called. They correspond to the parameters defined in the function's signature.
- **Parameter Scope**: The scope of the parameters is limited to the function body. They are accessible and valid only within the function's context.

Here are some examples to illustrate function definitions and calls:

```haskell
-- Function definitions
successor n = n + 1
average x y = (x + y) / 2

-- Function calls
successor 1
average 0 10
```

In addition to function definitions and calls, Haskell provides ways to define local bindings within functions. These local bindings allow you to define variables that are only accessible within the function. Let's explore different approaches using local bindings to calculate x^2 + 1/x^2:

```haskell
-- Local bindings in a function using explicit computation
f x = x * x + 1 / (x * x)

-- Local bindings in a function using let expressions
f x = let value = x * x
      in value + 1 / value

-- Local bindings in a function using where clauses
f x = value + 1 / value
  where value = x * x
```

In the first example, the computation is directly expressed in the function body. The second and third examples demonstrate the usage of let expressions and where clauses to define local variables within the function. Both approaches achieve the same result, but they differ in their syntax and scoping rules.

Let expressions provide a way to define local variables within a function. The scope of a let binding is limited to the body of the let expression. On the other hand, where clauses define local variables at the end of a function, and their scope extends to the entire function body.

By understanding function definitions, function calls, and the usage of local bindings, you can effectively write and utilize functions in Haskell to build complex computations and solve problems.

#### Pattern Matching
Pattern matching is a powerful feature in Haskell that allows for concise and expressive function definitions based on different patterns. Let's see how it works using an example with a factorial function:

```haskell
-- Using if-then-else
fact n = if n == 0 
         then 1 
         else n * fact (n - 1)

-- Using pattern matching
fact 0 = 1
fact n = n * fact (n - 1)
```

In the first example, the factorial function `fact` is defined using an `if-then-else` construct to handle the base case (when `n` is equal to 0) and the recursive case. However, the second example demonstrates the power of pattern matching. The factorial function is defined using two patterns: one for the base case and one for the recursive case. 

When a program calls the factorial function, Haskell tries to match the call's argument against each pattern, from top to bottom. As soon as it finds a match, Haskell uses that specific version of the function.

Pattern matching allows us to create specialized behavior for different inputs, making our code more concise and readable. It offers the flexibility to handle different cases directly in the function definition.

### Types in Haskell
Haskell is a statically typed language, meaning that types are checked during compilation. Let's explore some concepts related to types in Haskell:

- **Type-safe** (adjective): A program is considered type-safe when it has no type errors. Type errors occur when there is a mismatch between the expected and actual types of values in the program.
- **Type-check** (verb): To determine whether a program has type errors, the process of type checking is performed. Type checking ensures that the types of expressions, variables, and functions are consistent and compatible.
- **Static** (adjective): In Haskell, type checking is a static process, meaning it can be determined without running the program. The compiler performs type checking during the compilation phase, analyzing the program's types before execution.
- **Dynamic** (adjective): In contrast, dynamic properties of a program are determined by running the program. Dynamic type checking can occur during program execution and may result in runtime errors if type inconsistencies are encountered.
- **Statically typed** (adjective): Haskell is a statically typed programming language, which means it performs static type checking. The compiler checks the types of expressions, variables, and functions, ensuring type consistency throughout the program. If a type error is found, the program fails to compile.
- **Dynamically typed** (adjective): In dynamically typed programming languages, type checking may occur at runtime. Interpreters or runtime systems perform checks on types as the program executes. If a type error is encountered, the program may crash or raise runtime errors.
- **Type annotation** (noun): Type annotations provide explicit information about the types of variables, functions, or expressions. Programmers can annotate their code with type declarations to provide hints to the compiler or improve code clarity.
- **Type inference** (noun): Haskell features powerful type inference capabilities, allowing the compiler to deduce types without extensive type annotations. Type inference reduces the need for explicit type declarations while maintaining type safety.

By leveraging static type checking, Haskell helps catch potential type errors early in the development process, providing a high level of confidence in program correctness. The balance between static typing and type inference allows for concise code while maintaining type safety.
In Haskell, types are typically inferred by the compiler based on the expressions used. However, it's still good practice to provide type annotations for clarity and documentation.

You can check the type of an expression in GHCi using the `:type <expr>` or `:t <expr>` command.

```haskell
-- Function types
successor :: Integer -> Integer
average :: Double -> Double -> Double
```

#### Function Types
In Haskell, functions have explicit type declarations that specify the types of their parameters and the result they produce. Let's explore the concept of function types:

- Function Name: The name of the function identifies it and allows it to be called in the program.

- Parameter Types: Each parameter of a function has a specific type that defines the kind of values it can accept. Function types include the types of all their parameters.

- Result Type: The result type specifies the type of value that the function produces as its output.

In Haskell, function types are indicated using an arrow (`->`) notation. The arrow separates the parameter types from the result type, indicating the flow of data within the function. For example:

```haskell
successor :: Integer -> Integer
```

The `::` symbol is read as "has type," and the arrow (`->`) denotes the function type. In this case, it reads as "successor is a function that takes an `Integer` and results in an `Integer`." The arrow serves as a visual representation of the function's input and output.

Here's another example:

```haskell
average :: Double -> Double -> Double
```

In this case, the arrow separates the parameter types (`Double` and `Double`) from the result type (`Double`). The function type reads as "average is a function that takes two `Double` values and results in a `Double`."

By specifying the types of functions, Haskell enables static type checking. The type declarations provide information about the expected inputs and outputs, helping detect type errors early in the development process. Function types in Haskell facilitate program clarity, robustness, and maintainability. 

## Functional Programming: Some Basic Concepts

### What is Functional Programming?
- **Evaluation of Expressions**: In functional programming, computation occurs through the evaluation of expressions. This is in contrast to imperative programming, where computation relies on updating state.
- **Stateless Computation**: Functional programming emphasizes stateless computation, where the output of a function solely depends on its input, without any hidden side effects or reliance on external state.
- **Pure Functional Programming**: In pure functional programming, the evaluation of expressions is the sole mechanism for computation. Pure functions are used, which produce consistent results based only on their inputs, without modifying any external state.
- **Haskell: A Pure, Functional Language**: Haskell is an example of a pure, functional programming language. It enforces immutability, encourages the use of pure functions, and facilitates expression evaluation as the primary mode of computation.

Functional programming provides a different approach to software development, focusing on composing and evaluating expressions rather than manipulating state. By embracing the principles of functional programming, languages like Haskell enable developers to write code that is easier to reason about, facilitates code reuse, and supports efficient and parallel execution.

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
