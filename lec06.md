# CS 131: Programming Languages

## Code as Data, Evaluating Expressions

In this lecture, we explore the concept of code as data and delve into the evaluation of expressions. We will cover various topics, including the representation of abstract syntax, syntax and semantics, concrete and abstract syntax, and the evaluation of expressions with variables.

### CS131: Past, Present, Future

To understand the current landscape of CS131, it is essential to look back at its historical and social context. Influential figures such as Babbage, Lovelace, Turing, and Church paved the way for the development of computer science. Functional programming concepts, such as functions as values, higher-order functions, pattern matching, recursion, recursive data structures, and Haskell programming basics, form the foundation of CS131.

### What kinds of inputs/outputs can a program have?

Before delving into code as data, let's examine the various types of inputs and outputs that programs can handle. These examples will help us understand the versatility of programs:

- **Program 1:** Input: List of integers, Output: Average of the numbers
- **Program 2:** Input: Coordinates, Output: Shortest path
- **Program 3:** Input: Text file, Output: Spelling errors
- **Program 6:** Input: Source code (representation of a program), Output: Nicely formatted code
- **Program 7:** Input: Source code (representation of a program), Output: Binary machine code
- **Program 8:** Input: Source code (representation of a program), Output: Value (result of executing the program)

### Code as Data

The fundamental concept we will explore is "code is data." In programming, we can treat code as structured data, similar to other data types we manipulate in our programs. By representing code as data, we gain the ability to analyze, transform, and manipulate it programmatically.

### Syntax and Semantics

To understand code fully, we need to distinguish between syntax and semantics. 

- **Syntax** refers to what the programmer writes or is allowed to write. It encompasses the rules and structure of the programming language. For example, in C++, the `^` symbol is a valid binary operator.
- **Semantics** deals with the meaning and behavior of code. It describes how the code is interpreted and executed. For instance, the `^` operator, when applied to two integers, performs bitwise exclusive-or.

Attaching meaning (semantics) to symbols (syntax) is a crucial aspect of programming. It involves bridging the gap between the symbols we write in code and their intended interpretations. Linguistics, semiotics, and various branches of philosophy, such as the philosophy of AI and philosophy of mind, delve into the complexities of symbol grounding and meaning.

### Concrete and Abstract Syntax

To work with code effectively, we need to understand the distinction between concrete and abstract syntax.

- **Concrete syntax** refers to the code as written by the programmer. It encompasses the keywords, punctuation, and specific character sequences that make up the code. Concrete syntax allows us to write programs in a human-readable form.
- **Abstract syntax** captures the essential structure and meaning of the code, stripped of unnecessary details. It represents programs as structured data, typically in the form of trees. Abstract syntax provides a clear and unambiguous representation of code, facilitating manipulation and analysis.

When multiple concrete syntaxes map to the same abstract syntax, we can employ techniques like parsing and pretty printing to ensure consistency in representing and displaying code. The abstract syntax tree (AST) focuses on the relevant structure of the code while ignoring irrelevant details.

### Representing Abstract Syntax

In representing expressions using data types in Haskell, we aim for an elegant and effective approach. Let's consider some examples

 in mathematical and racket-style syntax:

In math syntax:
- (2 + 2) * 7 - 11
- 15 - 3
- 5 + 4 + 3 + 2 + 1

In racket-style syntax:
- (minus (times (plus 2 2) 7) 11)
- (minus 15 3)
- (plus 5 (plus 4 (plus 3 (plus 2 1))))

To represent abstract syntax, we have several options. Let's explore some of them:

- **Option 1 (Wrong!):** Using `Double` for numerical values and separate data constructors for each operation (Plus, Minus, Times, Divide). However, this approach lacks a label for the case when a numerical value is encountered.

- **Option 2 (Inelegant!):** Adding a separate data constructor (Num) for numerical values, along with data constructors for each operation. This approach introduces redundancy and requires additional pattern matching.

- **Option 3 (Nice!):** Introducing a data type (Op) to represent operators (PlusOp, MinusOp, TimesOp, DivOp), and using a single data constructor (BinOp) that combines an expression with an operator.

- **Option 4 (You've gone too far!):** Using a `String` type for operators instead of a custom data type (Op). This approach sacrifices type safety and clarity.

- **Option 5 (Not "abstract" enough):** Introducing an unnecessary data constructor (Parenthesized) for handling parentheses. This approach violates the principle that the tree structure of the expression already encodes the order of operations, rendering the parentheses redundant.

Option 3 provides an elegant representation, where expressions are composed of nested `BinOp` instances with associated operators and subexpressions. This approach eliminates redundancy and allows for concise pattern matching during evaluation.

### Evaluating Expressions

To evaluate expressions represented as abstract syntax, we need mechanisms to handle both numerical values and binary operations. Let's recap the abstract syntax representation using the `Op` and `Exp` data types:

```haskell
data Op = PlusOp | MinusOp | TimesOp | DivOp deriving (Show)

data Exp = Num Double | BinOp Exp Op Exp deriving (Show)
```

In addition to the representation, we also require functions for pretty printing and evaluation.

#### Pretty Printing

The `format` function provides a way to convert an abstract syntax expression to a human-readable string. We can use pattern matching to traverse the expression tree and construct the string representation:

```haskell
format :: Exp -> String
format (Num x) = show x
format (BinOp left op right) = 
    "(" ++ format left ++ opString op ++ format right ++ ")"

opString :: Op -> String
opString PlusOp  = " + "
opString MinusOp = " - "
opString TimesOp = " * "
opString DivOp   = " / "
```

The `format` function recursively traverses the expression, formatting each subexpression and concatenating them with appropriate operators.

#### Evaluation

The `eval` function allows us to compute the value of an abstract syntax expression. We define evaluation rules for numerical values and each binary operation:

```haskell
eval :: Exp -> Double
eval (Num x) = x
eval (BinOp left PlusOp  right) = eval left + eval right
eval (BinOp left MinusOp right) = eval left - eval right
eval (BinOp left TimesOp right) = eval left * eval right
eval (BinOp left DivOp   right) = eval left / eval right
```

By recursively evaluating sub

expressions and applying the appropriate operations, we can compute the final result of an expression.

### Evaluating Expressions with Variables

To introduce variables into our expressions, we expand the `Exp` data type to include a `Symbol` constructor representing symbolic variables. We also need a mechanism to look up the value of a symbol in a symbol dictionary.

```haskell
data Exp = Symbol String | Num Double | BinOp Exp Op Exp deriving (Show)

type SymbolDictionary = [(Exp, Exp)]

symbolLookup :: Exp -> SymbolDictionary -> Exp
symbolLookup symb [] = error "Symbol not found in dictionary."
symbolLookup symb ((key, val):rest)
    | symb == key = val
    | otherwise = symbolLookup symb rest
```

The `symbolLookup` function takes a symbol and a symbol dictionary and searches for a matching entry. If a match is found, the corresponding value is returned; otherwise, an error is raised.

We can modify the `eval` function to handle symbols by incorporating the symbol dictionary into the evaluation process:

```haskell
eval :: Exp -> SymbolDictionary -> Double
eval (Num x) _ = x
eval (Symbol x) dict =
    let expr = symbolLookup (Symbol x) dict
    in eval expr dict
eval (BinOp left PlusOp right) dict = eval left dict + eval right dict
eval (BinOp left MinusOp right) dict = eval left dict - eval right dict
eval (BinOp left TimesOp right) dict = eval left dict * eval right dict
eval (BinOp left DivOp right) dict = eval left dict / eval right dict
```

When encountering a symbol in the `eval` function, we perform a symbol lookup to retrieve its corresponding expression. We then evaluate that expression recursively, using the same symbol dictionary.

By extending the abstract syntax and evaluation mechanisms, we can handle expressions that involve variables alongside numerical values and binary operations.

These concepts lay the foundation for understanding code as data and evaluating expressions in a variety of programming languages. By exploring syntax, semantics, and abstract syntax representation, we gain insights into the underlying mechanisms that enable program execution and manipulation.