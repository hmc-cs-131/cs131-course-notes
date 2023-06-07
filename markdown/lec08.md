### CS 131: Programming Languages

#  Defining and Applying Functions

## Syntax and Semantics

- The syntax of a programming language refers to the sequence of characters or tokens that make up valid programs.
- The semantics of a programming language defines the meaning of programs and how they should be executed.

## Code as Data and Functions as Data

- An important concept in programming languages is that code is data.
- Functions can also be treated as data and manipulated like other values in the language.

### Representing Functions as Data

In order to represent functions as data structures, we can define a suitable abstract syntax. Here is an example of an abstract syntax for representing functions:

```haskell
data Op
    = PlusOp
    | MinusOp
    | TimesOp
    | DivOp
    deriving (Show, Eq)

type VarName = String

data Exp 
    = Var VarName
    | BinOp Exp Op Exp
    | Num Double
    | FuncDef VarName Exp
    | Apply Exp Exp
    deriving (Show, Eq)
```

- The `Op` data type represents different operators like addition, subtraction, multiplication, and division.
- The `VarName` type is a synonym for strings, representing variable names.
- The `Exp` data type represents expressions and includes variables, binary operations, numbers, function definitions, and function applications.

## Evaluating Expressions

To evaluate expressions, we define an `eval` function in Haskell. Here is the implementation:

```haskell
evalOp :: Exp -> Op -> Exp -> Exp
evalOp (Num x) PlusOp  (Num y) = Num(x + y)
evalOp (Num x) TimesOp (Num y) = Num(x * y)
evalOp (Num x) DivOp   (Num y) = Num(x / y)
evalOp (Num x) MinusOp (Num y) = Num(x - y)

eval :: Exp -> Exp
eval (Num x) = Num x
eval (BinOp left op right) = evalOp (eval left) op (eval right)
eval (FuncDef varname body) = FuncDef varname body
eval (Apply fexp exp) = 
    let (FuncDef varname body) = eval fexp in
        eval (substitute exp (Var varname) body)
```

- The `eval` function takes an expression and evaluates it to obtain the result.
- The `evalOp` function evaluates binary operations.
- The `eval` function pattern matches on different expression forms and recursively evaluates subexpressions.
- When encountering a function application, it substitutes the argument for the parameter in the body of the function.

## Let Expressions

### What does it mean to 'apply a function'?

Applying a function involves providing an argument to the function and obtaining the result. For example:

```haskell
Apply (FuncDef "x" (BinOp (Var "x") PlusOp (Num 1))) (Num 5)
```

- This applies the 'plus one' function to the argument `5`.
- The semantics of function application involve substituting the argument for the parameter in the body of the function.

### Let Bindings

A let expression in Haskell has the following form:

```haskell
let x = 100 in x + 17
```

- It consists of a variable (`x`), a value (`100`), and a body (`x + 17`).
- The value of the let expression is obtained by substituting the value for the variable in the let body.

### Adding Let Expressions to Abstract Syntax

To add let expressions to our abstract syntax, we can introduce a new constructor in

 the `Exp` data type. Here is the updated definition:

```haskell
data Exp 
    = Var VarName
    | BinOp Exp Op Exp
    | Num Double
    | Let VarName Exp Exp
    | FuncDef VarName Exp
    | Apply Exp Exp
    deriving (Show, Eq)
```

- The new `Let` constructor represents let expressions and takes a variable, an expression for the value, and a body expression.

### Using FuncDef for Let Expressions

We can express let expressions using our existing `FuncDef` constructor. Here is an example:

```haskell
Let "x" (Num 100) (BinOp (Var "x") PlusOp (Num 17))
```

- This let expression binds the value `100` to the variable `x`.
- The body of the let expression is `x + 17`.
- We can think of it as a function `f(x) = x + 17` and call `f` with the argument `100`.

### Evaluating Let Expressions

To evaluate let expressions, we need to substitute the value for the variable in the let body. Here is the updated `eval` function:

```haskell
eval (Let varname exp letBody) =  
    eval (Apply (FuncDef varname letBody) exp)
```

- The `eval` function pattern matches on the `Let` constructor.
- It constructs a function definition using the variable name and let body.
- Then it applies the function to the expression representing the value.

## Is Substitution Really the Way?

Instead of using substitution for evaluating function applications and let expressions, we can create new abstract syntax and express their semantics using existing semantics.

## Function Definition and Application

Here are examples of function definition and application using our abstract syntax:

```haskell
-- Identity function
(FuncDef "a" (Var "a"))

-- Apply the identity function
Apply (FuncDef "a" (Var "a")) (Num 1)

-- Use the eval function
eval (Apply (FuncDef "a" (Var "a")) (Num 1))   -- Result: (Num 1)
```

- The first example defines the identity function, which returns its argument.
- The second example applies the identity function to the number `1`.
- The third example uses the `eval` function to evaluate the expression and obtain the result.

### Functions with Multiple Variables

Functions with multiple variables can be represented using currying. Here is an example:

```haskell
-- Functions with multiple variables via currying
FuncDef "b" (FuncDef "a" (BinOp (Var "a") PlusOp (Var "b")))

-- Apply function to one argument and eval
eval (Apply (FuncDef "b" (FuncDef "a" (BinOp (Var "a") PlusOp (Var "b")))) (Num 1))
```

- The first example defines a function that takes two arguments `a` and `b` and returns their sum.
- The second example applies the function to one argument (`1`) and evaluates it.

### Adding More Arguments

We can continue adding more arguments to our functions. Here is an example:

```haskell
-- Functions with multiple variables via currying
FuncDef "a" (FuncDef "b" (FuncDef "c" (FuncDef "d" 
    (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (BinOp (Var "c") PlusOp (Var "d")))))))

-- Use our eval function
Apply (Apply (Apply (Apply 
    (FuncDef "a" (FuncDef "

b" (FuncDef "c" (FuncDef "d" 
    (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (BinOp (Var "c") PlusOp (Var "d")))))))) 
    (Num 1)) (Num 2)) (Num 3)) (Num 4)
```

- The first example defines a function with four variables `a`, `b`, `c`, and `d`.
- The function performs a series of addition operations.
- The second example demonstrates applying the function to four arguments and evaluating it.

As we add more arguments, the function expressions grow in size, resulting in more computational work. The complexity increases from O(N) to O(N^2), where N is the number of parameters.

## An Alternative to Substitution

#### Adding more arguments
We can use our `eval` function to handle additional arguments. Consider the following example:

```haskell
Apply (Apply (Apply (Apply 
    (FuncDef "a" (FuncDef "b" (FuncDef "c" (FuncDef "d" 
    (BinOp (Var "a") PlusOp 
    (BinOp (Var "b") PlusOp 
    (BinOp (Var "c") PlusOp (Var "d")))))))) 
    (Num 1)) (Num 2)) (Num 3)) (Num 4)
```

#### N parameters and function expressions of size O(N) → O(N^2) work!
When we add N parameters to a function and have function expressions of size O(N), the evaluation work increases to O(N^2).

#### Recall: Expressions with Variables
Let's review the data types for expressions with variables that we covered last week:

```haskell
data Op
   = PlusOp
   | MinusOp
   | TimesOp
   | DivOp
   deriving (Show)

data Exp
   = Var String 
   | Num  Double
   | BinOp Exp Op Exp
   deriving (Show)
```

#### VarDictionary and Evaluation

We introduce the `VarDictionary` type alias, which is a list of pairs representing the mapping of variables to values.

```haskell
type VarDictionary = [(Exp, Exp)]
```

We can perform variable lookup in the `VarDictionary` using the `varLookup` function:

```haskell
varLookup :: Exp -> VarDictionary -> Exp
varLookup symb [] = undefined
varLookup symb ((key, val) : rest) = 
    if symb == key then val else varLookup symb rest
```

The `eval` function evaluates expressions using the `VarDictionary`. Here's the implementation:

```haskell
eval :: Exp -> VarDictionary -> Double
eval (Num x) dict = x

eval (Var x) dict = 
    let expr = varLookup (Var x) dict
    in eval expr dict

eval (BinOp left PlusOp right) dict =  (eval left dict) + (eval right dict)
eval (BinOp left MinusOp right) dict =  (eval left dict) - (eval right dict)
eval (BinOp left TimesOp right) dict =  (eval left dict) * (eval right dict)
eval (BinOp left DivOp right) dict =  (eval left dict) / (eval right dict)
```

## A great idea: save the environment!

Instead of performing substitution every time, we can "remember" the substitutions and apply them when we need the values of the local parameters.

Consider the following expression:

```haskell
Apply (Apply (Apply (Apply 
    (FuncDef "a" (FuncDef "b" (FuncDef "c" (FuncDef "d" 
    (BinOp (Var "a") PlusOp 
    (BinOp (Var "b") PlusOp 
    (BinOp (Var "c") PlusOp (Var "d")))))))) 
    (Num 1)) (Num 2)) (Num 3)) (Num 4)
```

By saving the environment, we can avoid performing substitution at each step. Here's the modified expression:

```haskell
Apply (Apply (Apply 
   (FuncDef "b" (FuncDef "c" (FuncDef "d" 
   (BinOp (Var "a") PlusOp 
   (BinOp (Var "b") Plus
   (BinOp (Var "c") PlusOp (Var "d")))))) 
   (Num 1)) (Num 2)) (Num 3)
```

We can modify the expression by saving the environment and avoiding substitution at each step. Here's the modified expression:

```haskell
let env1 = [("a", Num 1)]
in Apply (Apply (Apply 
   (FuncDef "b" (FuncDef "c" (FuncDef "d" 
   (BinOp (Var "a") PlusOp 
   (BinOp (Var "b") PlusOp (Var "c")))))) 
   (Num 2)) (Num 3)) env1
```

In this modified expression, we create an environment `env1` that maps the variable "a" to the value `Num 1`. We then use this environment while evaluating the expression.

### Modifying the `eval` Function

To support saving the environment, we need to modify the `eval` function to take an additional parameter for the variable dictionary. Here's the updated implementation:

```haskell
eval :: Exp -> VarDictionary -> Double
eval (Num x) _ = x

eval (Var x) dict = 
    let expr = varLookup (Var x) dict
    in eval expr dict

eval (BinOp left PlusOp right) dict =  (eval left dict) + (eval right dict)
eval (BinOp left MinusOp right) dict =  (eval left dict) - (eval right dict)
eval (BinOp left TimesOp right) dict =  (eval left dict) * (eval right dict)
eval (BinOp left DivOp right) dict =  (eval left dict) / (eval right dict)

eval (FuncDef var body) dict = eval body ((Var var, body) : dict)

eval (Apply func arg) dict = 
    let funcVal = eval func dict
        argVal = eval arg dict
    in case funcVal of
        FuncDef var body -> eval body ((Var var, arg) : dict)
        _ -> error "Invalid application: non-function value"
```

### Example Evaluation with Saved Environment

Let's evaluate the modified expression using the updated `eval` function and the saved environment `env1`:

```haskell
eval (Apply (Apply (Apply 
   (FuncDef "b" (FuncDef "c" (FuncDef "d" 
   (BinOp (Var "a") PlusOp 
   (BinOp (Var "b") PlusOp (Var "c")))))) 
   (Num 2)) (Num 3)) env1
```

Here's how the evaluation proceeds:

1. Evaluate `Apply (FuncDef "b" (FuncDef "c" (FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))))) (Num 2)`:

   - Evaluate `FuncDef "b" (FuncDef "c" (FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c"))))))` with the current environment `env1`. This results in a function value.

   - Evaluate `(Num 2)` with the current environment `env1`. This results in the value `2`.

   - Apply the function value to the argument value. The function value is `FuncDef "b" (FuncDef "c" (FuncDef "d" (BinOp (Var "a

") PlusOp (BinOp (Var "b") PlusOp (Var "c"))))))`, and the argument value is `2`.

   - Create a new environment by extending `env1` with the binding `("b", Num 2)`.

2. Evaluate `Apply (FuncDef "c" (FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))))) (Num 3)`:

   - Evaluate `FuncDef "c" (FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c"))))))` with the current environment extended with `("b", Num 2)`. This results in a function value.

   - Evaluate `(Num 3)` with the current environment extended with `("b", Num 2)`. This results in the value `3`.

   - Apply the function value to the argument value. The function value is `FuncDef "c" (FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c"))))))`, and the argument value is `3`.

   - Create a new environment by extending the current environment with the binding `("c", Num 3)`.

3. Evaluate `FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))))` with the current environment extended with `("c", Num 3)`:

   - Evaluate `BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))` with the current environment extended with `("c", Num 3)`.

   - Evaluate `Var "a"` with the current environment extended with `("c", Num 3)`. This results in the value `Num 1`.

   - Evaluate `Var "b"` with the current environment extended with `("c", Num 3)` and `("a", Num 1)`. This results in the value `Num 2`.

   - Evaluate `Var "c"` with the current environment extended with `("c", Num 3)`, `("b", Num 2)`, and `("a", Num 1)`. This results in the value `Num 3`.

   - Apply the plus operator to `Num 1` and `(Num 2) + (Num 3)`. This results in the value `Num 6`.

   - Create a new environment by extending the current environment with the binding `("d", Num 6)`.

4. Evaluate `(Num 1)` with the current environment extended with `("d", Num 6)`. This results in the value `1`.

5. Apply the function value `FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))))` to the argument value `1`.

   - Create a new environment by extending the current environment with the binding `("d", Num 6)`.

   - Evaluate the body of `FuncDef "d" (BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))))` with the new environment.

   - Evaluate `BinOp (Var "a") PlusOp (BinOp (Var "b") PlusOp (Var "c")))` with the new environment.

   - Evaluate `Var "a"` with the new environment. This results in the value `Num 1`.

   - Evaluate `Var "

b"` with the new environment. This results in the value `Num 2`.

   - Evaluate `Var "c"` with the new environment. This results in the value `Num 3`.

   - Apply the plus operator to `Num 1` and `(Num 2) + (Num 3)`. This results in the value `Num 6`.

The final result of evaluating the expression is `Num 6`.

## Implementing Environments

### An Attempt at Lookup and Insert for Environments

Here is an attempt at implementing lookup and insert operations for environments in Haskell:

```haskell
type VarName = String
type Env = [(VarName, Exp)]

envLookup :: VarName -> Env -> Exp
envLookup v [] = error ("unbound identifier: " ++ v)
envLookup v ((key, val) : rest) = 
    if v == key 
    then val
    else envLookup v rest

envInsert :: VarName -> Exp -> Env -> Env
envInsert v exp [] = [(v, exp)]
envInsert v exp ((key, val) : rest) = 
    if v == key 
    then (v, exp) : rest
    else (key, val) : envInsert v exp rest
```

### Use a HashMap!

Alternatively, instead of using a list-based representation for environments, a better data structure to consider is `HashMap` available in Haskell. It provides more efficient lookup and insertion operations.

### Improving the Environment Representation

```haskell
import qualified Data.Map as Map

type VarName = String
type Env = Map.Map VarName Exp

envLookup :: VarName -> Env -> Exp
envLookup v env = case Map.lookup v env of
    Just val -> val
    Nothing -> error ("unbound identifier: " ++ v)

envInsert :: VarName -> Exp -> Env -> Env
envInsert = Map.insert
```

By using `Data.Map` module and `Map` data structure, we can simplify the implementation of lookup and insert operations for environments, leading to more efficient code.

## Eval Using Environments

The `eval` function allows us to evaluate expressions using environments.

```haskell
eval :: Env -> Exp -> Exp
eval env (Num x) = Num x
eval env (Var v) = envLookup v env
eval env (BinOp left op right) = evalOp (eval env left) op (eval env right)

eval env (FuncDef varname body) = Closure env varname body

eval env (Apply fexp exp) = 
    let (Closure closureEnv varname body) = eval env fexp 
        argval = eval env exp in
            eval (envInsert varname argval closureEnv) body
```

The `eval` function takes an environment (`Env`) and an expression (`Exp`) as arguments and returns the evaluated result (`Exp`). It supports different types of expressions, including numbers (`Num`), variables (`Var`), binary operations (`BinOp`), function definitions (`FuncDef`), and function applications (`Apply`).

The evaluation of a number simply returns the number itself. For a variable, the environment is used to perform a lookup and return the corresponding value. Binary operations are evaluated by recursively evaluating the left and right operands and applying the specified operator.

Function definitions are represented as closures, which store the environment (`env`), the variable name (`varname`), and the body of the function (`body`).

Function applications involve evaluating both the function expression (`fexp`) and the argument expression (`exp`). If the function expression evaluates to a closure, the closure's environment is extended with the argument value using `envInsert`, and the body of the closure is evaluated in the updated environment.

## Scope

### Dynamic Scope vs. Static Scope

There are two kinds of scope that can be used in programming languages: dynamic scope and static scope.

- **Dynamic Scope**: It uses the closest enclosing scope to look up local variables. The value of a variable is determined by the runtime call stack. Changes to the value of a variable in one part of the program can affect its value in other parts of the program that call the same function. Dynamic scope can be more flexible in certain scenarios but can also lead to unpredictable behavior and make code harder to reason about.

- **Static Scope**: It uses the lexical structure of the program to determine the scope of variables. The value of a variable is determined by its declaration in the source code. Variables are bound to their closest enclosing scope at the time of their declaration and remain bound to that scope throughout the execution of the program. Static scope provides more predictability and easier understanding of how variables are scoped.


### More Weirdness: Can we even function?

In the previous section, we explored the evaluation of expressions using the environment-based evaluation model. We encountered an issue when attempting to evaluate the following expression:

```haskell
(Apply (Apply (FuncDef "a" (FuncDef "b" (BinOp (Var "b") PlusOp (Var "a")))) (Num 100)) (Num 42))
```

The evaluation resulted in an error, specifically "unbound identifier: a." This error occurred because the identifier "a" was not found in the environment during the evaluation process.

Let's take a closer look at the `eval` function:

```haskell
eval :: Env -> Exp -> Exp
eval env (Num x) = Num x
eval env (Var v) = envLookup v env
eval env (BinOp left op right) = 
    evalOp (eval env left) op (eval env right)
eval env (Let varname exp letBody) = 
    eval env (Apply (FuncDef varname letBody) exp)
eval env (FuncDef varname body) = (FuncDef varname body)
eval env (Apply fexp exp) = 
    let (FuncDef varname body) = eval env fexp 
        argval = eval env exp in
            eval (envInsert varname argval env) body
```

We can observe that the `eval` function doesn't handle function definitions (`FuncDef`) and function applications (`Apply`) correctly. In the case of `FuncDef`, it simply returns the function definition itself without capturing the environment. Similarly, in the case of `Apply`, it attempts to destructure a `FuncDef` without considering the environment.

## Closures

To fix this issue, we need to introduce the concept of closures. A closure is a combination of a function and the environment in which it was defined. It allows us to capture the environment and associate it with the function, ensuring that variables within the function have access to their correct bindings.

To incorporate closures into our evaluation model, we need to make some modifications. First, we'll update the `Exp` data type to include a `Closure` constructor:

```haskell
data Exp 
    = Var VarName
    | Num Double
	...
    | Let VarName Exp Exp
    | FuncDef VarName Exp
    | Apply Exp Exp
    | Closure Env VarName Exp
    deriving (Show, Eq)
```

Now, let's modify the `eval` function to utilize closures:

```haskell
eval env (FuncDef varname body) = Closure env varname body

eval env (Apply fexp exp) = 
    let (Closure closureEnv varname body) = eval env fexp 
        argval = eval env exp in
            eval (envInsert varname argval closureEnv) body
```

In the case of `FuncDef`, instead of returning the function definition as is, we create a closure by combining the current environment (`env`), the variable name (`varname`), and the body of the function (`body`).

For `Apply`, we first evaluate the function expression (`fexp`) and extract the closure's components: the closure environment (`closureEnv`), the variable name (`varname`), and the body of the function (`body`). We also evaluate the argument expression (`exp`) to obtain its value (`argval`). Then, we perform the evaluation of the function body by inserting the argument value (`argval`) into the closure environment (`closureEnv`) with the variable name (`varname`) as the binding. This ensures that the correct environment is used within the function body.

By introducing closures and updating our evaluation model accordingly,

 we can now properly handle function definitions and function applications, allowing for the correct scoping of variables and access to their bindings.

This concludes our exploration of some of the core foundations of programming languages, including syntax, evaluation models, and scoping. These concepts form the basis for understanding how programming languages work and how code execution and variable scoping are handled. By mastering these foundations, you'll be well-equipped to dive deeper into the world of programming languages and explore more advanced topics.


