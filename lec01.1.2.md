# HMC CS 131
## Week 1, Lecture 1
## Introduction to Haskell and Functional Programming

Hello! This course module will provide an introduction to Haskell and functional programming. It's important to note that the content of slides skipped in the video lectures may still prove useful. The skipped slides usually pertain to content also available on the Sakai page or demonstrate "live coding" sessions from the video.

### Course Agenda
1. Attendance on gradescope
2. Module 1 check-in + lead into Module 2.1
3. Haskell on the lab machines
4. Module 2.1 introduction (2.2 coming this afternoon!)
5. Most of the day: HW 1

### Today's Topics
- The Read-Eval-Print Loop (REPL)
- A Tour of Haskell
- Functional Programming: definitions and foundations
- Abstraction: The Essence of CS 131

Learning a new programming language can be both exciting and frustrating. In this module, we'll get started with Haskell.

### Haskell: Basic Values and Types

In Haskell, we have various types of values, each with its unique characteristics. Below are the types and examples of values they can hold:

- Integer: 1, 2, 100000000000, -42, etc.
- Double: 3.14, 3.2831, -2.718, etc.
- Bool: True, False
- Char: 'a', 'z', etc.
- String: "hello", "world"

Also, Haskell supports complex data types like Lists and Tuples:
- [Integer]: [1, 2, 3, 4] (list of Integer)
- (Bool, Double): (True, 0.5) (tuple of Bool and Double)

Here are some operations you can perform in Haskell:
- Arithmetic operations: +, -, *, /
- Comparison operations: ==, /=, >, <, >=, <=
- Logical operations: &&, || (for boolean values)
- String concatenation: ++

#### Type Error
A type error occurs when the type of a value doesn't match the expected type. For example, creating a list [True, True, 'a'] will cause a type error because the list contains both Bool and Char types, but lists in Haskell are homogeneous.

### Haskell: Calling Functions

Haskell is a functional programming language, and calling functions in Haskell is straightforward. Here are examples of some function calls:

```haskell
sqrt 4
show 42
min 0 42
max 0 42
```
Here are a few things to be careful about while calling functions:
- Parentheses are necessary for certain operations, e.g., `max 100 (42 + 1)` is correct, while `max 100 42 + 1` is incorrect.
- `/` is floating-point division, while `div` is integer division.

### Haskell: Variables, Bindings, and Scope

In Haskell, the terms "binding" and "value" refer to the association of a variable name with an expression. The term "scope" refers to the region of the program where a name can be referenced. Here's an example of bindings in Haskell:

```haskell
x = 21
y = 2 * x 
```
Note that variable names in Haskell are always lower-case. Also, Haskell does not allow for re-assignment of variables. The value associated with a variable, once assigned, cannot be changed within its scope. 

### Haskell: Writing Code in Files

Haskell code files use the `.hs` extension. Top-level bindings can be included in a file, but standalone expressions are not permissible. To run Haskell code that's saved in a file, you would do so using a Haskell interpreter. Here is an example:

Let's say you have a file called `main.hs` with the following code:

```haskell
x = 21
y = 2 * x

main = print y
```

You can run this Haskell program in the terminal by typing `runhaskell main.hs`, which should output `42`.

### Haskell: Functions

Functions are the heart of Haskell and functional programming in general. Here's how we define a function in Haskell:

```haskell
double x = 2 * x
```

In this case, `double` is the name of the function, and `x` is the parameter. The expression `2 * x` is the body of the function.

A function can also take multiple parameters. For example:

```haskell
add x y = x + y
```

In this case, `add` is the function name, and `x` and `y` are the parameters. The body of the function is `x + y`.

Here's how you would call these functions:

```haskell
double 21   -- Outputs: 42
add 21 21   -- Outputs: 42
```

### Abstraction: The Essence of CS 131

The principle of abstraction is central to computer science and is closely related to the process of problem-solving. It involves simplifying complex systems by breaking them down into smaller, more manageable parts.

In functional programming, and Haskell specifically, abstraction is achieved through functions. By encapsulating specific tasks or computations inside functions, you can build complex systems from simple, reusable parts. This not only makes your code more readable and maintainable, but it also allows you to reason about your program at a higher level.

### Functional Programming: Definitions and Foundations

Functional programming is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data. It is a declarative programming paradigm, which means programming is done with expressions or declarations instead of statements.

Some of the core principles of functional programming include:
- **Immutability:** Once a data value is created, it cannot be changed. 
- **First-class and higher-order functions:** Functions in functional programming are first-class citizens, which means they can be passed as arguments to other functions, returned as values from other functions, and assigned to variables. A higher-order function is a function that takes one or more functions as arguments, returns a function as its result, or both.
- **Pure functions:** Pure functions are functions that, given the same input, will always return the same output, and they have no side effects (like changing external variables).
- **Recursion:** Since functional programming languages favor immutability and have no loops, they use recursion for tasks that would typically require iteration in imperative programming languages.

In the next lectures, we will dive deeper into these concepts and learn more about functional programming with Haskell.

That concludes the summary for today's lecture. Remember, there's a lot to learn when it comes to Haskell and functional programming, but with practice and patience, you will get the hang of it. Don't hesitate to ask questions if anything is unclear. Have a great day!

 
