# Key Terms in CS 131
_This document is meant to provide an overview of some key terms that will be used frequently across CS 131. Terms are alphabetized. By referring to these definitions, you can deepen your understanding of various programming concepts and the principles behind Haskell and functional programming._

**Abstract Syntax Tree (AST)** (noun): An Abstract Syntax Tree (AST) is a hierarchical representation of the structure and meaning of a program. It captures the essential syntax and semantics of the code, providing a more abstract and structured view. The AST represents the program as a tree-like data structure, where each node represents a construct such as an expression, statement, or declaration. The AST is commonly used for program analysis, optimization, and transformation in compiler and interpreter implementations.

**Abstract syntax** (noun): Abstract syntax captures the essential structure and meaning of code, stripped of unnecessary details present in concrete syntax. It represents programs as structured data, typically in the form of abstract syntax trees (ASTs). Abstract syntax provides a clear and unambiguous representation of code, focusing on the logical structure and semantics of the program. It serves as a basis for analysis, transformations, and interpretation of programs, abstracting away the specific details of the concrete syntax.

**Alpha-Equivalence** (α-Equivalence) (noun): Alpha-equivalence refers to the notion of renaming variables in a lambda expression without changing its meaning. It allows us to consider two lambda expressions equivalent even if they differ in variable names. Alpha-equivalence ensures that the choice of variable names does not affect the behavior or semantics of a lambda expression. It provides a way to reason about lambda expressions without being concerned with specific variable names, promoting clarity and consistency in lambda calculus and functional programming.

**Ambiguous** (adjective): Something that can have multiple meanings or interpretations.

**Application** (noun) or **apply** (verb): The use of an operator in an expression.

**Associativity** (noun): The rule that disambiguates an expression with multiple applications of the same operator. There are two types of associativity: - Left associativity: Resolves the ambiguity by evaluating the left-most application first. - Right associativity: Resolves the ambiguity by evaluating the right-most application first.

**Babbage, Charles** (1791-1871): Charles Babbage was an English mathematician, philosopher, and mechanical engineer. He is often referred to as the "father of the computer" for his work on mechanical computing devices. Babbage designed and conceptualized the Analytical Engine, a mechanical general-purpose computer that was never fully built during his lifetime. His pioneering ideas and designs laid the groundwork for modern computers and computational methods. Babbage's contributions revolutionized the field of computing and he is regarded as one of the most important figures in the history of computing.

**Back End** (noun): The back end focuses on semantics and program execution.

**Beta-Reduction** (β-Reduction) (noun): Beta-reduction (β-reduction) is a fundamental operation in lambda calculus and functional programming. It involves replacing occurrences of bound variables in a lambda expression with their corresponding arguments. Beta-reduction enables the evaluation of lambda expressions and the application of functions to arguments. The process is guided by the pattern of a function application, where the function is applied to its arguments by substituting the arguments for the bound variables in the function body. 

**Bind operator** (noun): The bind operator (`>>=`) is a fundamental operator in monadic programming. It allows sequential composition of computations within a monadic context. It takes a value wrapped in a monad and a function that maps a value to another monadic computation, returning a new monadic computation. The bind operator enables chaining multiple monadic actions, where the output of one action becomes the input to the next. It structures and sequences computations in a monadic context.

**Binding** (noun): Binding associates a variable name with an expression. This is similar to assignment (noun) and assign (verb), which we often see in imperative programming languages.

**Call-by-Name Evaluation** (noun): Call-by-Name evaluation is an evaluation strategy in programming languages where the arguments to a function are substituted unevaluated into the function body. The unevaluated expressions are passed as-they-are to the function. Within the function, the expressions are evaluated if and when they are needed. Call-by-Name evaluation allows for delayed evaluation and can be useful in scenarios where the arguments may not be needed in certain branches of the function or if the arguments have side effects that should be avoided. This evaluation strategy provides flexibility in terms of when and how the arguments are evaluated.

**Call-by-Value Evaluation** (noun): Call-by-Value evaluation is an evaluation strategy in programming languages where the arguments to a function are evaluated before substituting them into the function body. This approach ensures that the values of the arguments are determined before entering the function. The evaluated values are then used within the function. In call-by-value evaluation, each argument is evaluated exactly once. This evaluation strategy provides predictable behavior and is commonly used in many programming languages.

**Church, Alonzo** (1903-1995): Alonzo Church, an American mathematician and logician, contributed significantly to our understanding of computation through his development of lambda calculus. Lambda calculus is a formal system for manipulating symbols, with a specific focus on functions. It explores the structure and form of expressions, emphasizing the shape of functions. Church's work in lambda calculus delved into the boundaries of computability, revealing both the expressive power and limitations of the system. He demonstrated that there are computations that lambda calculus cannot express or compute, highlighting the concept of incompleteness within the system. Church's contributions to lambda calculus have had a profound impact on mathematical logic and the foundations of computer science.

**Closure** (noun): In programming languages, a closure is a function that captures and "closes over" the variables and bindings from its surrounding environment. It includes both the function itself and the environment in which it was defined. The closure allows the function to access and retain references to variables that were in scope at the time of its creation, even when called in a different context or scope. This enables functions to maintain their own private state and access variables that would otherwise be out of scope. Closures are particularly useful in functional programming and when working with higher-order functions, as they enable powerful and flexible control over variable scoping and encapsulation.

**Concatenation Operator** (noun): In functional programming and specifically in Haskell, the concatenation operator `++` is used to combine two lists into a single list by appending the elements of the second list to the end of the first list. It is written as `list1 ++ list2`, where `list1` and `list2` are the lists being concatenated. The concatenation operator allows for the creation of larger lists by joining multiple smaller lists together.

**Concrete syntax** (noun): Concrete syntax refers to the specific form of code as written by the programmer. It encompasses the keywords, punctuation, and specific character sequences that make up the code. Concrete syntax allows programmers to write programs in a human-readable and familiar form, using the language's predefined syntax rules and constructs.

**Cons Operator** (noun): In functional programming and specifically in Haskell, the cons operator `:` is used to construct a new list by adding an element to the front of an existing list. It is written as `element : list`, where `element` is the value to be added and `list` is the existing list. The cons operator is a fundamental operation for manipulating lists in functional programming languages.

**Curry** (verb): In programming languages, currying refers to the process of transforming a function that takes multiple arguments into a sequence of functions, each taking a single argument. The currying process involves breaking down a function with multiple arguments into a series of nested functions, where each function takes one argument and returns a new function that expects the remaining arguments. The name "currying" is derived from the mathematician Haskell Curry, who introduced this concept. 

**Data Type** (noun): A data type classifies and organizes data by defining the set of values it can hold and the operations that can be performed on those values. In Haskell, data types are static and strongly typed. They can be built-in (like `Int` and `Bool`) or user-defined using the `data` keyword. Data types ensure data integrity and enable type checking, facilitating reliable and maintainable code.

**Declarative Model** (noun): Declarative languages allow programmers to describe what they want without focusing on how to achieve it. SQL (Structured Query Language) is a popular declarative language used for database operations. Declarative languages often target specific domains and problem areas.

**Disambiguate** (verb): To resolve an ambiguity by choosing one specific meaning or interpretation.

**Do Notation** (noun): Do notation is a syntactic sugar in Haskell that provides a convenient way to sequence and compose monadic actions. It simplifies working with monads by allowing imperative-style code to be written in a more readable and structured manner. Do notation is commonly used with monads like `IO`, `Maybe`, and `Either` to perform sequential computations and handle potential effects. It enhances code readability and maintainability by abstracting away the underlying monadic structure.

**Dynamic Scope** (noun): Dynamic scope is a variable scoping mechanism that uses the closest enclosing scope at runtime to look up and determine the value of local variables. The value of a variable is determined by the current state of the runtime call stack. Changes to the value of a variable in one part of the program can affect its value in other parts of the program that call the same function. Dynamic scope provides flexibility in accessing variables, but it can also lead to unpredictable behavior and make code more difficult to reason about.

**Dynamic** (adjective): Dynamic properties of a program are determined by running the program. Dynamic type checking can occur during program execution and may result in runtime errors if type inconsistencies are encountered.

**Dynamically typed** (adjective): In dynamically typed programming languages, type checking may occur at runtime. Interpreters or runtime systems perform checks on types as the program executes. If a type error is encountered, the program may crash or raise runtime errors.

**Eager (or strict) evaluation** (noun): Eager (or strict) evaluation refers to a form of computation where subexpressions are evaluated before they are assigned or used in function calls.

**Environment** (noun): In programming languages, an environment is a data structure that associates names with their corresponding values or expressions. It serves as a mapping between identifiers and their bindings within a specific scope. The environment provides a mechanism for storing and retrieving the values of variables or references to functions. It is used during the evaluation of expressions to resolve names and access the associated values or expressions. The environment plays a crucial role in managing the state and scope of variables and functions within a program.

**Evaluate** (verb): Evaluate is the process of attempting to compute the result of an expression.

**Expression** (noun): An expression is a "piece of computation" in functional programming, such as `1 + 2` or `f 3`.

**Filter Function** (noun): In functional programming and specifically in Haskell, the `filter` function is a higher-order function that selects elements from a list based on a specified predicate or condition, producing a new list with the selected elements. It has the type signature `(a -> Bool) -> [a] -> [a]`, where the first argument is the predicate function that determines which elements to keep, and the second argument is the input list. The `filter` function provides a powerful mechanism for extracting elements that satisfy a given condition from a list, enabling concise and expressive list filtering operations.

**Fixity Declaration** (noun): A fixity declaration is a feature in Haskell that allows you to specify the associativity and precedence of operators. It helps disambiguate expressions with multiple operators and ensures they are evaluated in the desired order.

**Front End** (noun): The front end handles the concrete syntax and includes parsing.

**Function Composition** (noun): In programming languages, function composition refers to combining multiple functions to create a new function. It involves applying the output of one function as the input to another function, creating a chain or pipeline of functions. Function composition enables the creation of complex functions by combining simpler ones, promoting code reusability and modularity.

**Functional Model** (noun): The functional model treats computation as the evaluation of expressions. Haskell, Racket, and ML are functional languages. Functional languages resemble mathematical approaches to problem-solving.

**Functor** (noun): In functional programming, a functor is a typeclass that represents a container or context that can be mapped over. It provides a way to apply a function to the values inside the container while preserving the container's structure. Functors enable composition and transformation of values within a context, allowing for concise and reusable code. The main operation of a functor is fmap, which takes a function and applies it to the values inside the functor, producing a new functor with the transformed values. 

**GHCi** (noun): GHCi stands for Glasgow Haskell Compiler interactive environment. It is an interactive shell for running Haskell code, testing expressions, and exploring language features.

**Gödel, Kurt** (1906-1978): Kurt Gödel, an Austrian mathematician and logician, is renowned for his incompleteness theorem, published in 1931. This theorem demonstrated that in any consistent formal system containing arithmetic, there exist true statements that cannot be proven within that system. Gödel's work shattered the dream of a complete and consistent mathematical system, as envisioned by mathematicians like David Hilbert. His contributions have had a profound impact on logic, philosophy, and computer science, challenging the boundaries of mathematical reasoning and human knowledge.

**Grammar** (noun): A grammar is a set of rules that defines the structure and syntax of a programming language or any other formal language. It specifies the valid combinations and patterns of symbols or tokens that make up the language. In the context of parsing, a grammar describes the syntactic rules that govern the formation of valid expressions and statements in a programming language. It defines the syntax in terms of production rules, specifying how different language elements can be combined to form valid constructs.

**Higher-order Function** (noun): In functional programming, a higher-order function is a function that can take one or more functions as arguments and/or return a function as its result. It treats functions as first-class citizens, allowing them to be manipulated and used as values. Higher-order functions enable powerful abstractions and expressive programming paradigms, such as function composition, partial application, and currying. They play a central role in functional programming and enable writing more modular and reusable code.

**Hilbert, David** (1862-1943): David Hilbert, a renowned German mathematician, made significant contributions to algebra, number theory, mathematical logic, and the foundations of mathematics. He famously declared, "We must know. We will know," reflecting his firm belief in the power of mathematics to uncover truths and solve problems. Hilbert aimed to establish a complete and consistent foundation for mathematics through rigorous axiomatic systems. However, Kurt Gödel's incompleteness theorem, published in 1931, shattered Hilbert's dream. Gödel's theorem showed that in any sufficiently complex formal system, there will always be true statements that cannot be proven within that system. This profound result revealed the inherent limitations of formal systems and the existence of unprovable truths.

**Imperative Model** (noun): The imperative model centers around data and memory manipulation. Examples of imperative languages include C, Java, Python, OCaml, Swift, and JavaScript.

**Lambda Calculus** (noun): Lambda calculus is a formal system for expressing computation based on function abstraction and application using lambda expressions. It serves as a foundation for studying and understanding computation and programming languages. Lambda calculus consists of variables, lambda abstractions (functions), and function application, along with reduction rules (such as β-reduction) for evaluating expressions. It provides a simple yet powerful framework for reasoning about computation and has influenced the development of functional programming languages.

**Lazy evaluation** (noun): Lazy evaluation refers to a form of computation where subexpressions are evaluated only when their results are needed.

**List** (noun): In programming, a list is an ordered collection of elements. It allows storing and accessing data in a sequential manner. Lists are commonly used for organizing and manipulating data in various programming languages.

**Local bindings** (noun): These bindings have a limited scope within a function or a `let` expression.

**Lookup** (verb) or **resolve** (verb): Evaluate a name and find its value.

**Lovelace, Ada** (1815-1852): Ada Lovelace, born Augusta Ada Byron, was an English mathematician and writer. She is recognized as the world's first computer programmer for her work on Charles Babbage's Analytical Engine. Lovelace's visionary ideas laid the foundation for modern programming. In 1843, she wrote the first computer program, an algorithm for calculating Bernoulli numbers. Lovelace's contributions have had a lasting impact on computer science and she remains an inspiration for women in STEM fields.

**Map Function** (noun): In functional programming and specifically in Haskell, the `map` function is a higher-order function that applies a given function to every element of a list, producing a new list with the transformed elements. It has the type signature `(a -> b) -> [a] -> [b]`, where the first argument is the function to be applied and the second argument is the input list. The `map` function allows for concise and expressive transformations on lists, applying the provided function to each element in a uniform manner.

**Maybe** (noun): The `Maybe` type is a common type in Haskell and other functional programming languages used to represent the possibility of a value being present (`Just`) or absent (`Nothing`). It is often used when dealing with computations that may or may not produce a result. The `Maybe` type is defined as a sum type with two constructors: `Just` to wrap a value and indicate its presence, and `Nothing` to represent the absence of a value. It provides a way to handle potential absence or failure in a type-safe manner, allowing for more expressive and robust code.

**Middle** (noun): The middle represents the abstract syntax, a structured representation of the program.

**Monad** (noun): In functional programming, a monad is a programming construct that facilitates composition and sequencing of computations. It provides a way to encapsulate and manage effects, such as state, error handling, or non-determinism, in a controlled and composable manner. Monads provide a set of operations, such as `return` and `bind` (also known as `>>=`), that enable chaining of computations and handling of potential side effects. They promote code modularity, reusability, and maintainability by separating the concerns of computation and effects. Monads are a fundamental concept in Haskell and other functional programming languages, enabling elegant and expressive programming patterns.

**Normal Form** (noun): A lambda expression is in normal form if it cannot undergo any further β-reduction. It represents the fully evaluated and simplified state of an expression.

**Operand** (noun): A value or entity that is operated upon by an operator.

**Operator** (noun): A symbol or keyword that represents a specific operation to be performed on one or more operands.

**Parametrized Types** (noun): Parametrized types, also called generic types, are types that can take one or more type parameters. These parameters represent placeholders for specific types. Parametrized types enable code reuse by defining generic algorithms and data structures that can operate on different types.

**Parser Combinators** (noun): Parser combinators are a technique in functional programming for building parsers by combining smaller parsers into larger ones. They enable concise and modular parsing logic by using high-order functions to compose parsers. Parser combinators promote code reuse and expressiveness, making it easier to write and maintain parsers.

**Parsing**: Parsing is the process of converting concrete syntax into abstract syntax by analyzing the structure of code and constructing an abstract syntax tree (AST). It is performed by a parser, a software component responsible for interpreting the code and generating the AST. Parsing is crucial for further code analysis, interpretation, or compilation.

**Pattern matching** (noun): Pattern matching is a feature in Haskell that allows you to match the structure of data against predefined patterns. It provides a concise way to deconstruct complex data types and extract relevant information.


**Precedence** (noun): The rule that determines how to disambiguate an expression containing applications of different operators.

**Pure Expression** (noun): An expression that has no side effects and produces a result solely based on its inputs.

**Reference** (verb): Using a name in an expression. During evaluation, the name acts as an alias for the expression.

**Referentially Transparent** (adjective): A property of a sub-expression that allows it to be replaced with its result without impacting the overall result of the surrounding expression.

**Scope** (noun): The region of the program where a name can be referenced. A variable's scope depends on where it is bound. In Haskell, a scope can bind a name at most once. In other words, all "variables" are constants!

**Semantics** (noun): Semantics pertains to the meaning and behavior of code in a programming language. It describes how programs are interpreted and executed, including the effects and outcomes of various language constructs and operations. Semantics determine the behavior of code at runtime, such as the interpretation of operators and the execution of statements. For instance, the `^` operator, when applied to two integers, performs bitwise exclusive-or according to the semantics defined by the language.

**Side effect** (noun): Any action during expression evaluation that changes the state of the program or the external environment. Examples include modifying a variable's value or printing output.

**Static Scope** (noun): Static scope, also known as lexical scope, is a variable scoping mechanism that uses the lexical structure of the program to determine the scope of variables. The value of a variable is determined by its declaration in the source code. Variables are bound to their closest enclosing scope at the time of their declaration and remain bound to that scope throughout the execution of the program. Static scope provides predictability and a clearer understanding of how variables are scoped, as the scope is determined by the structure of the program rather than the runtime state.

**Static** (adjective): In Haskell, type checking is a static process, meaning it can be determined without running the program. The compiler performs type checking during the compilation phase, analyzing the program's types before execution.

**Statically typed** (adjective): Haskell is a statically typed programming language, which means it performs static type checking. The compiler checks the types of expressions, variables, and functions, ensuring type consistency throughout the program. If a type error is found, the program fails to compile.

**Substitution** (noun): Substitution is a fundamental concept in programming and formal languages. It refers to the process of replacing occurrences of a variable or expression with another variable, expression, or value. Substitution is commonly used in various contexts, such as variable assignment, parameter passing, and expression evaluation. It allows for the manipulation and transformation of code by replacing specific elements with their corresponding values or representations.

**Syntax** (noun): Syntax refers to the rules and structure of a programming language that determine how programs are written or expressed. It defines the permissible arrangements of symbols, keywords, and constructs in code. Syntax governs the overall structure, grammar, and composition of the language. For example, in C++, the `^` symbol is a valid binary operator according to the language's syntax.

**Termination** (noun): Termination refers to the outcome of evaluating an expression. It can either terminate with a result or diverge (run forever).

**Tokenization** (noun): Tokenization is the process of breaking down the concrete syntax of a program into individual tokens. Tokens are the smallest and most atomic units of code that have meaning in the programming language. During tokenization, the input program is divided into distinct tokens, which can include literals, numbers, strings, punctuation, identifiers, operators, reserved words, and whitespace. Tokenization serves as a preliminary step in the parsing process, as the resulting tokens are then used as input for further analysis and processing.

**Top-level bindings** (noun): Similar to global variables, these bindings have a scope that extends throughout the entire file or the rest of the GHCi (Glasgow Haskell Compiler interactive environment) session.

**Tuple** (noun): In programming, a tuple is an ordered collection of elements, typically of different types. Tuples are immutable, meaning their values cannot be modified once they are created. They are commonly used for grouping related data together. Unlike lists, tuples are fixed in size and provide a way to represent heterogeneous data structures.

**Turing, Alan** (1912-1954): Alan Turing, a British mathematician and computer scientist, made groundbreaking contributions to the understanding of computation. He proposed the concept of Turing machines, which are abstract state machines capable of universal computation. Turing machines operate by transitioning between states and manipulating symbols on an infinite tape. They provided a theoretical framework for studying computation and played a crucial role in the development of computer science. Turing also investigated the limitations of Turing machines, particularly through his exploration of the halting problem, which demonstrated the existence of undecidable problems in computation.

**Type annotation** (noun): Type annotations provide explicit information about the types of variables, functions, or expressions. Programmers can annotate their code with type declarations to provide hints to the compiler or improve code clarity.

**Type Conflict** or **Type Error** (noun): A type conflict, also known as a type error, occurs when there is a mismatch between the expected and actual types of values in a program. It represents a violation of the type rules defined by the type system. Type conflicts can arise when performing incompatible operations, passing arguments of incorrect types to functions, or assigning values of different types to variables. Type conflicts are detected during the compilation phase in statically typed languages, preventing the execution of code that may lead to runtime errors or unexpected behavior.

**Type inference** (noun): Haskell features powerful type inference capabilities, allowing the compiler to deduce types without extensive type annotations. Type inference reduces the need for explicit type declarations while maintaining type safety.

**Type System** (noun): A type system is a set of rules that governs the usage of types in a programming language. It assigns types to variables, expressions, and functions, ensuring compatibility and detecting type errors. 

**Type** (noun): A type is a concept in programming that serves multiple purposes. Firstly, types allow us to abstract a collection of individual data pieces, providing a way to discuss properties and operations associated with them. Secondly, types define what data is and what can be done with it by establishing a set of allowed values and fundamental operations. They impose constraints on the behavior and capabilities of values. Thirdly, types act as labels and provide context for data, helping us understand the intended use and interactions with specific data. Lastly, types can be composed to create more complex types by combining base types, enabling the representation of structured data.

**Type-check** (verb): To determine whether a program has type errors, the process of type checking is performed. Type checking ensures that the types of expressions, variables, and functions are consistent and compatible.

**Type-safe** (adjective): A program is considered type-safe when it has no type errors. Type errors occur when there is a mismatch between the expected and actual types of values in the program.

**Typeclass** (noun): In Haskell, typeclasses define common behavior for different types, allowing the use of generic functions and operations. They serve as interfaces or contracts specifying expected behavior from types that are instances of the typeclass. Typeclasses facilitate polymorphism and code reuse. Some common typeclasses include `Eq`, `Ord`, `Show`, `Read`, `Num`, `Functor`, `Monad`, `Applicative`, `Foldable`, and `Traversable`. These typeclasses enable equality comparison, ordering, conversion to strings, arithmetic operations, mapping over values, sequencing computations, combining computations, folding data structures, and traversing data structures, respectively. They form the foundation for generic programming in Haskell, promoting code abstraction and modularity.

**Value** (noun): The expression to which a name is bound.

**Variable name** (noun): The name given to a variable. In Haskell, variable names are written in lowercase.

**Well-Typed Program** (noun): A well-typed program is a program that adheres to the rules and constraints of the type system. It implies that all expressions, variables, and functions in the program have consistent and compatible types. In a well-typed program, type conflicts and type errors are eliminated, ensuring type safety and preventing runtime errors caused by type mismatches. Well-typed programs can be statically verified by the compiler, giving developers confidence in the correctness and reliability of their code.

**Wildcard** (noun): In Haskell, a wildcard is represented by an underscore (`_`) and is used as a placeholder in patterns or expressions. It allows the programmer to ignore or match any value of a certain position or type. The wildcard is useful when the specific value is not needed or when writing partial patterns or expressions. It acts as a "catch-all" and can help simplify code by avoiding the need to specify unnecessary details.

**Y Combinator** (noun): The Y combinator is a higher-order function in lambda calculus that enables the definition of recursive functions. It provides a way to express recursion without using traditional recursive definitions. The Y combinator takes a function as an argument and returns its fixed point, which is a function that behaves the same as the original function but can call itself recursively. The Y combinator is a powerful construct that demonstrates the expressive power of lambda calculus and functional programming languages. It plays a fundamental role in understanding recursion and defining recursive computations in lambda calculus.