### CS 131: Programming Languages

# Parsing, Part 1

## Today's Topics
- Software architecture of a programming language
- Parsing: terminology and approaches
- Grammars
- Tokenization
- Recursive-descent parsers

## Parsing: An Overview
Recall: syntax and semantics

- What the programmer writes is a sequence of characters (text, strings).
- A tree data structure represents the meaning.
- Haskell data types and eval function are written in Haskell.

**Previous focus:**
- Recall: syntax and semantics
- What the programmer writes
- A tree data structure
- The meaning
- Sequence of characters
- Haskell data types
- eval function written in Haskell

**Current focus:**
- What does a parser do?
  1. Check for syntax errors.
  2. If there are no syntax errors, construct the Abstract Syntax Tree (AST).

**How do we implement a parser?**
1. By hand, from scratch.
2. By hand, using a library.
3. Using a parser generator that compiles a description of the syntax to parser code.
4. Using a parser synthesizer that uses examples of (in)valid programs to create parser code.

## Tokenization
What are the smallest pieces of this code?
```c
int main()
{
    for (int count = 0; count < 10; ++count) {
        printf("Hello, World!");
    }
    return 0;
}
```

- Type: literal, number, string, punctuation, identifier, operator, reserved word, whitespace (ignored)

**Some vocabulary:**
- Token (noun): an atomic piece of syntax (e.g., a reserved word, a literal value, or an operator).
- Tokenize (or lex) (verb): turn concrete syntax into a list of tokens.
- Tokenizer (or lexer) (noun): a piece of code that tokenizes.

**Implementing a Tokenizer:**
A first step towards parsing.

Step 1: Data type for tokens
```haskell
data Token = CrossToken      -- ^ the '+' character
           | DashToken       -- ^ the '-' character
           | StarToken       -- ^ the '*' character
           | SlashToken      -- ^ the '/' character
           | LParenToken     -- ^ the '(' character
           | RParenToken     -- ^ the ')' character
           | NumberToken Double  -- ^ a numeric literal
           deriving (Eq, Show)
```

Step 2: `tokenize` function
```haskell
tokenize :: String -> [Token]
-- Tokenize literal characters
tokenize ('+':rest) = CrossToken : tokenize rest
tokenize ('-':rest) = DashToken : tokenize rest
tokenize ('*':rest) = StarToken : tokenize rest
tokenize ('/':rest) = SlashToken : tokenize rest
tokenize ('(':rest) = LParenToken : tokenize rest
tokenize (')':rest) = RParenToken : tokenize rest
tokenize [] = []
tokenize s@(c:rest)
    -- Skip whitespace
    | isSpace c = tokenize rest
    -- Tokenize a numeric literal
    | isNumber c =
        let (num, s') = span isNumber s in
        (NumberToken (read num)) : tokenize s'
    -- Everything else is an error
    | otherwise = error ("Invalid character: " ++ show c)
```

## Grammars
A grammar is a specification for a parser.

**Example Grammar:**
```
Expr ::= Expr + Expr
       | Expr - Expr
       | Expr * Expr
       | Expr / Expr
       | number
       | (Expr)


```

- `Expr`: The start symbol.
- Alternatives: Different valid forms for expressions.
- Production rules: Definitions for each alternative.
- Terminal symbols: Tokens or characters.
- Non-terminal symbols: Symbols representing syntactic categories.

## From a Grammar to a Parser
The goal is to write parser code that resembles the grammar.

**Approach: Recursive-descent parsing**
- Each non-terminal becomes a parsing function.
- The type of a parsing function is `[Token] -> Bool` (for now).

**Recursive-descent Parsing:**
A problem with the grammar:
```
Expr ::= Expr + Expr
       | Expr - Expr
       | Expr * Expr
       | Expr / Expr
       | number
       | (Expr)
```

Problem: Left-recursion causes the parser to diverge.

**Our grammar "refactored" to remove left-recursion:**
```
Expr ::= Factor + Expr
       | Factor - Expr
       | Factor * Expr
       | Factor / Expr
       | Factor

Factor ::= number
         | (Expr)
```

A problem with the grammar:
```
Expr ::= Factor + Expr
       | Factor - Expr
       | Factor * Expr
       | Factor / Expr
       | Factor

Factor ::= number
         | (Expr)
```

Problem: All operators have the same precedence.

**Our grammar "refactored" to add precedence:**
```
Expr ::= Term + Expr
       | Term - Expr
       | Term

Term ::= Factor * Term
       | Factor / Term
       | Factor

Factor ::= number
         | (Expr)
```

A problem with the grammar:
```
Expr ::= Term + Expr
       | Term - Expr
       | Term

Term ::= Factor * Term
       | Factor / Term
       | Factor

Factor ::= number
         | (Expr)
```

Problem: All operators have right-associativity.

**Our grammar "refactored" to handle left-associativity:**
```
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

This grammar can help us with left-associativity.