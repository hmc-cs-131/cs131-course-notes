### CS 131: Programming Languages

# Type Systems

In this lecture, we will recap the concept of types and delve deeper into type systems. We'll explore how to represent possible types using grammars and understand the relationship between types and proofs.

## Representing Types with Grammars

Grammars provide a formal way to represent the syntax and structure of types. They specify the possible forms and combinations of types in a programming language. Although similar to Haskell syntax, the grammar notation used here is simplified. Recognizing a grammar as a specification is a valuable skill in programming languages.

## Types and Proofs

Types and proofs are interconnected in programming languages. Recall the concept of Natural Deduction from CS81, where premises are used to derive conclusions. Similarly, in type systems, typing rules allow us to infer the type of an expression based on premises. Typing rules define how types interact and provide a basis for type inference and checking.

## Typing Rules for Simple Expressions

Typing rules describe the types of expressions based on their structure. Let's start with simple expressions involving constants, such as true and false. These expressions have known types, so no premises are needed to determine their types.

We can then move on to more complex expressions and introduce typing rules for variables. These rules define the types of variables based on their declaration and usage in the program.

## Environments and Type Checking

Environments help us keep track of variables and their types. We maintain a value environment that maps variables to their values and a type environment that maps variables to their types. By using these environments, we can perform type checking and ensure that expressions and statements use variables of the correct types.

## Typing Rules: Examples

Let's apply the typing rules to various examples to demonstrate how they work in practice.

Example 1: We prove that `z :: int ⊢ 3 + 7 :: int`. We start with the typing rule for addition and use the typing rules for constants to establish the types of `3` and `7`. By following the typing rules and connecting the premises, we conclude that the expression `3 + 7` is of type `int`.

Example 2: We prove that `⊢ 3 + 7 :: int`. Here, no premises are given, but we still use the typing rules for constants to establish the types of `3` and `7`. By connecting the premises, we conclude that the expression `3 + 7` is of type `int`.

Example 3: We prove that `x :: int ⊢ if 2 < x then x else 5 :: int`. This example involves an if/then/else statement. We use the typing rules for comparison, variables, and constants to establish the types of the subexpressions and ensure that the overall expression is well-typed.

Example 4: We prove that `y :: bool ⊢ let x = 5 in x + 1 :: int`. This example introduces a let expression. We extend the type environment to include the type of the variable `x`. By following the typing rules for let expressions and addition, we establish the well-typedness of the expression.

## Subtypes and Substitutability

Subtyping is an important concept in type systems that allows for substitutability of types. Subtyping defines relationships between types, where one type is considered a subtype of another.

Subtyping enables substitutability, meaning that it is always safe to substitute a value of a subtype in place of a value of its supertype. This allows for more flexible and polymorphic programming.

### Subtyping with Functions

Subtyping also applies to functions. We can have subtyping relationships between function types,

 enabling us to substitute one function type with another. If one function type expects a more general type as an argument or produces a more specific type as a result, we can safely substitute it with a function type that expects or produces a subtype.

By defining subtyping rules for functions, we ensure that functions can be used in contexts where a more general or specific function type is expected.

## Any and None Types

In type systems, we often encounter special types called "Any" and "None."

The Any type is a generic type that encompasses all other types. It is a top type in the type lattice, meaning that all types are subtypes of Any. However, the Any type is not very informative because it provides little specific information about the actual type of a value.

The None type, on the other hand, is a bottom type in the type lattice. It is a subtype of all other types and represents the absence of a value. None is often used to indicate cases where there are no valid values of a particular type.

## Type Lattices

Type lattices visualize the subtype relationships between types in a flowchart-like structure. Types are represented as nodes in the graph, and subtyping relationships are shown by the relative heights of the nodes.

In a type lattice, if one type is below another type, it means that the lower type is a subtype of the higher type. This graphical representation helps us understand the hierarchy and relationships between types in a type system.

An example type lattice is presented, including Any and None types, to illustrate how subtyping relationships can be visualized.

Understanding type lattices and the relationships between types helps us reason about type compatibility, substitutability, and the overall structure of a type system.

This concludes our exploration of type systems. By understanding types, grammars, typing rules, and subtyping, we can effectively analyze, infer, and ensure the well-typedness of programs in various programming languages.