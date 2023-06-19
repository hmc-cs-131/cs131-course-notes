### CS 131: Programming Languages

# Syntax, semantics, evaluation of simple expressions


## Syntax, Abstract Syntax, and Semantics

In our previous lecture, we discussed the fundamental concepts of syntax, abstract syntax, and semantics, which play a crucial role in understanding programming languages. Let's recap the key ideas:

- **Code as Data**: We introduced the concept that code is data, meaning that we can represent code using data structures. This perspective allows us to manipulate and analyze code using the principles of data manipulation.

- **Concrete Syntax**: Concrete syntax refers to the textual representation of code that the programmer writes. It consists of the sequence of characters or strings that make up the program.

- **Abstract Syntax**: Abstract syntax is a tree-like data structure that encodes the programmer's code in an unambiguous manner. It captures the underlying structure and meaning of the code without the noise of concrete syntax. In other words, it represents the essential components and relationships of the program.

- **Parsing**: Parsing is the process of converting concrete syntax into abstract syntax. It involves constructing the tree-like structure that represents the code's abstract syntax. A parser is a software component responsible for performing this conversion.

- **Semantics**: Semantics refers to the meaning and behavior of code. Once we have the abstract syntax, we can evaluate it to understand its semantics. Evaluation involves interpreting the code and determining its effects or outcomes.

In CS 131, we adopt a specific approach to understanding programming languages:

- The programmer writes code as a sequence of characters or strings.
- We use Haskell data types to represent the abstract syntax, which takes the form of a tree structure.
- We implement an evaluation function in Haskell to determine the semantics of the code.

Our current focus is on abstract syntax and semantics, and we haven't yet explored parsing. Parsing will be covered in detail in the future. For now, let's continue delving into abstract syntax and semantics to gain a comprehensive understanding of programming languages.

## Representing Abstract Syntax in Haskell

To represent the abstract syntax of programming languages in Haskell, we utilize data types. Let's consider an example of representing the abstract syntax for simple arithmetic expressions, which we'll refer to as "Arith."

We start by defining two data types: `Op` and `Exp`.

```haskell
data Op
  = PlusOp
  | MinusOp
  | TimesOp
  | DivOp
  deriving (Show)
```

The `Op` data type represents arithmetic operators, including addition (`PlusOp`), subtraction (`MinusOp`), multiplication (`TimesOp`), and division (`DivOp`). These operators serve as the building blocks for arithmetic expressions.

Next, we define the `Exp` data type:

```haskell
data Exp
  = Num Double
  | BinOp Exp Op Exp
  deriving (Show)
```

The `Exp` data type encompasses the different types of expressions within the arithmetic language. It has two constructors: `Num` and `BinOp`.

- The `Num` constructor represents a numerical value and takes a `Double` parameter. For example, `Num 5.0` represents the number 5.0.
- The `BinOp` constructor represents a binary operation and takes three parameters: an expression (`Exp`), an operator (`Op`), and another expression. It signifies that two expressions are combined using a specific operator. For instance, `BinOp (Num 3.0) PlusOp (Num 2.0)` represents the expression "3.0 + 2.0".

By defining these data types, we create a structured representation of arithmetic expressions in Haskell. The `Op` data type captures the available operators, while the `Exp` data type encompasses the expressions themselves, including numbers and binary operations.


## Evaluation of Expressions

To evaluate expressions, we define an `eval` function that operates on the abstract syntax representation. The `eval` function employs recursion and pattern matching to handle different cases based on the structure of the expression. Here's the detailed implementation:

```haskell
eval :: Exp -> Double
eval (Num x) = x
eval (BinOp left PlusOp right) = eval left + eval right
eval (BinOp left MinusOp right) = eval left - eval right
eval (BinOp left TimesOp right) = eval left * eval right
eval (BinOp left DivOp right) = eval left / eval right
```

The `eval` function recursively evaluates expressions by breaking them down into subexpressions and applying the appropriate operations. For example, when encountering a number (`Num`), the associated value is simply returned. For binary operations (`BinOp`), the evaluation is performed recursively on the left and right subexpressions, with the operator applied to the results.


### Evaluating Expressions with Variables

To extend the evaluation of expressions to include variables, we introduce the concept of a symbol dictionary. The symbol dictionary associates symbols (variables) with their corresponding values or expressions. Here's the detailed implementation:

```haskell
type SymbolDictionary = [(Exp, Exp)]

symbolLookup :: Exp -> SymbolDictionary -> Exp
symbolLookup symb [] = undefined
symbolLookup symb ((key, val) : rest) =
  if symb == key
  then val
  else symbolLookup symb rest
```

The `SymbolDictionary` type is a list of pairs, where each pair consists of a symbol (represented as an expression) and its associated value or expression. The `symbolLookup` function retrieves the expression associated with a symbol from the symbol dictionary.

With the symbol dictionary and the `symbolLookup` function, we can evaluate expressions with variables by replacing variable symbols with their corresponding expressions or values during the evaluation process.

## What We Can Do With Functions

Before delving into the representation of functions in Haskell, let's take a moment to revisit the fundamental capabilities of functions. Understanding what we can do with functions will provide a solid foundation for our exploration.

### Defining Functions

The first important aspect of functions is their ability to be defined. When defining a function, we specify its input parameters and describe the computation it should perform. This computation is encapsulated within the function's body. For the sake of simplicity, let's assume that all functions in Haskell have a single parameter.

### Applying Functions

The second crucial aspect of functions is their application. We can apply a function to an argument, effectively invoking the function and obtaining a result. In Haskell, function application is straightforward. By writing the function name followed by the argument, we can apply the function. It's worth noting that the argument can be a simple value or a more complex expression.

Now, let's examine an example to solidify our understanding. Suppose we have a function called `addFive` defined elsewhere. To apply this function to an argument, say the number 5, we would write `addFive 5`. This function application computes the result of adding 5 to the argument.

## Representing Functions in Haskell

With our understanding of what we can do with functions, let's explore how to represent them in Haskell. We will extend the existing `Exp` data type we discussed earlier, introducing additional constructors to handle functions.

```haskell
data Exp
  = Num Double
  | BinOp Exp Op Exp
  | Var String
  | FunDef String Exp
  | Apply Exp Exp
  deriving (Show)
```

To represent functions, we introduce three new constructors to the `Exp` data type:

- `Var`: This constructor represents variables and takes a `String` parameter. In our function definitions, we will use strings to represent variables.
- `FunDef`: This constructor represents function definitions. It takes two parameters: a variable name (the function's parameter) and an expression representing the body of the function.
- `Apply`: This constructor represents function application. It takes two expressions as parameters: the function expression and the argument expression.

Let's consider an example function definition and its application to understand how these new constructors work:

```haskell
FunDef "x" (BinOp (Var "x") PlusOp (Num 1.0))
Apply (FunDef "x" (BinOp (Var "x") PlusOp (Num 1.0))) (Num 5.0)
```

In this example, we define an anonymous function that takes a parameter `x` and adds 1 to it. We then apply this function to the argument 5. The semantics of this expression can be roughly stated as "apply the plus one function to the argument 5."

As we proceed, we will delve deeper into the concept of applying functions in the next section to gain a more comprehensive understanding.

## Applying Functions

Let's explore the concept of applying a function using the following example:

```haskell
Apply (FuncDef "x" (BinOp (Var "x") PlusOp (Num 1))) (Num 5)
```

1. In this example, we have a function definition represented by `FuncDef "x" (BinOp (Var "x") PlusOp (Num 1))`. The function takes a parameter `x` and performs the operation of adding one to it.

2. To apply this function, we use the `Apply` constructor, followed by the function definition and the argument enclosed in parentheses: `Apply (FuncDef "x" (BinOp (Var "x") PlusOp (Num 1))) (Num 5)`.

3. The argument we are applying the function to is `(Num 5)`, representing the number five.

4. When we apply the function, the following steps occur:
   - We locate the variable `x` within the body of the function.
   - We substitute the parameter `x` with the argument `(Num 5)`.
   - The resulting expression becomes `BinOp (Num 5) PlusOp (Num 1)`.

5. At this point, we have simplified the expression by replacing the parameter with the argument.

6. To obtain the final result, we evaluate the simplified expression. In this case, the expression `BinOp (Num 5) PlusOp (Num 1)` evaluates to the value `(Num 6)`.

By applying the function, we effectively substitute the parameter in the function's body with the corresponding argument and evaluate the resulting expression. This process allows us to compute and obtain the desired result based on the given function definition and argument.

## Substitution: Syntax and Examples

To perform expression substitution, we substitute one expression for a variable within another expression. This process can be represented using a specific syntax:

```
e[x → e']
```

Here, `e` represents the original expression, `x` is the variable to be substituted, and `e'` is the expression replacing `x`. The arrow (`→`) denotes the substitution operation.

Let's explore some examples to further illustrate expression substitution:

1. Substituting in `(x + 1)[x → 5]`:
   - We replace `x` with `5` in the expression `(x + 1)`.
   - Applying the substitution, we get `5 + 1`, which evaluates to `6`.

2. Substituting in `(z * z + 7)[z → 2]`:
   - We substitute `2` for `z` in the expression `(z * z + 7)`.
   - After the substitution, we have `2 * 2 + 7`, which simplifies to `4 + 7`, resulting in `11`.

3. Substituting in `(x + y + z)[y → (x / 3)]`:
   - Here, we substitute `(x / 3)` for `y` in the expression `(x + y + z)`.
   - After substitution, the expression becomes `x + (x / 3) + z`.

It's important to note that during substitution, no evaluation occurs. We focus solely on replacing symbols within the expressions. The resulting expressions are not simplified or evaluated at this stage.

Expression substitution plays a fundamental role in understanding the behavior of programming languages and how variables are replaced within expressions. It enables us to manipulate and transform expressions to create new computations based on specific substitutions.

## Substitution: Implementation

We will now delve into the implementation details of expression substitution. We will explore the Haskell code for the `substitute` function, which enables us to replace variables within expressions.

### Syntax of Expression Substitution

The syntax for expression substitution is represented as:

```
e[x → e']
```

Here, `e` denotes the original expression, `x` is the variable to be substituted, and `e'` represents the expression replacing `x`. The arrow (`→`) signifies the substitution operation.

### Implementing the `substitute` Function

To implement expression substitution, we define a function `substitute` in Haskell. This function takes three arguments: the expression to be substituted (`exp'`), the variable to be replaced (`var`), and the original expression (`exp`). The implementation of the `substitute` function is as follows:

```haskell
substitute :: Exp -> Exp -> Exp -> Exp
substitute _ (Var v) (Num x) = Num x
substitute exp' (Var v) (Var w) =
  if v == w then exp' else (Var w)
substitute exp' var (BinOp left op right) =
  BinOp (substitute exp' var left) op (substitute exp' var right)
substitute exp' var (FuncDef varname body) =
  FuncDef varname (substitute exp' var body)
substitute _ _ _ = error "Invalid substitution"
```

Let's explore the implementation in detail:

- If we are substituting the expression `exp'` for the variable `var` in a number expression (`Num x`), the function returns the number `x`.
- When the original expression is a variable (`Var w`), we compare the variable `var` with `w`. If they match, the substitution is performed, and `exp'` is returned. Otherwise, the original variable `Var w` is returned.
- In the case of a binary operation (`BinOp left op right`), we recursively apply the substitution to both the left and right sides of the expression using the `substitute` function. Then, we reconstruct the expression using the `BinOp` constructor.
- If the original expression is a function definition (`FuncDef varname body`), we apply the substitution to the body of the function using the `substitute` function.
- If none of the above cases match, an error is thrown, indicating an invalid substitution.

### Examples of Expression Substitution

Let's explore some examples to gain a better understanding of expression substitution:

1. Substituting `10` for the variable `X` in the expression `Var X`:
   - The substitution results in `Num 10`, as the variable `X` is replaced with the number `10`.

2. Substituting `10 + 5` for the variable `X` in the expression `BinOp (Var X) TimesOp (Var X)`:
   - The substitution yields `BinOp (Num 10 + 5) TimesOp (Num 10 + 5)`. Here, the variable `X` is replaced with the expression `10 + 5` in the original expression.

These examples showcase how expression substitution operates by replacing variables with corresponding expressions.

## Evaluating Function Application

### Applying a Function

Applying a function involves substituting the function's argument into the function's body and evaluating the result. Let's consider an example to understand this process better:

```haskell
Apply (FuncDef "x" (BinOp (Var "x") PlusOp (Num 1))) (Num 5)
```

Here, we apply the "plus one" function to the argument `5`. The semantics of applying a function entail substituting `5` for the parameter `x` in the function's body.

### Evaluating Function Application

To evaluate function application, we need to define how functions and their arguments are evaluated. In Haskell, we can implement the evaluation process using the `eval` function. The implementation of `eval` considers various cases based on the type of expression being evaluated.

### Evaluation of Expressions

Let's first define the basic evaluation of expressions using the `eval` function:

```haskell
eval :: Exp -> Exp
eval (Num x) = Num x
eval (BinOp left op right) = evalOp (eval left) op (eval right)
```

- For a number expression (`Num x`), the evaluation simply returns the number itself.
- In the case of a binary operation (`BinOp left op right`), we recursively evaluate the left and right subexpressions and apply the operation (`op`) to obtain the result.

### Evaluation of Function Definitions

To incorporate function definitions into the evaluation process, we extend the `eval` function as follows:

```haskell
eval (FuncDef varname body) = (FuncDef varname body)
```

- When encountering a function definition (`FuncDef varname body`), we return the function definition itself. Functions are treated as values and can be passed as arguments or stored in variables.

### Evaluation of Function Application

Now, let's focus on the evaluation of function application. We consider two approaches to handle function application in Haskell.

#### Call-by-Name Evaluation

In call-by-name evaluation, the argument is substituted unevaluated into the function body. This approach is implemented as follows:

```haskell
eval (Apply (FuncDef varname body) arg) =
    eval (substitute arg (Var varname) body)
```

- Here, the argument (`arg`) is substituted for the parameter (`Var varname`) in the body of the function. The resulting expression is then evaluated.

#### Call-by-Value Evaluation

In call-by-value evaluation, the argument is evaluated before substituting it into the function body. This approach is implemented as follows:

```haskell
eval (Apply (FuncDef varname body) arg) =
    let val = eval arg in
        eval (substitute val (Var varname) body)
```

- The argument (`arg`) is first evaluated, and the resulting value (`val`) is substituted for the parameter (`Var varname`) in the body of the function. Finally, the substituted expression is evaluated.

### Handling Functions with Multiple Arguments

So far, our examples have only involved functions with a single argument. However, what if we need functions with multiple arguments? Let's consider an example:

```haskell
FuncDef "x" (FuncDef "y" (BinOp (Var "x") PlusOp (Var "y")))
```

To handle functions with multiple arguments, we introduce nested function definitions. The innermost function takes the second argument, and the outer function takes the first argument. This allows us to achieve function currying and evaluate function applications with multiple arguments sequentially.

