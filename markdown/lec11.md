### CS 131: Programming Languages

# Parsing, Part 3

In this lecture, we continue our exploration of parsing techniques, focusing on parameterized parsers and parsers capable of constructing Abstract Syntax Trees (ASTs). These concepts enhance our ability to parse complex language structures and extract meaningful representations from the input.

## Recap: Our Library So Far

To provide context, let's briefly recap the progress we have made with our parsing library. We started by understanding the distinction between syntax and semantics, where syntax refers to what the programmer writes, and semantics captures the meaning behind the syntax. Our library aims to check for syntax errors and construct an AST when the syntax is correct.

### Syntax and Abstract Syntax

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

These data types capture the structure of expressions and operators in our language, forming the foundation for building the AST.

### Grammar

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

The grammar defines the valid structure and rules for constructing expressions in our language.

### Parsing Functions and State

To facilitate parsing, we introduced the concept of a parsing function, which takes a string as input and produces either a successful parse result or a failure result. Initially, our parsing function returned a boolean value indicating success or failure:

```haskell
type ParsingFunction = String -> Bool
```

However, we realized the need to keep track of the state and the remaining unparsed portion of the input string. To address this, we modified our parsing function to return a tuple of type `(Bool, String)`:

```haskell
type ParsingFunction = String -> (Bool, String)
```

This modification allowed us to handle more complex parsing scenarios and maintain the necessary state information during the parsing process.

### Parser Combinators

We then developed parsing functions for different non-terminals, such as `expr` and `factor`, using combinators such as `<&&>` and `<||>` to handle sequencing and alternatives. These parser combinators enabled us to build more complex parsers by combining simpler parsers, following the structure of our grammar.

### Current Limitations

While our parsers successfully determine syntactic validity, they currently only return a boolean result and do not generate the desired abstract syntax tree (AST). In the next lecture, we will focus on modifying our parsers to produce the desired AST, thereby completing our parsing library.

By combining the existing notes with the provided lecture transcript, we have created a comprehensive recap of the progress made in building our parsing library.

Certainly! Here's the updated combined markdown with the code incorporated and explanations provided:

Certainly! Here's the updated combined markdown with the code incorporated and explanations provided:

## String Parser

While our parsing library successfully checks for syntax errors, it currently falls short in constructing an AST, which represents the structure and meaning of the parsed expression. To address this limitation, we need to enhance our parsing functions to generate AST nodes.

To achieve AST construction, we introduce a new type called `Parser`:

```haskell
type Parser a = String -> Maybe (a, String)
```

The `Parser` type takes a type variable `a` and represents a function that takes a string as input and returns a `Maybe` result containing the parsed value of type `a` and the remaining unparsed portion of the input string.

By utilizing the `Maybe` type, we can handle both successful parses (`Just (result, remainder)`) and parse failures (`Nothing`), providing a clearer indication of success or failure compared to the previous approach.

Let's explore some of the key components of our enhanced parsing library.

### Parsing Functions

At the core of our library are the parsing functions, which are functions that take an input string and produce a parsed result. We define the type `Parser a` to represent such parsing functions:

```haskell
type Parser a = String -> Maybe (a, String)
```

A `Parser a` is a function that takes a `String` as input and returns a `Maybe` value. If the parsing is successful, the `Maybe` result will contain a tuple `(result, remainder)`, where `result` is the parsed value of type `a`, and `remainder` is the unparsed portion of the input string. If the parsing fails, the `Maybe` result will be `Nothing`.

### Running a Parser

To run a parser on an input string and retrieve the parsed result, we define the `parse` function:

```haskell
parse :: Parser a -> String -> a
parse p input = 
  case p input of 
    Just (result, "") -> result
    Just (_, remainder) -> error ("Unexpected input: " ++ remainder)
    Nothing -> error "Parse error"
```

The `parse` function takes a parser `p` and an input string `input`. It applies the parser `p` to the input string and examines the result. If the parsing is successful and the entire input is consumed (`""`), it returns the parsed result. Otherwise, it raises an error indicating unexpected input.

### Parser Combinators

Parser combinators are functions that allow us to build more complex parsers by combining simpler parsers. Here are some key parser combinators in our library:

#### `return`

The `return` combinator constructs a parser that always succeeds without consuming input. It simply wraps a value into a parser:

```haskell
return :: a -> Parser a
return result s = Just (result, s)
```

#### `pfail`

The `pfail` combinator constructs a parser that always fails without consuming input. It represents a parsing failure:

```haskell
pfail :: Parser a
pfail _ = Nothing
```

#### `<|>`

The `<|>` combinator combines two parsers as alternatives. It tries the first parser, and if it fails, it tries the second parser:

```haskell
(<|>) :: Parser a -> Parser a -> Parser a
(p1 <|> p2) s = 
  case p1 s of
    Just (result, s') -> Just (result, s')
    Nothing -> p2 s
```

#### `<++>`

The `<++>` combinator concatenates two parsers that produce lists. It applies the first parser and the second parser sequentially, and concatenates their results:

```haskell


(<++>) :: Parser [a] -> Parser [a] -> Parser [a]
(p1 <++> p2) s =
  case p1 s of
    Just (result1, s') -> case p2 s' of
                            Nothing -> Nothing
                            Just (result2, s'') -> Just (result1 ++ result2, s'')
    Nothing -> Nothing
```

#### `<:>`

The `<:>` combinator combines a parser that produces a single element with a parser that produces a list. It applies the first parser to get an element and the second parser to get a list, and combines them:

```haskell
(<:>) :: Parser a -> Parser [a] -> Parser [a]
(p1 <:> p2) s =
  case p1 s of
    Just (result1, s') -> case p2 s' of
                            Nothing -> Nothing
                            Just (result2, s'') -> Just (result1 : result2, s'')
    Nothing -> Nothing
```

#### `<+>`

The `<+>` combinator combines two parsers and returns their results as a pair:

```haskell
(<+>) :: Parser a -> Parser b -> Parser (a, b)
(p1 <+> p2) s =
  case p1 s of
    Just (result1, s') -> case p2 s' of
                            Nothing -> Nothing
                            Just (result2, s'') -> Just ((result1, result2), s'')
    Nothing -> Nothing
```

#### `<-+>`

The `<-+>` combinator combines two parsers and discards the result of the first parser, returning the result of the second parser:

```haskell
(<-+>) :: Parser a -> Parser b -> Parser b
(p1 <-+> p2) s =
  case p1 s of
    Just (_, s') -> p2 s'
    Nothing -> Nothing
```

#### `<+->`

The `<+->` combinator combines two parsers and discards the result of the second parser, returning the result of the first parser:

```haskell
(<+->) :: Parser a -> Parser b -> Parser a
(p1 <+-> p2) s =
  case p1 s of
    Just (result1, s') -> case p2 s' of
                            Nothing -> Nothing
                            Just (_, s'') -> Just (result1, s'')
    Nothing -> Nothing
```

## Parametrized Parser

In this section, we'll explore how to make our parsing library more flexible and reusable by introducing parameterized types. Instead of hardcoding specific result types, we'll use type variables to create parsers that can handle different types of results.

### Updating the Parser Type

To begin, we need to update our `Parser` type to be parameterized by a type variable `a`. This will make the result type of the parser generic, allowing it to handle different kinds of results. Here's the updated definition:

```haskell
newtype Parser a = Parser { runParser :: String -> Maybe (a, String) }
```

Now, instead of `String` being the fixed result type, it will be replaced by `a` throughout the code.

### Parser Combinators

Next, we'll update our parser combinators and functions to work with the parameterized `Parser` type.

#### `pars`

The `pars` combinator takes a parser `p` and applies it to an input string. It has the following updated type signature:

```haskell
pars :: Parser a -> String -> Maybe (a, String)
```

This function applies the parser `p` to the input string and returns the parse result as a `Maybe` value containing a pair of the result and the remaining string.

#### `returnP`

The `returnP` function constructs a parser that always succeeds without consuming any input. It has the following updated type signature:

```haskell
returnP :: a -> Parser a
```

The `returnP` function takes a value `x` and returns a parser that always succeeds with the value `x` as the result.

#### `p <|> q`

The `<|>` combinator combines two parsers `p` and `q` and returns a new parser that tries `p` first and if it fails, tries `q`. It has the following updated type signature:

```haskell
(<|>) :: Parser a -> Parser a -> Parser a
```

This combinator takes two parsers of the same type and returns a new parser of the same type.

#### `p <++> q`

The `<++>` combinator combines two parsers `p` and `q` and returns a new parser that applies both parsers and concatenates their results. It has the following updated type signature:

```haskell
(<++>) :: Parser [a] -> Parser [a] -> Parser [a]
```

This combinator takes two parsers that produce lists of elements and returns a new parser that produces a concatenated list.

#### `p <:> q`

The `<:>` combinator combines a parser that produces a single element with a parser that produces a list. It has the following updated type signature:

```haskell
(<:>) :: Parser a -> Parser [a] -> Parser [a]
```

This combinator takes a parser that produces a single element and a parser that produces a list of elements and returns a new parser that produces a list with the single element followed by the list.

#### `p <+> q`

The `<+>` combinator combines two parsers and returns their results as a pair. It has the following updated type signature:

```haskell
(<+>) :: Parser a -> Parser b -> Parser (a, b)
```

This combinator takes two parsers of different types and returns a new parser that produces a pair of results.

#### `p <-+> q`

The `<-+>` combinator combines two parsers and discards the result of the first parser, returning the result of the second parser. It has the following updated type signature:

```haskell
(<-+>) :: Parser a -> Parser b -> Parser b
```

This combinator takes

 two parsers of different types and returns a new parser that produces the result of the second parser.

### Basic Parsers

We'll update our basic parsers to work with the parameterized `Parser` type.

#### `getCharThat`

The `getCharThat` function constructs a parser that matches a character satisfying a given predicate. It has the following updated type signature:

```haskell
getCharThat :: (Char -> Bool) -> Parser Char
```

This function takes a predicate on characters and returns a parser that matches a character if it satisfies the predicate.

#### `letter`

The `letter` parser matches a single letter. It has the following updated type signature:

```haskell
letter :: Parser Char
```

This parser is constructed using `getCharThat` with the predicate `isLetter`.

#### `letters`

The `letters` parser matches one or more letters. It has the following updated type signature:

```haskell
letters :: Parser String
```

This parser is constructed using the `some` combinator with the `letter` parser.

#### `space`

The `space` parser matches a single space character. It has the following updated type signature:

```haskell
space :: Parser Char
```

This parser is constructed using `getCharThat` with the predicate `isSpace`.

#### `spaces`

The `spaces` parser matches one or more space characters. It has the following updated type signature:

```haskell
spaces :: Parser String
```

This parser is constructed using the `some` combinator with the `space` parser.

#### `skipws`

The `skipws` combinator skips leading whitespace and applies a parser `p`. It has the following updated type signature:

```haskell
skipws :: Parser a -> Parser a
```

This combinator takes a parser `p` and returns a new parser that skips leading whitespace before applying `p`.

#### `number`

The `number` parser matches a number, ignoring leading whitespace. It has the following updated type signature:

```haskell
number :: Parser String
```

This parser is constructed using the `skipws` combinator with the `digits` parser.

#### `sym`

The `sym` function constructs a parser that matches a specific character, ignoring leading whitespace. It has the following updated type signature:

```haskell
sym :: Char -> Parser Char
```

This function takes a character `c` and returns a parser that matches that character, ignoring leading whitespace.

By parameterizing our parser library, we have made it more flexible and reusable. The parsers can now handle different types of results, allowing for greater versatility in parsing various input formats.

