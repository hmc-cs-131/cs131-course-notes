# Code as Data, Evaluating Expressions

In this chapter, we will cover functional programming concepts, Haskell programming basics, and the idea of representing code as data. We will also discuss different types of inputs and outputs that a program can have.

## Outline
1. [Inputs and Outputs of Programs](#inputs-and-outputs-of-programs)
2. [Code as Data](#code-as-data)
3. [Representing Expressions](#representing-expressions)
4. [Expressions and Statements](#expressions-and-statements)


## Inputs and Outputs of Programs

Different programs can have different types of inputs and outputs. Here are some examples:

1. **Program 1**: Takes a list of integers as input and returns their average.
2. **Program 2**: Takes coordinates as input and returns the shortest path.
3. **Program 3**: Takes a text file as input and returns the spelling errors found in it.
4. **Program 5**: Takes source code as input and returns the number of lines of code.
5. **Program 6**: Takes source code as input and returns nicely formatted code.
6. **Program 7**: Takes source code as input and returns binary machine code.
7. **Program 8**: Takes source code as input and returns the result of running the code.

## Code as Data

An essential concept in programming languages is that **code can be treated as data**. This idea allows for the manipulation and transformation of code, enabling various tasks such as code optimization and metaprogramming.

## Representing Expressions

To represent expressions using data types in Haskell, we can create algebraic data types to model different operations and values.

For example, consider the following mathematical expressions:

- `(2 + 2) * 7 - 11`
- `15 - 3`
- `5 + 4 + 3 + 2 + 1`

To represent these expressions in Haskell, we can create an algebraic data type like this:

```haskell
data Expr
  = Val Integer
  | Add Expr Expr
  | Subtract Expr Expr
  | Multiply Expr Expr
  deriving (Show)
```

## Expressions and Statements

### Terminology

- **Expression**: A computation that calculates a value. In functional programming, computation means evaluating expressions.
- **Statement**: A computation that is performed for its effect (modifying the state of the system). Statements may change values, but they do not, themselves, have a value. In imperative programming, computation means executing a series of statements.
- **Side-Effect**: Anything an expression does besides calculating a value. Functional languages allow few (Racket) or no (Haskell) side-effects.

### Identifying C and C++ Expressions and Statements

#### Example 1:

```c
10 * z + 4
```

This is an expression, as it evaluates to a value.

#### Example 2:

```c
x++;
