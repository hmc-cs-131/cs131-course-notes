### CS 131: Programming Languages

# Lambda Calculus

Lambda Calculus is a formal system in mathematical logic that provides a foundation for understanding computation using functions. It was introduced by Alonzo Church in the 1930s as a way to investigate the notion of effective computability.

## Historical and Contextual Recap

Before diving deeper into Lambda Calculus, let's briefly recap its historical and contextual significance. Lambda Calculus emerged as part of the broader effort to develop formal systems and mechanical methods for mathematics and computation.

At the time, the fields of engineering, mathematics, and computer science were starting to intersect, giving birth to new ideas and approaches. Courses like Engineering Mathematics (CS105), Introduction to Programming (E115), Computer Organization and Systems (CS140), and Lambda Calculus (CS131) provided the necessary foundations for understanding computation from different perspectives.

### Computation is More Than Numbers

While early forms of computation focused on numerical calculations and algorithms, Lambda Calculus expanded the notion of computation to include functions and symbolic manipulation. It introduced a way to represent and reason about computations using functions as the fundamental building blocks.

This shift in perspective opened up new possibilities, allowing for the manipulation of functions and the exploration of higher-level concepts beyond mere numbers.

### Could we compute EVERYTHING?

The question of whether it is possible to compute everything has intrigued many great minds in the history of computer science and mathematics. Several prominent figures have expressed their thoughts on this matter:

- **David Hilbert**, a mathematician, expressed an optimistic viewpoint, believing that with the right methods and tools, all problems in mathematics could be solved.
- **Alonzo Church**, the creator of Lambda Calculus, disagreed with Hilbert's optimistic view. He demonstrated that there is no general-purpose algorithm that can determine if two lambda expressions are equivalent.
- **Alan Turing**, another influential figure in computer science, also reached a similar conclusion. He proved the undecidability of the Halting Problem, showing that there are limits to what can be computed.

These perspectives highlight the inherent complexity and limitations of computation.

### Lambda Calculus and Turing Machines

Lambda Calculus and Turing Machines are two foundational models of computation. While Turing Machines focus on the mechanics of computation and provide a theoretical framework for understanding computation in terms of tape manipulation and state transitions, Lambda Calculus approaches computation from a functional perspective.

Alan Turing's Machines, introduced in 1936, are theoretical devices capable of performing any computation that can be algorithmically described. Turing showed that it is impossible to have a general procedure that determines whether an arbitrary Turing Machine halts.

On the other hand, Alonzo Church's Lambda Calculus, developed in 1935, provides a formal system for manipulating symbols based on functions. Church demonstrated that there is no general-purpose algorithm that can determine if two lambda expressions are equivalent.

These two models of computation, while different in their approach and formalism, highlight the fundamental limits and challenges in determining the computability of certain problems.

### Up and Down the Ladder of Abstraction

Understanding computation involves navigating different levels of abstraction. The ladder of abstraction provides a framework for visualizing these levels:

- At the lowest level, we have **Turing Machines**. They are simple, low-level models that operate on bits and perform basic operations.
- Moving up, we encounter the **von Neumann Architecture**, which is the foundation of most modern computers. It consists of a CPU, memory, and I/O systems.
- Above that, we have **Assembly Language**, which represents machine instructions using mnemonics. It provides a closer connection to the underlying machine language.
- **Imperative Languages** like C/C++ operate at a low level, offering manual memory management and direct control over hardware.


- **Higher-level Languages** such as Python provide abstractions and handle memory management automatically. They focus more on expressing algorithms and logic rather than low-level details.
- **Functional Languages** like Racket treat functions as first-class citizens, allowing functions to be manipulated and composed as data.
- **Pure Functional Languages** like Haskell eliminate mutable state altogether, emphasizing immutability and function purity.

Moving up and down this ladder of abstraction allows us to explore different levels of expressiveness, control, and simplicity in programming languages and systems.

## Haskell: The Vehicle, Not the Focus

In this class, Haskell serves as the vehicle for exploring various programming language concepts. The focus is not solely on Haskell itself but on the underlying concepts of functional programming, data representation, parsing, and interpreters.

While Haskell is a powerful and expressive language, the principles and ideas learned can be applied to other languages and systems. Haskell provides a unique environment for understanding and experimenting with these concepts, offering a concise and elegant syntax.

## Some Topics in this Class

Throughout the course, several topics will be covered, each providing valuable insights into programming language concepts. Here are some of the topics presented in a bumper sticker style:

- **Functional Programming**: Functions are treated as data, enabling powerful abstractions and expressive programming.
- **Pattern Matching**: Leveraging the structure of data for manipulation and analysis, making code concise and clear.
- **Representing Your Data**: Exploring different data structures and their representation in a functional programming style.
- **Parsing**: Transforming characters into structured programs, allowing for the creation of interpreters and compilers.
- **Interpreters**: Understanding how programs are executed by interpreting their semantics.
- **Abstraction**: The art of doing more with less code, reducing complexity and increasing modularity.
- **Types**: Ensuring that computations produce the desired kind of results and catching errors at compile-time.
- **Lambda Calculus**: Exploring the essence of computation through lambda abstractions and function manipulations.

These topics provide a comprehensive understanding of programming language concepts, preparing students to think critically and design elegant solutions to complex problems.

## Lambda Calculus: Introduction

Lambda Calculus is a formal system that operates on symbols, specifically functions. It serves as a foundation for understanding computation using functions as the central element.

The term "lambda" refers to the Greek letter λ, which Alonzo Church used to symbolize function abstraction in Lambda Calculus.

### Lambda Calculus: Syntax

Lambda Calculus expressions are built using a simple syntax consisting of three types of expressions:

- **Variables**: Represented by lowercase alphabetic symbols (a, b, c, ..., z). Variables are used to bind values and represent arguments in lambda abstractions.
- **Function Application**: Expressions of the form (expr1 expr2), where expr1 represents the function and expr2 represents the argument being applied to the function.
- **Lambda Abstraction**: Expressions of the form (λ var . expr), where λ denotes the lambda symbol, var represents the parameter being bound, and expr represents the body of the function.

The lambda symbol λ and the dot (.) are used to construct lambda abstractions, allowing for the definition of anonymous functions.

Lambda Calculus expressions are deliberately kept simple, providing a foundation for expressing complex computations using only these basic constructs.

### Lambda Calculus: Examples

Lambda Calculus expressions can be as simple as a single variable or as complex as nested abstractions and function applications. Here are some examples:

- (λx.x): An identity function that returns its argument as it is.
- (λx.y): A function that ignores its argument and always returns y.
- (x y): Applying the function x to the argument y.
- (x x): Applying the function x to itself.
- z

: A variable representing a specific value.
- ((λx.x) a): Applying the identity function to the argument a.

These examples showcase the versatility and expressiveness of Lambda Calculus in representing computations and functions.

### Lambda Calculus: Vocabulary

To understand and reason about Lambda Calculus expressions, it's essential to be familiar with the following vocabulary:

- **Parameter**: The variable used in a lambda abstraction, representing the argument being bound.
- **Bound Variable**: A variable that is bound within the scope of a lambda abstraction.
- **Body**: The expression following the lambda abstraction, representing the function's behavior.
- **Lambda Abstraction**: The process of defining an anonymous function using the λ symbol, parameter, and body.
- **Closed Expression**: A lambda abstraction where all variables are bound within the expression.
- **Free Variable**: A variable that appears outside the scope of a lambda abstraction.
- **Open Expression**: A lambda abstraction with free variables, indicating dependencies on variables outside the function definition.

Understanding these terms helps in analyzing Lambda Calculus expressions and reasoning about their behavior.

### Lambda Calculus: β-Reduction, α-Equivalence, Normal Forms

In Lambda Calculus, β-reduction, α-equivalence, and normal forms are important concepts that allow us to manipulate and simplify lambda expressions.

**β-Reduction**: β-reduction is the process of applying a function to an argument by substituting the argument for the parameter in the function's body. It allows us to evaluate lambda expressions and simplify them further.

For example, given the lambda expression `(λx.x) a`, we can perform β-reduction as follows:

```
(λx.x) a  ⟶   a
```

The expression `(λx.x) a` represents a function `(λx.x)` applied to an argument `a`. By substituting `a` for the parameter `x` in the body of the function `(λx.x)`, we obtain the result `a`.

Another example is the β-reduction of a nested lambda expression:

```
((λx.(λy.x)) a)  ⟶  (λy.a)
```

In this case, we have a function `(λx.(λy.x))` applied to an argument `a`. By substituting `a` for `x` in the body of the outer function and removing the redundant inner function, we obtain the result `(λy.a)`.

**α-Equivalence**: α-equivalence refers to the notion of renaming variables in a lambda expression without changing its meaning. It allows us to consider two lambda expressions equivalent even if they differ in variable names.

For example, consider the lambda expressions `(λx.x)` and `(λy.y)`. These two expressions are α-equivalent because we can rename `x` to `y` in the first expression to obtain the second expression. Both expressions represent the identity function, which returns its argument unchanged.

However, not all lambda expressions are α-equivalent. If a variable is free in one expression but bound in another, they are not considered α-equivalent.

**Normal Form**: A lambda expression is said to be in normal form if it cannot undergo any further β-reduction. In other words, a lambda expression is in normal form when we can no longer simplify it using β-reduction.

For example, consider the expression `(λx.x) z`. We can perform β-reduction as follows:

```
(λx.x) z  ⟶  z
```

The resulting expression `z` is in normal form because no further β-reduction is possible. It represents the value `z` without any additional computations.

On the other hand, some lambda expressions do not have a normal form. A well-known example is the expression `(λx.(x x)) (λx.(x x))`. It leads to an infinite loop of self-application and cannot be reduced to a normal form.

Understanding β-reduction, α-equivalence, and normal forms allows us to manipulate and reason about lambda expressions effectively in Lambda Calculus.

### Lambda Calculus: Useful Functions

Lambda Calculus allows us to define and manipulate various functions. Here are some notable ones:

- **Identity Function**: (λx.x) returns its argument as it is, preserving its value.
- **Constant Functions**: Functions like (λx.y) always return a constant value, ignoring their argument.
- **Nested Functions and Applications**: Combining lambda abstractions and function applications to create more complex computations.

These functions demonstrate the flexibility and power of Lambda Calculus in defining different behaviors and operations.

### Useful Encodings: Simple Logic and Data Structures

Lambda Calculus provides a framework for encoding logical operations and basic data structures. Here are some examples:

**Booleans**: Booleans are fundamental in programming logic. In Lambda Calculus, we can represent booleans using lambda abstractions and if-then-else expressions. We define two constants:

- **TRUE**: Represented as (λa.(λb.a)), which takes two arguments and returns the first argument.
- **FALSE**: Represented as (λa.(λb.b)), which takes two arguments and returns the second argument.

These boolean representations allow us to perform logical operations using lambda abstractions and function applications. For example, to define the conjunction (AND) operation:

- **Conjunction (AND)**: We define the AND operation as a lambda abstraction that takes two boolean arguments and returns the result of logical conjunction. The lambda expression for AND can be defined as:

  ```
  AND ≜ (λa.(λb.((a b) FALSE)))
  ```

  The AND function takes two boolean arguments, `a` and `b`, and applies `a` to `b` (function application). If `a` is FALSE, the result is always FALSE. Otherwise, it returns the value of `b`, which represents the logical conjunction.

- **Disjunction (OR)**: Similar to the AND operation, we can define the OR operation as a lambda abstraction that takes two boolean arguments and returns the result of logical disjunction. The lambda expression for OR can be defined as:

  ```
  OR ≜ (λa.(λb.((a TRUE) b)))
  ```

  The OR function takes two boolean arguments, `a` and `b`, and applies `a` to TRUE. If `a` is TRUE, the result is always TRUE. Otherwise, it returns the value of `b`, representing the logical disjunction.

- **Negation (NOT)**: To negate a boolean value, we define the NOT operation as a lambda abstraction that takes a boolean argument and returns the negated value. The lambda expression for NOT can be defined as:

  ```
  NOT ≜ (λb.((b FALSE) TRUE))
  ```

  The NOT function takes a boolean argument `b` and applies it to FALSE. If `b` is FALSE, the result is always TRUE. Otherwise, it returns FALSE, representing the logical negation.

These encodings of logical operations in Lambda Calculus allow us to reason about boolean logic and perform basic logical computations.

**Pairs**: Pairs are a simple data structure that allows us to combine two values into a single entity. In Lambda Calculus, we can encode pairs using lambda abstractions and function applications. We define the following operations:

- **MKPAIR**: MKPAIR is a lambda abstraction that takes two values `x` and `y` and returns a pair representation. The lambda expression for MKPAIR can be defined as:

  ```
  MKPAIR ≜ (λx.(λy.(λb.((b x) y))))
  ```

  MKPAIR takes two arguments, `x` and `y`, and creates a lambda abstraction that represents the pair. The resulting function takes a boolean argument `b` and applies it to `x` and `y` accordingly, returning the desired component of the pair.

- **FST**: FST is a lambda abstraction that takes a pair and returns its first component. The lambda expression for FST can be defined as:

  ```
  FST ≜ (λp.(p TRUE))
  ```

  FST takes a pair `p` and applies it to TRUE. As per the MKPAIR encoding, applying TRUE to a pair retrieves its first component.

These encodings demonstrate how Lambda Calculus can represent complex concepts using simple constructs and function manipulations.

Lambda Calculus serves as a foundation for understanding computation and exploring the fundamental principles of programming languages and systems. Its simplicity and expressive power make it a valuable tool for reasoning about computations and defining functions.