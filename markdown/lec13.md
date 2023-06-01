### CS 131: Programming Languages

# Functors and Monads Review

In this review, we will revisit the concepts of functors and monads. Functors and monads are powerful abstractions in functional programming that enable us to work with parameterized types in a structured and compositional manner.

## Parameterized Types

Let's start with a reminder about parameterized types. Parameterized types, such as `Maybe a`, `[a]`, and `Tree a`, allow us to create types that can hold values of any type `a`. For example, `Maybe a` represents a value that can either be `Nothing` or `Just x`, where `x` is a value of type `a`. Similarly, `[a]` represents a list of values of type `a`, and `Tree a` represents a binary tree with values of type `a`.

## Functors

Functors are a typeclass that defines the `fmap` function, allowing us to apply a function to each element within a parameterized type while preserving the structure.

```haskell
fmap :: Functor f => (a -> b) -> f a -> f b
```

The `fmap` function takes a function `(a -> b)` and a parameterized type `f a` and returns a new parameterized type `f b`. It applies the function to each element within the structure and returns the updated structure.

Functors provide a way to perform transformations on parameterized types without unwrapping and rewrapping them. They allow us to work with different data structures in a uniform way.

## Monads

Monads are another typeclass that provides a way to sequence computations and handle effects within a parameterized type. Monads encapsulate computations within a context and provide operations to compose these computations in a structured manner.

The key operations in monads are `(>>=)` (bind) and `return`. `(>>=)` allows us to chain computations together. It takes a monadic value, extracts the value inside it, and applies a function that produces a new monadic value. `return` allows us to lift pure values into the monadic context.

Monads enable us to handle effects, such as IO, error handling, and non-determinism, in a controlled and modular way. They provide a structured approach to sequencing actions, handling failures, and managing state.

## Exercise

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