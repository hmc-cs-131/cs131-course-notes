# HMC CS 131: Programming Languages

## Lambda Calculus Encodings

### Functional Encoding of Sets

In lambda calculus, we can encode sets using functional encodings. The idea is to represent a set as a function that takes an argument and evaluates to either `True` or `False` depending on whether the argument is in the set or not.

For example, in Haskell, we can define boolean functions for `NOT`, `AND`, `OR`, as well as functions for creating pairs (`MKPAIR`), extracting the first component (`FST`), and extracting the second component (`SND`).

```haskell
NOT ≜ (λb.((b FALSE) TRUE))
TRUE ≜ (λa.(λb.a))
FALSE ≜ (λa.(λb.b))
AND ≜ (λa.(λb.((a b) FALSE)))
OR ≜ (λa.(λb.((a TRUE) b)))
MKPAIR ≜ (λx.(λy.(λb.((b x) y))))
FST ≜ (λp.(p TRUE))
SND ≜ (λp.(p FALSE))
```

These definitions provide a way to perform logical operations and manipulate pairs in lambda calculus.

### Encoding Sets as Functions

We can represent sets as functions in lambda calculus. The idea is that a set `S` can be thought of as a function that takes an argument `x` and evaluates to `True` if `x` is in the set, and `False` otherwise.

In Haskell, we can define functions for `empty` set, `universe` set, `singleton` set, as well as operations like `complement`, `union`, and `intersection` on sets.

```haskell
empty _ = False
universe _ = True
singleton = (==)
complement s = not . s
union s t x = (s x) || (t x)
intersection s t x = (s x) && (t x)
```

Similarly, in lambda calculus, we can encode these set operations using lambda functions.

```plaintext
empty = (λx. False)
universe = (λx. True)
singleton = (λx. (λy. ((Equal x) y)))  # Equal from HW8
complement = (λs. (λx. (Not (s x))))
union = (λs. (λt. (λx. ((Or (s x)) (t x)))))
intersection = (λs. (λt. (λx. ((And (s x)) (t x)))))
```

These encodings allow us to perform set operations using lambda calculus.

### Set Theory Paradox: Russell's Set

One of the famous paradoxes in set theory is Russell's Paradox. It arises when we consider a set `R` defined as follows:

```
R = { x | x ∉ x }
```

The paradox arises when we ask whether `R` is an element of itself (`R ∈ R`). If `R` is an element of itself, then it should not be an element of itself, and if it is not an element of itself, then it should be an element of itself. This leads to a contradiction.

In lambda calculus, we can encode Russell's set as `R = (λx. (Not (x x)))`. When we try to beta-reduce this expression, we encounter an infinite recursion:

```
(R R) = ((λx. (Not (x x))) R) = (Not (R R))
```

This infinite recursion leads to the paradox.

### A Puzzle: How to Write a Recursive Anonymous Function?

In functional

 programming, recursion is a powerful technique. We often write recursive functions to solve problems. However, when working with anonymous functions, it is not immediately obvious how to write a recursive anonymous function.

For example, let's say we want to write a recursive anonymous function that calculates the factorial of a number. In Haskell, we can define the factorial function recursively as follows:

```haskell
fact n = if n == 0 then 1 else n * fact (n - 1)
```

But how can we write the factorial function using a recursive anonymous function?

### The Y Combinator

The Y combinator is a higher-order function that plays a fundamental role in lambda calculus. It enables the definition of recursive functions without the need for named function definitions. The Y combinator allows us to achieve recursion in anonymous functions, which is particularly useful in languages like lambda calculus where explicit recursion is not built into the language itself.

The Y combinator is defined as:

```
Y = (λf. ((λx. (f (x x))) (λx. (f (x x)))))
```

At first glance, the definition of the Y combinator may seem confusing. However, it embodies a clever mechanism that creates a recursion "loop" within a function expression.

To understand how the Y combinator works, let's break down its components:

- `(λf. ...)` defines a function that takes a function `f` as an argument.
- `((λx. (f (x x))) (λx. (f (x x))))` represents the recursion mechanism.

Within the recursion mechanism, `(λx. (f (x x)))` is responsible for creating a function that can call `f` on itself. This self-application is achieved by applying `x` to `x`. However, since the function `(λx. (f (x x)))` is itself the argument for `x`, we end up with `(f (x x))`.

Next, `(λx. (f (x x)))` is also applied to `(λx. (f (x x)))`, effectively passing the self-applicable function to itself. This creates the recursive loop necessary for recursion.

By applying the Y combinator to a function `f`, we obtain a recursive function that repeatedly applies `f` to itself. This recursion allows for the construction of complex computations and the definition of functions that depend on their own results.

Using the Y combinator, we can define recursive functions in lambda calculus without explicit naming. This is particularly useful in lambda calculus, where named function definitions are not available.

### Recursive Function Example: Factorial

Let's illustrate the usage of the Y combinator with an example: computing the factorial function.

In Haskell, the factorial function can be defined using recursion as follows:

```haskell
fact n = if n == 0 then 1 else n * fact (n - 1)
```

Using the Y combinator, we can write the factorial function in lambda calculus as:

```
fact = Y (\f. \n. if n == 0 then 1 else n * f (n - 1))
```

Here's how the Y combinator works in this context:

- The function `\f. \n. if n == 0 then 1 else n * f (n - 1)` represents the factorial computation with a parameter `f` for recursive calls.
- Applying the Y combinator to this function: `Y (\f. \n. if n == 0 then 1 else n * f (n - 1))` creates a recursive function that can call itself using `f`.

By defining the factorial function with the Y combinator, we can now compute factorials in lambda calculus without needing explicit recursion or named functions.

### The Power of the Y Combinator

The Y combinator's ability to introduce recursion in anonymous functions is powerful. It allows us to solve recursive problems and perform computations that would otherwise require named functions or explicit recursion.

With the Y combinator, we can define a wide range of recursive functions in lambda calculus, from simple arithmetic calculations to complex data manipulations.

However, it's worth noting that the Y combinator is not limited

 to factorial calculations alone. It can be applied to any function that requires recursion. By applying the Y combinator to a suitable function expression, we can achieve recursion and solve a variety of problems within the lambda calculus framework.

### Recursion Recipe with the Y Combinator

To use the Y combinator to define a recursive function, follow this recipe:

1. Define the function expression using a parameter (e.g., `exprs`).
2. Wrap the expression with the Y combinator: `(Y (\f. exprs f exprs f exprs ... f exprs))`.

By following this recipe, you can define recursive functions in lambda calculus using the Y combinator.

The Y combinator is a fascinating concept that showcases the expressive power of lambda calculus. It highlights the ability to achieve recursion without explicit recursion constructs or named functions, opening up new avenues for computation within the lambda calculus paradigm.

