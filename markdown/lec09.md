### CS 131: Programming Languages

# Parsing, Part 1

## Parsing: An Overview

In CS 131, we now shift our focus to parsing, which is the front end of a programming language. Parsing involves transforming the concrete syntax, which is what the programmer writes, into the abstract syntax, which represents the program as data. The parser plays a crucial role in this transformation process.

### The Architecture of a Programming Language

Before diving into parsing, let's briefly review the architecture of a programming language. It consists of three main components:

1. Front End: The front end deals with the concrete syntax and includes the parsing phase.
2. Middle: The middle represents the abstract syntax, which is a data structure representing the program.
3. Back End: The back end focuses on the semantics and execution of the program.

Throughout the semester, we have primarily focused on the middle and back end components, working with abstract syntax and implementing evaluators using Haskell data types and pattern matching functions.

### The Role of a Parser

The parser is responsible for transforming the concrete syntax into the abstract syntax. It performs two primary tasks:

1. Syntax Error Checking: The parser checks for syntax errors in the input program.
2. Abstract Syntax Tree (AST) Construction: If there are no syntax errors, the parser constructs the AST, representing the program as data.

### Writing a Parser

There are several approaches to writing a parser. We will explore two common methods in this course:

1. Hand-Written Parser: This approach involves writing the parser code entirely by hand.
2. Hand-Written Parser with Library: In this method, we write the parser manually but leverage a library to assist us.

While there are other techniques like parser generators and parser synthesizers, we will focus on the first two approaches. Writing our own parsers will enhance our understanding of parsing and provide insights into implementing programming languages.

### Parser Implementation Methods

#### Hand-Written Parser

In a hand-written parser, we write the parsing code from scratch. We manually define the rules and logic for recognizing the syntax and constructing the AST. This approach gives us full control over the parsing process and allows us to deeply understand the intricacies of parsing.

#### Hand-Written Parser with Library

The second approach involves writing the parser manually but utilizing a parsing library to handle some aspects of the parsing process. The library provides tools and functions that simplify the parsing logic, making the implementation more manageable and concise.

#### Benefits of Writing Our Own Parsers

By writing our own parsers, we gain a better understanding of parsing techniques and the inner workings of programming languages. It allows us to explore the field of parsing, which is vast and complex. Although parsing itself could be a dedicated course, our focus in CS 131 is to grasp the fundamental concepts and insights related to parsing.


## Tokenization: Breaking Down the Code

Tokenization is the process of dividing the concrete syntax of a program into individual tokens, which are the smallest and most atomic pieces of code. Tokens can include literals, numbers, strings, punctuation, identifiers, operators, reserved words, and whitespace (which is usually ignored during parsing).

To understand tokenization better, let's examine the tokenization process for the following code snippet:

```c
int main()
{
    for (int count = 0; count < 10; ++count) {
        printf("Hello, World!");
    }
    return 0;
}
```

When tokenizing this code, we can identify different types of tokens, including:

- **Type**: The reserved word "int"
- **Identifier**: The identifier "main"
- **Punctuation**: Curly braces, semicolon, parentheses
- **Reserved word**: "for", "int", "return"
- **Operator**: `<`, `=`, `++`
- **Literal**: The string literal "Hello, World!"
- **Number**: The numeric literal 0
- **Whitespace**: Spaces, tabs, and line breaks

### Vocabulary

To discuss tokenization, it's helpful to understand the following vocabulary:

- **Token (noun)**: An atomic piece of syntax, such as a reserved word, a literal value, or an operator.
- **Tokenize (or lex) (verb)**: The process of transforming concrete syntax into a list of tokens.
- **Tokenizer (or lexer) (noun)**: A piece of code responsible for tokenizing.

### Implementing a Tokenizer

The implementation of a tokenizer is an initial step towards parsing. Here's how we can implement a tokenizer in Haskell:

#### Step 1: Define a Data Type for Tokens

We start by defining a data type called `Token` to represent the different types of tokens. Each token has a corresponding constructor within the data type:

```haskell
data Token = CrossToken       -- ^ The '+' character
           | DashToken        -- ^ The '-' character
           | StarToken        -- ^ The '*' character
           | SlashToken       -- ^ The '/' character
           | LParenToken      -- ^ The '(' character
           | RParenToken      -- ^ The ')' character
           | NumberToken Double  -- ^ A numeric literal
           deriving (Eq, Show)
```

#### Step 2: Implement the `tokenize` Function

The `tokenize` function takes an input string and returns a list of tokens. Here's an example implementation in Haskell:

```haskell
tokenize :: String -> [Token]
-- Tokenize literal characters
tokenize ('+':rest) = CrossToken : tokenize rest
tokenize ('-':rest) = DashToken : tokenize rest
tokenize ('*':rest) = StarToken : tokenize rest
tokenize ('/':rest) = SlashToken : tokenize rest
tokenize ('(':rest) = LParenToken : tokenize rest
tokenize (')':rest) = RParenToken : tokenize rest
-- Handle other cases
tokenize [] = []
tokenize s@(c:rest)
    -- Skip whitespace
    | isSpace c = tokenize rest
    -- Tokenize a numeric literal
    | isNumber c =
        let (num, s') = span isNumber s in
        (NumberToken (read num)) : tokenize s'
    -- Handle errors for unknown characters
    | otherwise = error ("Invalid character: " ++ show c)
```

In this implementation, we handle literal characters by pattern matching on the first character of the input string. For each literal character, we prepend the corresponding token to the result of tokenizing the rest of the string.

We also handle whitespace by skipping it using the `isSpace` function. Numeric literals are tokenized by using the `span` function to extract a sequence of numeric characters. The extracted string is then converted to a `Double` using the `read` function, and a `NumberToken` is created with the numeric value.

For any other character encountered, an error is raised to indicate an invalid character.

By implementing the `tokenize` function, we can convert the code's concrete syntax into a list of tokens, which can then be used for further parsing tasks.

## Grammars 

A grammar serves as a specification for a parser, defining the valid structure and syntax of programs. Let's explore the concept of grammars in more detail and connect it to the example grammar provided.

### Grammars

A grammar provides a set of rules and production rules that describe the valid structure and composition of programs in a specific language. It consists of terminal symbols, non-terminal symbols, production rules, and a start symbol.

### Example Grammar: Arithmetic Expressions

Let's consider the example grammar for arithmetic expressions:

```plaintext
Expr ::= Expr + Expr
       | Expr - Expr
       | Expr * Expr
       | Expr / Expr
       | number
       | (Expr)
```

In this grammar, `Expr` represents the start symbol, indicating the root of the concrete syntax tree. The grammar provides different alternatives for constructing expressions using the production rules.

- Alternatives: The different valid forms for expressions, such as addition, subtraction, multiplication, division, numeric literals, and parenthetical expressions.
- Production rules: These rules define how to derive or construct non-terminal symbols. Each alternative in the grammar corresponds to a production rule.
- Terminal symbols: These symbols represent the actual tokens or characters present in the language, such as "+", "-", "*", "/", and numeric literals.
- Non-terminal symbols: These symbols represent syntactic categories or placeholders that can be further expanded or derived.

### Parsing and Concrete Syntax Trees

The role of a parser is to determine whether a program adheres to the specified grammar. By applying the grammar's rules, the parser constructs a concrete syntax tree (also known as a parse tree) that represents the structure of the program.

When parsing an arithmetic expression using the provided grammar, the parser explores the alternatives and applies the production rules to derive the concrete syntax tree. The resulting tree confirms the program's syntactic validity based on the grammar's specifications.

Understanding the components of grammars, such as alternatives, production rules, terminal symbols, and non-terminal symbols, helps us implement effective parsers that can validate programs in a given language.

## Grammars and Parsing: From a Grammar to a Parser

The process of transforming a grammar into a parser involves writing parser code that closely resembles the grammar. Recursive-descent parsing is an approach commonly used for this purpose. In recursive-descent parsing, each non-terminal symbol in the grammar becomes a parsing function.

Let's start with the initial grammar:

```plaintext
Expr ::= Expr + Expr
       | Expr - Expr
       | Expr * Expr
       | Expr / Expr
       | number
       | (Expr)
```

This grammar suffers from left recursion, which can cause the parser to enter an infinite recursion loop and not terminate. To address this issue, the grammar can be refactored to eliminate left recursion:

```plaintext
Expr ::= Factor + Expr
       | Factor - Expr
       | Factor * Expr
       | Factor / Expr
       | Factor

Factor ::= number
         | (Expr)
```

The refactored grammar successfully eliminates left recursion. However, it treats all operators as having the same precedence, which might not be desired. To handle operator precedence, the grammar can be further modified:

```plaintext
Expr ::= Term + Expr
       | Term - Expr
       | Term

Term ::= Factor * Term
       | Factor / Term
       | Factor

Factor ::= number
         | (Expr)
```

In this modified grammar, the `Expr` production rule now consists of terms with plus or minus operators, and the `Term` production rule handles factors with multiplication or division operators.

However, the modified grammar still exhibits right-associativity for all operators. To achieve left-associativity, the grammar can be further refined:

```plaintext
Expr ::= Term PlusMinus

PlusMinus ::= + Term PlusMinus
            | - Term PlusMinus
            | ε

Term ::= Factor TimesDiv

TimesDiv ::= * Factor TimesDiv
           | / Factor TimesDiv
           | ε

Factor ::= number
         | (Expr)
```

In this refactored grammar, the `PlusMinus` non-terminal handles plus and minus operators, while the `TimesDiv` non-terminal handles multiplication and division operators. The use of epsilon (`ε`) allows for an empty alternative, indicating the end of a chain of operators.

By refactoring the grammar and introducing additional non-terminal symbols, we achieve left-associativity for operators.

To implement the parser, we use a recursive descent approach where each non-terminal symbol corresponds to a parsing function. The code closely mirrors the structure of the grammar, with each alternative in the grammar represented by a set of parsing function calls and token checks.

It's important to note that the code provided here is a simplified example to illustrate the concept. Actual parser implementations often involve additional error handling, token consumption, and other considerations.


## State

In this lecture, we focused on modifying our parser to consume tokens as it progresses. This modification involved updating the type of our parse function and keeping track of the remaining tokens.

### Updating the Parser Type

We began by changing the type of our parse function to include the remaining tokens. Previously, it only returned a Boolean result. With the modification, the parse function now has the following type:

```haskell
type Parser a = [Token] -> (Bool, [Token])

parse :: Parser Bool
```

This change allowed us to keep track of both the parsing result and the remaining tokens.

### Handling Successful and Failed Parses

To handle successful and failed parses, we adjusted the logic of our parse function. If the parse succeeded and there are no leftover tokens, the overall result is considered true. However, if there are remaining tokens, the result is false. In the case of a failed parse, the result is always false.

The updated parse function now looks like this:

```haskell
parse tokens =
  let (result, remainingTokens) = expr tokens
  in if result && null remainingTokens
       then (True, remainingTokens)
       else (False, remainingTokens)
```

Here, `expr` represents the parsing function for our grammar's expression rule.

### Updating Parsing Functions

With the changes to our parse function, we needed to update our parsing functions accordingly. Previously, these functions returned only Booleans, but now they return pairs of Booleans and remaining tokens.

For example, here's an updated version of the `expr` parsing function:

```haskell
expr :: Parser Bool
expr tokens =
  case factor tokens of
    (True, tokens') ->
      case parsePlus tokens' of
        (True, tokens'') ->
          expr tokens''
        _ ->
          (False, tokens)
    _ ->
      (False, tokens)
```

In this example, we handle the case where the expression starts with a factor and a plus operator. We recursively call `expr` on the remaining tokens after parsing the factor and plus operator. If any of the parsing steps fail, we return `(False, tokens)`.

Similar updates were made to the parsing functions for other grammar rules, such as `parseMinus`, `parseTimes`, `parseDivide`, and `factor`.

### Pattern Matching for Tokens

To improve readability and handle different cases, we utilized pattern matching when parsing tokens. This approach allowed us to check the type of the first token and perform specific parsing actions based on that.

For instance, in the `factor` function, we checked if the first token is a number token. If it is, we considered it a successful parse.

```haskell
factor :: Parser Bool
factor ((NumberToken _):tokens') =
  (True, tokens')
factor _ =
  (False, tokens)
```

Similarly, for a parenthetical expression starting with a left parenthesis, we checked if the following tokens matched the expression rule. If so, we considered it a successful parse.

```haskell
parenExpr :: Parser Bool
parenExpr ((LeftParenToken):tokens') =
  case expr tokens' of
    (True, (RightParenToken):tokens'') ->
      (True, tokens'')
    _ ->
      (False, tokens)
parenExpr _ =
  (False, tokens)
```

### Testing the Modified Parser

After making these updates, we tested our modified parser. We parsed various expressions and verified if the results matched our expectations.

```haskell
parse "1 + 2" -- Should return (True, [])
parse "3 * 4" -- Should return (True, [])
parse "1 + 2 *

 3" -- Should return (True, [])
parse "(1 + 2" -- Should return (False, [RightParenToken])
```

However, it is important to note that while the modifications allowed us to consume tokens during parsing, the resulting code became less readable and more complex.

## Constructing an AST

### Abstract Syntax Tree (AST)

The `MathAST` module introduces two key types of AST constructors: `Num` and `BinOp`. These constructors allow us to represent literal numbers (`Num`) and binary operations (`BinOp`) between two expressions. The `BinOp` constructor includes the left-hand expression, operator, and right-hand expression.

```haskell
data Exp = Num Double
         | BinOp Exp Op

data Op = PlusOp
        | MinusOp
        | TimesOp
        | DivOp
```

With these constructors, we can create ASTs that accurately reflect the structure of our mathematical expressions.

### Modifying the Parser

To incorporate the construction of ASTs during parsing, we need to update our parser code. Instead of returning booleans, our parser functions will now return expressions (`Exp`). To achieve this, we import the `MathAST` module and redefine the `parse` function as follows:

```haskell
import MathAST

parse :: [Token] -> (Exp, [Token])
```

### Handling Parsing Success and Failure

When a parse is successful, we will have an expression and possibly some remaining tokens. If there are no leftover tokens, the result will be the expression itself. However, if there are remaining tokens, we need to handle the error case by indicating unexpected input.

```haskell
parse tokens =
  let (exp, remainingTokens) = expr tokens
  in if null remainingTokens
       then (exp, remainingTokens)
       else error "Unexpected input: " ++ show remainingTokens
```

### Handling Binary Operations

To handle binary operations, we need to modify the parsing function `expr`. Instead of returning booleans, it will now return an expression (`Exp`). We introduce a variable `left` to store the left-hand side of the binary operation and `right` to store the right-hand side. This allows us to construct the appropriate `BinOp` AST.

```haskell
expr :: [Token] -> (Exp, [Token])
expr tokens =
  case factor tokens of
    (left, tokens') ->
      case parsePlus tokens' of
        (PlusOp, tokens'') ->
          case expr tokens'' of
            (right, tokens''') ->
              (BinOp left PlusOp right, tokens''')
            _ -> error "Unexpected input"
        _ -> (left, tokens')
```

Similar modifications need to be made for other binary operations (`MinusOp`, `TimesOp`, `DivOp`). These changes ensure that the parsing function constructs the appropriate `BinOp` AST.

### Handling Factors

To handle factors, we update the `factor` parsing function. Instead of returning booleans, it will now return an expression (`Exp`). We check if the first token is a number token and construct a `Num` AST with the corresponding value. Additionally, we handle parenthetical expressions by recursively parsing the expression inside the parentheses and ensuring a matching right parenthesis follows.

```haskell
factor :: [Token] -> (Exp, [Token])
factor ((NumberToken n) : tokens') = (Num n, tokens')
factor _ = error "Unexpected input"
```

### Evaluating the AST

To evaluate the AST, we define an `eval` function that

 takes an expression (`Exp`) and computes its numerical value. We pattern match on the AST constructors to handle different cases. For binary operations, we evaluate the left and right expressions and perform the appropriate mathematical operation based on the operator.

```haskell
eval :: Exp -> Double
eval (Num n) = n
eval (BinOp left op right) =
  case op of
    PlusOp -> eval left + eval right
    MinusOp -> eval left - eval right
    TimesOp -> eval left * eval right
    DivOp -> eval left / eval right
```

### Creating a Main Program

We can create a main program by importing the parser and evaluator modules. The `run` function takes a program (as a string) and returns the computed result. It first parses the program using the parser and then evaluates the resulting AST.

```haskell
import Parser
import Evaluator

run :: String -> Double
run program =
  let (ast, _) = parse (tokenize program)
  in eval ast
```

By calling the `run` function with the desired program, we can run and evaluate mathematical expressions.

```haskell
run "1 + 2" -- Evaluates to 3.0
```
