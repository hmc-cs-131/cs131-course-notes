# CS131: Programming Languages

## Functional Abstractions

Hello! In this lecture, we will explore functional abstractions in Haskell. We'll cover important concepts such as typeclasses, functors, monads, and the do notation. These concepts provide powerful tools for writing reusable and composable code. So let's dive in!

### Typeclasses

Typeclasses in Haskell allow us to define common behavior for different types. They provide a way to generalize functions and operations that can work with various data types. We can think of typeclasses as interfaces or contracts that specify the behavior expected from types that are instances of the typeclass.

Let's take a look at some examples of typeclasses:

- **Eq**: The `Eq` typeclass defines equality and inequality operations. Instances of this typeclass can be compared for equality using the `==` operator.

- **Show**: The `Show` typeclass provides a way to convert values to strings. Instances of this typeclass can be converted to strings using the `show` function.

- **Read**: The `Read` typeclass enables conversion from strings to values. Instances of this typeclass can be created from strings using the `readsPrec` function.

- **Ord**: The `Ord` typeclass is used for types that can be compared. Instances of this typeclass can be compared using operators like `<=`, `<`, `>=`, `>`.

- **Num**: The `Num` typeclass represents numeric types and provides operations like addition (`+`), subtraction (`-`), multiplication (`*`), and more.

- **Fractional**: The `Fractional` typeclass is used for fractional numbers and provides division (`/`) and other related operations.

### Functors

Functors in Haskell represent data structures that can be mapped over. They define the `fmap` function, which allows us to apply a function to each element within the structure while preserving the structure itself.

Let's consider an example of a functor: lists. We can use the `fmap` function to apply a function to each element of a list. This operation is often referred to as mapping over the list.

```haskell
fmap :: Functor f => (a -> b) -> f a -> f b
```

Functors provide a way to perform common transformations on data structures without unwrapping and rewrapping them.

### Monads

Monads are a powerful abstraction in functional programming that enable sequencing of computations. They encapsulate computations within a context and provide operations to compose these computations in a structured manner.

The key operation in monads is `(>>=)`, pronounced as "bind," which allows us to chain computations together. It takes a monadic value, extracts the value inside it, and applies a function that produces a new monadic value.

Monads also provide the `return` function, which takes a value and wraps it in a monad. It allows us to lift pure values into the monadic context.

Monads enable us to handle effects, such as IO, error handling, and non-determinism, in a controlled and modular way. They provide a way to sequence actions, handle failures, and manage state.

### Do Notation

The do notation is a convenient syntax for working with monadic computations. It allows us to write imperative-style code in a monadic context, making it easier to understand and reason about sequential operations.

In the do notation, we can use the `<-` symbol to bind the result of a monadic computation to a variable. We can then use this variable in subsequent computations. The do notation takes care of unwrapping and rewrapping monadic values automatically.

The do notation is particularly useful when working with IO operations

. It provides a clear and concise way to express sequences of input/output actions.

Let's consider an example of using the do notation with the IO monad:

```haskell
reverseInput :: IO ()
reverseInput = do
  putStr "Enter a string: "
  input <- getLine
  let reversed = reverse input
  putStrLn ("Reversed string: " ++ reversed)
```

In this example, we prompt the user for a string, read the input using `getLine`, reverse the string, and then print the reversed string using `putStrLn`. The do notation helps us express this sequential flow of IO actions in a readable and intuitive way.

### IO in Haskell

IO is a special monad in Haskell that allows us to perform input and output operations. It represents computations that interact with the external world, such as reading from the console, writing to files, or making network requests.

In Haskell, IO operations are executed in a controlled manner to ensure referential transparency and purity. IO actions can be composed using monadic operations like `(>>=)` and `return`, and the do notation provides a convenient syntax for working with IO computations.

The IO monad has a type `IO a`, where `a` represents the type of the result produced by the IO action. For example, an IO action that reads a string from the console has the type `IO String`, and an IO action that performs some output has the type `IO ()` (unit type).

IO operations are executed when they are sequenced in a do block and invoked using the `main` function, which is the entry point of a Haskell program. The main function must have the type `IO ()` to indicate that it performs IO operations but does not produce any meaningful result.

### Recap

In this lecture, we covered important functional abstractions in Haskell, including typeclasses, functors, monads, and the do notation. Typeclasses provide a way to define common behavior for different types, allowing us to write generic functions. Functors enable mapping over data structures, applying functions to each element while preserving the structure. Monads facilitate sequencing of computations and handling effects in a modular way. The do notation provides a convenient syntax for working with monadic computations, making them easier to read and understand.

By leveraging these functional abstractions, we can write expressive and reusable code in Haskell, taking advantage of its strong type system and purity guarantees.