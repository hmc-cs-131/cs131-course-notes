### CS 131: Programming Languages

# Code as Data, Evaluating Expressions

In this lecture, we delve into the concept of code as data and explore how expressions can be represented and evaluated. By understanding the abstract syntax representation of expressions and employing evaluation techniques, we gain insights into the inner workings of programming languages.

## CS131: Past, Present, Future

Before diving into the details, let's take a moment to reflect on the historical and social context of computer science. Influential figures like Babbage, Lovelace, Turing, and Church have shaped the field and laid the foundations for modern computing. We'll also touch upon functional programming concepts, including functions as values, higher-order functions, pattern matching, recursion, recursive data structures, and the basics of Haskell programming.

## What kinds of inputs/outputs can a program have?

Programs can have diverse inputs and outputs, depending on their purpose and functionality. Some examples include:

- Program 1: Input - List of integers, Output - Average of the list
- Program 2: Input - Coordinates, Output - Shortest path
- Program 3: Input - Text file, Output - Spelling errors
- Program 6: Input - Source code, Output - Nicely formatted code
- Program 7: Input - Source code, Output - Binary machine code
- Program 8: Input - Source code, Output - Value
- Program 5: Input - Source code, Output - Number of lines of code

This broad range of inputs and outputs highlights the versatility of programming and the various tasks it can accomplish.

## Important concept alert! Code is data

One key concept to grasp is that code itself can be treated as data. This idea forms the basis for code manipulation, evaluation, and interpretation. By representing code as data, we can analyze, transform, and reason about programs in powerful ways.

## Brainstorm: Representing expressions

To understand how expressions can be represented using data types in Haskell, let's consider some examples. We'll examine expressions written in both mathematical syntax and racket-style syntax.

In math syntax:
- (2 + 2) * 7 - 11
- 15 - 3
- 5 + 4 + 3 + 2 + 1

In racket-style syntax:
- (minus (times (plus 2 2) 7) 11)
- (minus 15 3)
- (plus 5 (plus 4 (plus 3 (plus 2 1))))

These expressions serve as a starting point to explore different ways of representing abstract syntax.

## Expressions and Statements

Before diving into abstract syntax representation, let's clarify the distinction between expressions and statements.

**Expression:** An expression is a computation that calculates a value. In functional programming, "computation" refers to the evaluation of expressions. Expressions can be combined and manipulated to produce desired results.

**Statement:** A statement is a computation performed for its effect, typically involving the modification of the system's state. While statements may change values, they do not inherently have a value themselves. In imperative programming, "computation" often refers to executing a series of statements. Statements introduce side effects, which can go beyond calculating values.

Identifying expressions and statements in languages like C and C++ can help understand their behavior:

- Example 1: `10 * z + 4` is an expression since it evaluates to a value.
- Example 2: `x++;` is a statement that increments the value of `x`. Interestingly, `x++` is an expression with a side effect because it returns a value.
- Example

 3: `while (x > 3) { x = x-1; y = y+1; }` is a statement. It is not appropriate to consider `x = (while (...)) {...}` since `while` is not an expression that returns a value.

Understanding the distinction between expressions and statements helps in comprehending the semantics and behavior of different programming constructs.

## Syntax and Semantics

To further our understanding of programming languages, let's explore the concepts of syntax and semantics.

**Syntax:** Syntax refers to the rules and structure governing the correct formation of programs. It encompasses the valid symbols, keywords, punctuation, and the overall grammar of the language. Syntax defines what programmers are allowed to write.

**Semantics:** Semantics deals with the meaning and interpretation of the code. It defines the behavior and consequences of executing programs written in a particular language. Semantics answers questions like "What does this code do?" and "How does it behave?" Semantics describes what happens when a particular syntax is executed.

Distinguishing between syntax and semantics allows us to comprehend the rules for writing valid code and the implications of executing that code.

## Attaching meaning (semantics) to symbols (syntax)

Attaching meaning to symbols is a fundamental aspect of programming languages. It relates to how we interpret and understand the symbols used in code.

This idea is akin to René Magritte's painting "The Treachery of Images," where an image of a pipe is accompanied by the text "This is not a pipe." The painting challenges our perception and highlights the distinction between the symbol (the image of a pipe) and its actual referent (a physical pipe).

Similarly, in the context of programming languages, we must understand the distinction between symbols (syntax) and their associated meaning (semantics). This topic touches upon linguistics, semiotics, and philosophical aspects related to AI, the philosophy of mind, and the symbol grounding problem.

## Concrete and Abstract Syntax

To represent code in a structured and meaningful way, we distinguish between concrete syntax and abstract syntax.

**Concrete Syntax:** Concrete syntax refers to the actual code written by programmers. It represents programs as linear sequences of characters and includes elements such as keywords, punctuation, and legal identifiers. Concrete syntax encompasses the specific syntax rules of a language, including how to resolve ambiguities. It is defined by a formal grammar.

**Abstract Syntax:** Abstract syntax captures the essence of code and represents programs as structured data in the form of trees. In abstract syntax, specific keywords and punctuation are discarded, and only the essential structure remains. Abstract syntax eliminates ambiguities by using the tree structure to unambiguously represent the program's intended meaning.

Even though different concrete syntaxes can express the same abstract syntax, the abstract syntax captures the core structure and semantics of the program.

## Variation in Concrete Syntax

Concrete syntax often allows for different ways of writing the same abstract syntax. This flexibility arises from language-specific conventions and syntax options. Despite variations in concrete syntax, the underlying abstract syntax remains unchanged.

Two views of syntax, such as "(4 + 2) * 7," can be understood through the processes of parsing and pretty printing. Parsing involves analyzing the concrete syntax and constructing the corresponding abstract syntax tree. Pretty printing, on the other hand, focuses on formatting the abstract syntax tree into a human-readable form.

The abstract syntax representation, by ignoring irrelevant details of concrete syntax, allows us to reason about programs more effectively.

## Syntax Exercise

Let's engage in a syntax exercise to explore different ways of writing an expression:

```
2 - \frac{7(2+3)}{1+1}
```

Possible variations include:

- `2−7(2+3)1+1`
- `(- 2.0 (/ (* 

7.0 (+ 2.0 3.0)) (+ 1.0 1.0)))`
- `(-) 2 ((/) ((*) 7 ((+) 2.0 3.0)) ((+) 1.0 1.0))`
- "add two and three and multiply that by seven, dividing the result by one plus one and then subtract that result from 2"
- "SUBTRACT FROM TWO THE RESULT OF DIVIDING SEVEN TIMES THE SUM OF TWO AND THREE BY THE SUM OF ONE AND ONE"
- `2 7 2 3 + * 1 1 + / -`

These examples illustrate different representations of the same mathematical expression, showcasing the versatility and flexibility of syntax.

## Representing Abstract Syntax

To represent expressions using data types in Haskell, we explore various options. The goal is to capture the essential structure of expressions while enabling easy manipulation and evaluation.

Option 1:
```haskell
data Exp = Double
         | Plus   Exp Exp
         | Minus  Exp Exp
         | Times  Exp Exp
         | Divide Exp Exp
```

In this option, the data type `Exp` represents expressions. However, there is a crucial omission—the missing label for the case involving the `Double`. Without the proper labeling, Haskell will create a value called `Double` without an associated value, leading to unintended results.

Option 2:
```haskell
data Exp = Num    Double
         | Plus   Exp Exp
         | Minus  Exp Exp
         | Times  Exp Exp
         | Divide Exp Exp
```

This option corrects the issue by including the `Num` constructor to represent numbers explicitly. Now, expressions can be properly differentiated from plain numbers.

Option 3:
```haskell
data Op  = PlusOp | MinusOp | TimesOp | DivOp
data Exp = Num    Double
         | BinOp  Exp Op Exp
```

Option 3 offers a more elegant solution. It introduces a separate data type, `Op`, to represent operators. The `Exp` data type uses the `BinOp` constructor to indicate a binary operation involving two expressions and an operator.

Option 4:
```haskell
type Op  = String
data Exp = Num    Double
         | BinOp  Exp Op Exp
```

Option 4 uses a `String` type for operators instead of a separate data type. While this option is valid, it sacrifices some type safety and clarity compared to Option 3.

Option 5:
```haskell
data Op    = PlusOp | MinusOp | TimesOp | DivOp
data Paren = LeftParen | RightParen
data Exp   = Num             Double
           | BinOp           Exp Op Exp
           | Parenthesized   Paren Exp Paren
```

Option 5 adds an unnecessary level of complexity by introducing `Paren` data type to represent parentheses. Since the `BinOp` constructor already allows nesting of expressions, the `Parenthesized` constructor becomes redundant and allows nonsensical expressions.

Choosing an appropriate representation for abstract syntax strikes a balance between clarity, maintainability, and ease of manipulation.

## Evaluating Expressions

Now that we understand how to represent expressions using abstract syntax, let's explore how to evaluate these expressions to obtain their values.

Recall the abstract syntax representation from Option 3:
```haskell
data Op  = PlusOp | MinusOp | TimesOp | DivOp
data Exp = Num    Double
         | BinOp  Exp Op Exp
```

To evaluate expressions, we define an evaluation function `eval` that operates on the abstract syntax representation.

```haskell
eval :: Exp -> Double
eval (Num

 x) = x
eval (BinOp left PlusOp  right) = eval left + eval right
eval (BinOp left MinusOp right) = eval left - eval right
eval (BinOp left TimesOp right) = eval left * eval right
eval (BinOp left DivOp   right) = eval left / eval right
```

The `eval` function recursively evaluates expressions by pattern matching on the abstract syntax representation. When encountering a `Num`, the associated value is simply returned. For binary operations (`BinOp`), the evaluation is performed recursively on the left and right subexpressions, with the operator applied to the results.

With the `eval` function, we can compute the values of expressions by traversing the abstract syntax tree and performing the necessary computations.

## Evaluating Expressions with Variables

Expanding upon expression evaluation, let's introduce the concept of symbols and their lookup in a symbol dictionary. This allows us to evaluate expressions involving variables.

To represent variables, we extend the abstract syntax representation with a `Symbol` constructor:
```haskell
data Exp
   = Symbol String 
   | Num    Double
   | BinOp  Exp Op Exp
```

To evaluate expressions with variable symbols, we introduce a `SymbolDictionary` type, which associates symbols with their corresponding expressions:
```haskell
type SymbolDictionary = [(Exp, Exp)]
```

We also define a symbol lookup function, `symbolLookup`, that retrieves the expression associated with a symbol from the symbol dictionary:
```haskell
symbolLookup :: Exp -> SymbolDictionary -> Exp
symbolLookup symb [] = undefined
symbolLookup symb ((key, val) : rest) =
    if symb == key
    then val
    else symbolLookup symb rest
```

The `eval` function is extended to handle symbol lookup:
```haskell
eval :: Exp -> SymbolDictionary -> Double
eval (Num x) dict = x
eval (Symbol x) dict =
    let expr = symbolLookup (Symbol x) dict
    in eval expr dict
eval (BinOp left PlusOp  right) dict =  (eval left dict) + (eval right dict)
eval (BinOp left MinusOp right) dict =  (eval left dict) - (eval right dict)
eval (BinOp left TimesOp right) dict =  (eval left dict) * (eval right dict)
eval (BinOp left DivOp   right) dict =  (eval left dict) / (eval right dict)
```

With symbol lookup, we can evaluate expressions involving both numbers and variables by retrieving the corresponding values from the symbol dictionary.

By understanding code as data, representing expressions using abstract syntax, and evaluating them with or without variables, we gain deeper insights into programming language concepts and the inner workings of programming languages.