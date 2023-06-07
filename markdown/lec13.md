### CS 131: Programming Languages

# Functors and Monads Review

## Refactoring Our Parser Combinator Library

#### Refactoring Combinators

We start by reviewing the existing combinators we implemented in the previous lecture. These combinators are similar but differ in their types and how they combine results. Our goal is to refactor these combinators to eliminate code duplication and reduce direct state manipulation. Refactoring will make our code easier to modify and less error-prone.

### Parser Combinator Refactoring

#### Common Structure

Upon closer examination, we observe that several combinators have a similar structure. When a parser is applied to an input, certain actions occur based on the success or failure of the parser. We can identify common elements in these actions and abstract them away.

#### Generalizing the Next Step

We can think of the next step after parsing as a function that takes the elements of the parse state and produces a new parse state. This function takes the parse result and the remaining input as arguments and returns a new parse state. By using type variables, we generalize this function to be of type `A -> Parser B`.

#### Introducing the Bind Operator

To encapsulate this idea, we introduce a new operator called the "bind" operator. Its syntax is `>>=`, represented as "greater than greater than equals." The bind operator takes a parser `A` and a function from `A` to `Parser B`, returning a `Parser B`. This operator simplifies the implementation by automatically passing the successful state to the next step.

### Using the Bind Operator

Now, let's explore how to use the bind operator to define new parsing operations. Suppose we have a parser for lowercase letters called `letter`. To convert the parsed letter to uppercase, we can use the bind operator with the function `toUpper`. Using the `return` function, we can convert the uppercase letter into a parser. This operation can be further simplified using the `bind:` operator, which combines the bind operator with function composition. This operator provides a convenient way to transform parsed results without explicitly using the `return` function.

#### Sequencing Parsers

The bind operator is also useful for sequencing parsers. For example, we can parse `P1` and then parse `P2`, combining their results into a pair. By chaining the bind operator, we can run multiple parsers sequentially and retrieve their results without explicit error checking. This technique simplifies the implementation of combinators such as the `<:>` and `<++>` operators.

### Parser Combinator Core

Let's now delve into the core components of our parser combinator library. The `Parser` interface consists of a parser type parameterized by its parse result. The `parse` function takes a parser, an input string, and returns either a parse result or an error if parsing fails.

#### Core Functions and Combinators

We have a basis of simple parsing functions and combinators:

1. `get`: Retrieves a single character from the input.
2. `return`: Constructs a parser that always succeeds and returns a given value.
3. `pfail`: A

 parser that always fails.
4. `<+>`: Combines two parsers and produces a parser that accepts either of their inputs.
5. `<:>`: Combines a single value parser with a list parser, returning the combined result.
6. `<++>`: Concatenates two list parsers and produces a parser that returns the combined list.

### Refactoring Our Parser Library

With the core components and combinators defined, let's continue by refactoring our parser library. We'll incorporate the `<+>`, `<:>`, and `<++>` combinators, as well as the `get`, `return`, and `pfail` functions, using the monadic approach.

#### The `<+>` Combinator

The `<+>` combinator allows us to combine two parsers and produce a parser that accepts either of their inputs. It has the following type signature:

```haskell
(<+>) :: Parser a -> Parser b -> Parser (a, b)
```

Here's an example usage of the `<+>` combinator:

```haskell
parse (digit <+> letter) "1a"
-- Output: ('1', 'a')
```

To implement `<+>`, we can utilize the monadic operations `>>=` and `return`. Here's the refactored implementation:

```haskell
(<+>) :: Parser a -> Parser b -> Parser (a, b)
(p1 <+> p2) s =
 case p1 s of
   Nothing -> Nothing
   Just (result1, s') -> case p2 s' of
                           Nothing -> Nothing
                           Just (result2, s'') -> Just ((result1, result2), s'')
```

#### The `<:>` Combinator

The `<:>` combinator combines a single value parser with a list parser. It applies the value parser and then the list parser, producing a parser that returns the combined result. Its type signature is as follows:

```haskell
(<:>) :: Parser a -> Parser [a] -> Parser [a]
```

Here's an example usage of the `<:>` combinator:

```haskell
parse (digit <:> letters) "1abc"
-- Output: "1abc"
```

To implement `<:>`, we can utilize the monadic operations `>>=` and `return`. Here's the refactored implementation:

```haskell
(<:>) :: Parser a -> Parser [a] -> Parser [a]
(p1 <:> p2) s =
 case p1 s of
   Nothing -> Nothing
   Just (result1, s') -> case p2 s' of
                           Nothing -> Nothing
                           Just (result2, s'') -> Just (result1 : result2, s'')
```

#### The `<++>` Combinator

The `<++>` combinator concatenates two list parsers and produces a parser that returns the combined list. It has the following type signature:

```haskell
(<++>) :: Parser [a] -> Parser [a] -> Parser [a]
```

Here's an example usage of the `<++>` combinator:

```haskell
parse (digits <++> letters) "123abc"
-- Output: "123abc"
```

To implement `<++>`, we can utilize the monadic operations `>>=` and `return`. Here's the refactored implementation:

```haskell
(<++>) :: Parser [a] -> Parser [a] -> Parser [a]
(p1 <++> p2) s =
 case p1 s of
   Nothing -> Nothing
   Just (result1, s') -> case p2 s' of
                           Nothing -> Nothing
                           Just (result2

, s'') -> Just (result1 ++ result2, s')
```

### Conclusion

In this lecture, we explored monadic parsing and refactored our parser library to incorporate monadic operations and combinators. We learned about the `<+>`, `<:>`, and `<++>` combinators and their usage in building parsers. By using monadic parsers, we can handle complex input structures and process them according to specific grammar rules. The bind operator, along with the core functions and combinators, forms the foundation of our parser combinator library. By refactoring and generalizing common patterns, we have simplified the implementation and reduced code duplication. This modular and extensible library allows for efficient parsing of different programming language constructs.

## Exercises

Let's consider some exercises to test our understanding of monads in the `Maybe` monad.

1. **Exercise 1**
   ```haskell
   e1 :: Maybe Integer
   e1 = do
     v <- value
     return (v + 1)
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

2. **Exercise 2**
   ```haskell
   e2 :: Maybe Integer
   e2 = do
     let v = value
     return (v + 1)
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

3. **Exercise 3**
   ```haskell
   e3 :: Maybe Integer
   e3 = do
     let v = value
     return v
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

4.

 **Exercise 4**
   ```haskell
   e4 :: Maybe Integer
   e4 = do
     let v = value
     v
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

5. **Exercise 5**
   ```haskell
   e5 :: Maybe Integer
   e5 = do
     v <- value
     let v' = value + 1
     return v'
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

6. **Exercise 6**
   ```haskell
   e6 :: Maybe Integer
   e6 = do
     v <- value
     let v' <- value + 1
     return v'
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

7. **Exercise 7**
   ```haskell
   e7 :: Maybe Integer
   e7 = do
     v <- value
     v' <- value + 1
     return v'
   ```
   Given `value :: Maybe Integer` where `Maybe` is a monad, is the expression correct or incorrect? If correct, what is the result? If incorrect, what is the problem, and how should we fix it?

In these exercises, we're exploring different scenarios of working with the `Maybe` monad and how it handles computations with potential missing values. Understanding these exercises will help solidify our understanding of monadic computations and their behavior in the `Maybe` monad.