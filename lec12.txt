# CS131: Programming Languages

## Parsing, Part 3

In this lecture, we continue our exploration of parsing techniques, focusing on parameterized parsers and parsers capable of constructing Abstract Syntax Trees (ASTs). These concepts enhance our ability to parse complex language structures and extract meaningful representations from the input.

### Recap: Our Library So Far

To provide context, let's briefly recap the progress we have made with our parsing library. We started by understanding the distinction between syntax and semantics, where syntax refers to what the programmer writes, and semantics captures the meaning behind the syntax. Our library aims to check for syntax errors and construct an AST when the syntax is correct.

We defined the concrete syntax and abstract syntax for our language, which involves representing expressions and operators using data types. For example:

```haskell
data Exp = Num Double
         | BinOp Exp Op Exp
   deriving (Show, Eq)

data Op = PlusOp
        | MinusOp
        | TimesOp
        | DivOp
   deriving (Show, Eq)
```

Additionally, we established the grammar for expressions, which consists of factors and various operations:

```
Expr ::= Factor + Expr
      | Factor - Expr
      | Factor * Expr
      | Factor / Expr
      | Factor

Factor ::= number
          | (Expr)
```

To facilitate parsing, we introduced the concept of a parsing function, which takes a string as input and produces either a successful parse result or a failure result. Initially, our parsing function returned a boolean value indicating success or failure:

```haskell
type ParsingFunction = String -> Bool
```

However, we realized the need to keep track of the state and the remaining unparsed portion of the input string. To address this, we modified our parsing function to return a tuple of type `(Bool, String)`:

```haskell
type ParsingFunction = String -> (Bool, String)
```

We then developed parsing functions for different non-terminals, such as `expr` and `factor`, using combinators such as `<&&>` and `<||>` to handle sequencing and alternatives.

### Introducing AST Construction

While our parsing library successfully checks for syntax errors, it currently falls short in constructing an AST, which represents the structure and meaning of the parsed expression. To address this limitation, we need to enhance our parsing functions to generate AST nodes.

To achieve AST construction, we introduce a new type called `Parser`:

```haskell
type Parser a = String -> Maybe (a, String)
```

The `Parser` type takes a type variable `a` and represents a function that takes a string as input and returns a `Maybe` result containing the parsed value of type `a` and the remaining unparsed portion of the input string.

By utilizing the `Maybe` type, we can handle both successful parses (`Just (result, remainder)`) and parse failures (`Nothing`), providing a clearer indication of success or failure compared to the previous approach.

### Refining Parsing Functions for AST Construction

With the introduction of the `Parser` type, we can enhance our parsing functions to produce AST nodes instead of simple success or failure indications.

For example, let's consider the `expr` parsing function. Previously, it had the type `ParsingFunction`, but now we can redefine it as a `Parser Exp`:

```haskell
expr :: Parser Exp
```

This revised `expr` function encapsulates the logic for parsing expressions and constructs AST nodes of type `Exp`.

To achieve this, we need to modify the implementation of our parsing functions to return the parsed AST node along with the remaining unparsed portion of the input string.

### Wrapping Up

With the introduction of parameterized parsers

 and the ability to construct ASTs, our parsing library becomes more powerful and expressive. We can now handle complex language structures, parse with context, and generate meaningful representations of the input.

By leveraging the `Parser` type and refining our parsing functions, we bridge the gap between the syntax of the input and its corresponding AST, enabling us to perform further analysis and interpretation of programming languages.

This lecture provides a foundation for understanding advanced parsing techniques and sets the stage for deeper explorations into programming language implementation.