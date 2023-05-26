# CS131: Programming Languages

## Recap: Syntax, semantics, evaluation of simple expressions

In this lecture, we will provide a detailed recap of the important concepts related to syntax, semantics, and evaluation of simple expressions. We will also explore the representation of abstract syntax and the evaluation of expressions involving variables and functions.

## Syntax and Semantics

Syntax refers to the rules and structure of a programming language that define what constitutes a valid expression or statement. It is essentially the way programmers write code using a sequence of characters or strings. In Haskell, syntax is expressed using concrete syntax, which includes elements such as function calls, operators, and values.

Semantics, on the other hand, deals with the meaning or interpretation of expressions. It defines how expressions are evaluated and the results they produce. In Haskell, semantics is expressed using abstract syntax, which represents expressions as a tree-like data structure.

## Representing Abstract Syntax

To represent abstract syntax in Haskell, we utilize data types. Let's consider an example of representing the abstract syntax for simple arithmetic expressions, which we'll refer to as "Arith":

```haskell
data Op
  = PlusOp
  | MinusOp
  | TimesOp
  | DivOp
  deriving (Show)

data Exp
  = Num  Double
  | BinOp Exp Op Exp
  deriving (Show)
```

The `Op` data type represents arithmetic operators such as addition, subtraction, multiplication, and division. The `Exp` data type represents expressions, including numbers (`Num`) and binary operations (`BinOp`).

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

## Evaluating Expressions with Variables

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

## Evaluating Expressions with Functions

To represent functions in the abstract syntax, we extend the `Exp` data type. Here's the updated definition:

```haskell
data Exp
  = Var VarName
  | Num Double


  | BinOp Exp Op Exp
  | FuncDef VarName Exp
  | Apply Exp Exp
  deriving (Show)
```

The `FuncDef` constructor represents function definitions, where the first parameter is the function's name and the second parameter is the function's body. The `Apply` constructor represents function application, where the first expression is the function to be applied, and the second expression is the argument to the function.

To evaluate function application, we modify the `eval` function as follows:

```haskell
eval :: Exp -> SymbolDictionary -> Exp
eval (Num x) _ = Num x
eval (Var x) dict = symbolLookup (Var x) dict
eval (BinOp left op right) dict =
  let evalLeft = eval left dict
      evalRight = eval right dict
  in evalOp evalLeft op evalRight
eval (FuncDef varname body) _ = FuncDef varname body
eval (Apply func arg) dict =
  let evaluatedFunc = eval func dict
      evaluatedArg = eval arg dict
  in case evaluatedFunc of
       FuncDef param body ->
         let substitutedBody = substitute evaluatedArg (Var param) body
         in eval substitutedBody dict
       _ -> error "Invalid function application"
```

The modified `eval` function handles function application by checking if the evaluated function is a `FuncDef`. If it is, it substitutes the evaluated argument for the function's parameter in the body and evaluates the resulting expression.

## Expression Substitution

To perform expression substitution, we define a `substitute` function:

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

The `substitute` function takes an expression to substitute (`exp'`), a variable to be replaced (`Var v`), and an expression in which the substitution is performed. It recursively traverses the expression and replaces occurrences of the variable with the substitution expression.

By combining syntax, semantics, and evaluation, we can work with expressions, variables, and functions in a structured and systematic manner, gaining a deeper understanding of programming language concepts and their implementation.
