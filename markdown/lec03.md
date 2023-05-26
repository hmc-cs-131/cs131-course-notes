# CS 131: Programming Languages

## Functions = Values

### Today's Topics
- Referential transparency
- Lazy evaluation
- Operators
- Currying
- Higher-order functions
- Composition

## Recap: Expressions, Functions, and Functional Programming

In this course, we have been exploring the world of programming languages, particularly focusing on expressions, functions, and the principles of functional programming. Before we delve into today's topics, let's quickly review some important concepts.

### Some Vocabulary
To understand the upcoming topics better, let's familiarize ourselves with a few key terms:
- Expression (noun): An expression refers to a "piece of computation," such as `1 + 2` or `f 3`.
- Evaluate (verb): When we evaluate an expression, we attempt to compute its result.
- Side effect (noun): During evaluation, a side effect refers to anything that changes the state. Examples of side effects include modifying the value of a variable or printing a message to the screen.
- Referential transparency: A sub-expression within an expression is said to be referentially transparent if it can be replaced with its result without affecting the overall result of the surrounding expression.
- Pure expression: A pure expression is one that has no side effects.
- Purely functional programming language: A programming language is considered purely functional when its computation relies solely on the evaluation of pure expressions.

### The Advantages of Purely Functional Languages
As we have learned, Haskell is an example of a purely functional programming language. In Haskell, all "variables" are treated as constants since side effects are not allowed. This characteristic of purely functional languages makes programs written in them easier to reason about. By disallowing side effects, we eliminate the uncertainty and complexity that arises from state changes. However, this also means that we cannot directly print information to the screen. While there are ways to achieve output in Haskell, we'll explore those concepts later in the course. For now, let's focus on one key benefit of referential transparency: laziness!

## Lazy Evaluation

### Some Vocabulary
Before we dive into lazy evaluation, let's introduce a few terms:
- Eager (or strict) evaluation: In eager evaluation, subexpressions are evaluated first. This form of computation is likely the most familiar to you.
- Lazy evaluation: In contrast, lazy evaluation only evaluates subexpressions when they are actually needed.

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
- Application (noun) or apply (verb): The use of

 an operator in an expression.
- Ambiguous (adjective): Something that can have multiple meanings or interpretations.
- Disambiguate (verb): To resolve an ambiguity by choosing one specific meaning or interpretation.
- Precedence (noun): The rule that determines how to disambiguate an expression containing applications of different operators. An operator with higher precedence is applied before an operator with lower precedence.
- Associativity (noun): The rule that disambiguates an expression with multiple applications of the same operator. There are two types of associativity:
  - Left associativity: Resolves the ambiguity by evaluating the left-most application first.
  - Right associativity: Resolves the ambiguity by evaluating the right-most application first.

### Precedence and Associativity in Haskell
In Haskell, operators have specific properties based on their precedence and associativity. Here are some examples:
- Function application: It is left associative, which means the leftmost application is evaluated first.
- Exponentiation: It is right associative, which means the rightmost application is evaluated first.
- Multiplication, division: They are left associative, evaluated from left to right.
- (In)equality: They are left associative, evaluated from left to right.
- Logical and: It is left associative, evaluated from left to right.
- Logical or: It is left associative, evaluated from left to right.

To handle expressions with operators effectively, it's essential to understand these properties.

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

All Haskell functions take only one argument!
This statement may seem surprising at first, but it holds true. Even functions with multiple parameters in Haskell are curried.

For instance, consider the following function:
```haskell
average :: Double -> Double -> Double
average x y = (x + y) / 2
```

Although `average` appears to take two arguments, it can be thought of as a series of functions, each taking a single argument. This concept

 is known as currying.

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

## Composition

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
