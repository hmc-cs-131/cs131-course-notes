### CS 131: Programming Languages

# Functions = Values

## Recap: Expressions, Functions, and Functional Programming

In this course, we have been exploring the world of programming languages, particularly focusing on expressions, functions, and the principles of functional programming. Before we delve into today's topics, let's quickly review some important concepts.

### Some Vocabulary
To understand the upcoming topics better, let's re-familiarize ourselves with a few key terms:

- **Expression** (noun): A "piece of computation" in functional programming, such as `1 + 2` or `f 3`.
- **Evaluate** (verb): The process of attempting to compute the result of an expression.
- **Termination**: The outcome of evaluating an expression, which can either **terminate with a result** or **diverge** (run forever).
- **Side effect** (noun): Any action during expression evaluation that changes the state of the program or the external environment. Examples include modifying a variable's value or printing output.
- **Referentially Transparent**: A property of a sub-expression that allows it to be replaced with its result without impacting the overall result of the surrounding expression.
- **Pure Expression**: An expression that has no side effects and produces a result solely based on its inputs.
- **Purely Functional Programming Language**: A programming language, such as Haskell, where computation is achieved by evaluating only pure expressions.

### Haskell is a Purely Functional Language!
In Haskell, being a purely functional programming language has several implications:

- **Immutable Variables**: In Haskell, all "variables" are actually constants. Once a value is assigned, it cannot be changed. This immutability promotes a more predictable and reliable programming style.

- **No Side Effects**: Haskell enforces the absence of side effects. Side effects refer to actions that modify the state of the program or the external environment. By disallowing side effects, Haskell programs become more reliable and easier to reason about.

- **Enhanced Program Reasoning**: With the absence of side effects, Haskell programs become amenable to formal reasoning techniques. Program correctness can be verified more easily, leading to more robust and bug-free software.

- **Limitations on Printing**: Due to the prohibition of side effects, direct printing to the screen, which is typically a side effect, is not allowed in Haskell. However, it is possible to achieve similar functionality through more advanced techniques, though this requires a deeper understanding of the language.

- **Referential Transparency**: One of the key features enabled by referential transparency in Haskell is lazy evaluation. Haskell allows expressions to be evaluated only when their results are actually needed, leading to more efficient and flexible computation.

In summary, Haskell's purely functional nature brings advantages such as immutability, absence of side effects, improved program reasoning, and the ability to leverage referential transparency and lazy evaluation for more elegant and efficient programming.

## Lazy Evaluation

### Some Vocabulary
Before we dive into lazy evaluation, let's introduce a few terms:
- **Eager (or strict) evaluation**: Eager (or strict) evaluation refers to a form of computation where subexpressions are evaluated before they are assigned or used in function calls. In this evaluation strategy, expressions are computed before they are assigned to variables, and arguments are evaluated before a function call is made. For example, in the expression x = 1 + 2, the subexpression 1 + 2 is evaluated first, resulting in x = 3. Similarly, in the function call f(1 + 2, 3 * 4), the subexpressions 1 + 2 and 3 * 4 are evaluated before the function is called with the computed values. This form of computation is likely the most familiar to you.
- **Lazy evaluation**: Lazy evaluation refers to a form of computation where subexpressions are evaluated only when their results are needed. In this evaluation strategy, expressions are not immediately evaluated when assigned to variables. Similarly, arguments are not evaluated before a function call is made. Instead, they are evaluated only when they are actually used within the function. For example, in the expression x = 1 + 2, the subexpression 1 + 2 is not immediately evaluated. Similarly, in the function ignoreFirstArgument, the arguments (1 + 2) and (3 * 4) are not evaluated before the function call. They are evaluated only when needed, such as when ignoreFirstArgument uses the values (1 + 2) and (3 * 4) in the expression 3 * 4.

### Benefits of Lazy Evaluation
Lazy evaluation brings several advantages to the table:
1. No unnecessary computation: With lazy evaluation, a program only evaluates what is necessary. This approach minimizes redundant calculations, leading to more efficient execution.
2. Fewer redundant computations: Thanks to referential transparency, Haskell can "remember" the results of certain computations, avoiding redundant evaluations.
3. Evaluation can happen in parallel: Without side effects, independent expressions can be evaluated in any order, allowing for potential parallel execution.
4. Efficient handling of large (even infinite) data structures: Lazy evaluation allows Haskell programs to construct and operate on large data structures more efficiently. The program can choose to evaluate only the parts that are needed, instead of constructing the entire structure.

With these benefits in mind, let's explore operators in Haskell.

## Operators

### Their Properties and How They Work in Haskell

Consider the expression `5 - 1 - 2 * 2`. How do we know that it is interpreted as `(5 - 1) - (2 * 2)` and not `((5 - 1) - 2) * 2` or `(5 - (1 - 2)) * 2`?

### Some Vocabulary
To understand how expressions with operators are interpreted, let's introduce a few terms:
- **Operator** (noun): A symbol or keyword that represents a specific operation to be performed on one or more operands. It defines the action or manipulation to be carried out in an expression.
- **Operand** (noun): A value or entity that is operated upon by an operator. It can be a variable, constant, or another expression. The operator uses the operands to perform a specific computation or transformation.
- **Application** (noun) or **apply** (verb): The use of an operator in an expression.
- **Ambiguous** (adjective): Something that can have multiple meanings or interpretations.
- **Disambiguate** (verb): To resolve an ambiguity by choosing one specific meaning or interpretation.
- **Precedence** (noun): The rule that determines how to disambiguate an expression containing applications of different operators. An operator with higher precedence is applied before an operator with lower precedence.
- **Associativity** (noun): The rule that disambiguates an expression with multiple applications of the same operator. There are two types of associativity:
  - **Left associativity**: Resolves the ambiguity by evaluating the left-most application first.
  - **Right associativity**: Resolves the ambiguity by evaluating the right-most application first.

### Precedence and Associativity in Haskell
In Haskell, operators have specific properties based on their precedence and associativity. Here are some examples:

| Operation name(s)     | Operator(s)       | Associativity |
|-----------------------|-------------------|---------------|
| function application  |                   | left          |
| exponentiation        | ^, **             | right         |
| multiplication, division | *, /           | left          |
| (in)equality          | ==, /=, <, >, <=, >= | left         |
| logical and           | &&                | left          |
| logical or            | \|\|              | left          |

The operators are listed in order of precedence, with operators with highest precedence at the top and operators with lowest precendence at the bottom.

### Advanced Haskell Operators

#### Infix Notation and Fixity Declarations

Did you know that operators are just functions in Haskell? Let's explore this idea further.

Operators are Functions:
In Haskell, a binary operator is essentially a function that takes two arguments. We can call operators just like any other function. However, if the operator is a symbol, such as `+`, we need to put the symbol in parentheses when treating it as a function.

Examples:
```haskell
(+) 1 2        -- Result: 3
(&&) :: Bool -> Bool -> Bool   -- Type of operator &&
```

Functions as Operators:
If a binary operator is a two-argument function, it can also be used as an operator. Haskell provides infix notation to treat a two-argument function like an operator. In infix notation, the function is surrounded by tick marks (`)`, and its arguments are placed on either side of the function.

Examples:
```haskell
4 `div` 2      -- Result: 2
17 `mod` 12    -- Result: 5
```

#### Fixity Declaration
In Haskell, a fixity declaration allows us to define the associativity and precedence for custom operators. By specifying fixity, we can control how expressions involving these operators are evaluated.

For example, let's define the `addMod60` operator with left associativity and the same precedence as the `mod` operator:
```haskell
infixl 7 `addMod60`

addMod60 :: Integer -> Integer -> Integer
addMod60 x y = (x + y) `mod` 60
```

By understanding operator properties and utilizing fixity declarations, we can manipulate expressions effectively.

Now, let's move on to exploring currying and higher-order functions.

## Currying & Higher-order Functions

In Haskell, all functions are designed to take **only one argument**, which might seem counterintuitive at first. This concept, known as _currying_, allows functions with multiple parameters to be treated as a sequence of functions, each accepting a single argument.

Let's consider the example of the `average` function:
```haskell
average :: Double -> Double -> Double
average x y = (x + y) / 2
```

Although it appears that `average` takes two arguments, it can be understood as a curried function. When we call `average` with the first argument `x`, it returns a new function that takes the second argument `y` and produces the final result. This means that we can partially apply `average` by supplying only the first argument and obtain a new function that expects the second argument.

For example, if we call `average 3.0`, we get a new function `average 3.0 :: Double -> Double`, which takes another `Double` as an argument and calculates the average with `3.0` as the first argument. This flexibility of currying allows us to create specialized functions by partially applying arguments and reuse them in various contexts.

### Some Vocabulary
Before we delve deeper, let's introduce a couple of terms:
- Curried function (noun): A multi-argument function that takes its arguments one at a time. In Haskell, all multi-argument functions are curried.
- Higher-order function (noun): A function whose input or output is another function. A programming language that supports higher-order functions is said to have first-class functions.

Currying in Action:
Let's consider the function `increment`:
```haskell
increment :: Integer -> Integer
increment n = 1 + n
```

Although it may appear as if `increment` takes a single argument, we can interpret it as a curried function. The `1 + n` expression is actually equivalent to `(+) 1 n`. This understanding allows us to pass `increment` as a function to other functions.

Higher-order Functions:
Now, let's explore the concept of higher-order functions, which play a significant role in functional programming. A higher-order function is one that either takes a function as an input or returns a function as output. In a programming language with first-class functions, functions are treated as values.

Consider the function `compose`, which combines two functions `g` and `f`:
```haskell
compose :: (a -> b) -> (b -> c) -> a -> c
compose g f n = g (f n)
```

Here, `compose` takes two functions `g` and `f` as inputs, along with a value `n`. It applies `f` to `n`, then applies `g` to the result, producing the final output.

Understanding currying and higher-order functions allows us to write concise and modular code. We'll explore these concepts further in the upcoming lessons.

Now, let's move on to the final topic: function composition.

## Function Composition

Function composition is a powerful operation that allows us to combine simple functions to create more complex ones. Let's see it in action.

Consider the following functions:
```haskell
increment :: Integer -> Integer
increment n = 1 + n

double :: Integer -> Integer
double n = 2 * n

square :: Integer -> Integer
square n = n ^ 2
```

We can use function composition to create new functions by combining these simpler functions.

### Function Composition in Haskell
In Haskell, function composition is denoted by the `(.)` operator. It takes two functions `g` and `f` and returns a new function `h` such that `h(x) = g(f(x))`.

Let's explore some examples:
```haskell
(increment . double) 1    -- Result: 3
(double . increment) 1    -- Result: 2
(increment . square) 1    -- Result: 2
```

In these examples, `(.)` composes the functions `increment`, `double`, and `square` to produce new functions. We can chain these compositions to create more complex transformations.

Function composition allows us to write elegant and concise code. By breaking down complex operations into smaller, reusable functions, we can improve code modularity and readability.

In summary, by understanding currying, higher-order functions, and function composition, we gain powerful tools for creating flexible and modular code in Haskell.
