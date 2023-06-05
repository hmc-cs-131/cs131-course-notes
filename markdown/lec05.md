### CS 131: Programming Languages

# Haskell Data Types, Pattern Matching, Type Classes

## Warm-up Problem: Working with Shapes
In this lecture, we will explore the foundations of Haskell data types, pattern matching, and type classes. As a warm-up problem, let's consider working with shapes such as circles, squares, and right triangles.

We want to represent shapes and perform various operations on them, including computing areas and shifting their positions.

### Question 1: Object-Oriented Approach
How would you approach this problem using an object-oriented programming language like Java, C++, or Python? Consider how you would represent the shapes, implement methods for shifting and computing areas, and outline your solution.

### Question 2: How Was Your Weekend?

## Warm-up Problem Solution
### Object-Oriented Approach
Let's consider an object-oriented solution using Java for representing and operating on shapes.

```java
abstract class Shape {
  double x, y;
  
  public abstract double area();
  
  public void shift(double deltaX, double deltaY) {
    x += deltaX;
    y += deltaY;
  }
}

class Circle extends Shape {
  double radius;
  
  public double area() {
    return Math.PI * radius * radius;
  }
}

class Square extends Shape {
  double side;
  
  public double area() {
    return side * side;
  }
}

class RightTriangle extends Shape {
  double base, height;
  
  public double area() {
    return base * height / 2;
  }
}
```

### Haskell Solution using Data Types and Pattern Matching
In Haskell, we can represent shapes and perform operations on them using data types and pattern matching.

```haskell
data Shape
  = Circle Double Double Double
  | Square Double Double Double
  | RightTriangle Double Double Double Double
  deriving Show

area :: Shape -> Double
area shape =
  case shape of
    Circle _ _ radius -> pi * radius * radius
    Square _ _ side -> side * side
    RightTriangle _ _ base height -> base * height / 2

shift :: Shape -> Double -> Double -> Shape
shift shape deltaX deltaY =
  case shape of
    Circle x y radius -> Circle (x + deltaX) (y + deltaY) radius
    Square x y side -> Square (x + deltaX) (y + deltaY) side
    RightTriangle x y base height -> RightTriangle (x + deltaX) (y + deltaY) base height
```

### Functional Programming vs. Object-Oriented Programming
In object-oriented programming, shapes are objects that know how to perform different operations on themselves. In functional programming, functions know how to compute over different data types. The shift function in Haskell knows how to compute a shifted shape (circle, square, or right triangle), while the area function knows how to compute the area for each shape.

Functional programming takes a different approach by separating data from behavior and treating functions as first-class citizens.

## Recursive Data Types
We can define recursive data types in Haskell. Let's consider a simple example of creating lists.

```haskell
data IntList
  = Empty
  | Cons Int IntList
  deriving Show
```

Here, an `IntList` is either an `Empty` list or a `Cons` cell containing an integer and another `IntList`.

### Recursive Data Types: Operations on IntList
We can define various operations on `IntList` using pattern matching.

```haskell
intListLength :: IntList -> Int
intListLength Empty = 0
intListLength (Cons _ xs) = 1 + intListLength xs

intListHead :: IntList -> Int
intListHead Empty = undefined
intListHead (Cons x _)

 = x

intListTail :: IntList -> IntList
intListTail Empty = undefined
intListTail (Cons _ xs) = xs

intListMap :: (Int -> Int) -> IntList -> IntList
intListMap _ Empty = Empty
intListMap f (Cons x xs) = Cons (f x) (intListMap f xs)
```

### Recursive Data Types: Example
Let's create some examples of `IntList`:

```haskell
list1 = Empty
list2 = Cons 6 Empty
list3 = Cons 10 (Cons 20 list2)
list4 = Cons (-4) list3
list5 = Cons 100 (Cons 13 list4)
list6 = Cons 100 (Cons 13 list5)
```

### Recursive Data Types: List Operations
We can define operations on lists, such as finding the length or sum.

```haskell
intListLength :: IntList -> Int
intListLength Empty = 0
intListLength (Cons _ xs) = 1 + intListLength xs

intListSum :: IntList -> Int
intListSum Empty = 0
intListSum (Cons x xs) = x + intListSum xs
```

## Combining Data Types
We can combine multiple data types to create more complex structures. Let's combine the `CardSuit` and `FaceValues` types to represent a deck of cards.

```haskell
data CardSuit = Clubs | Diamonds | Hearts | Spades
  deriving (Show, Eq, Ord)

data FaceValues
  = Two | Three | Four | Five | Six | Seven | Eight
  | Nine | Ten | Jack | Queen | King | Ace
  deriving (Show, Eq, Ord)

type Card = (FaceValues, CardSuit)

data CardList
  = Empty
  | Hand Card CardList
  deriving (Show, Eq, Ord)
```

Now we can create a deck of cards represented by `CardList` and perform operations on it.

## Type Classes
Type classes in Haskell define a set of functions that can operate on certain types. Some common type classes are `Eq`, `Ord`, `Show`, and `Read`.

For example, the `CardSuit` and `FaceValues` types can derive the `Show`, `Eq`, and `Ord` type classes, allowing us to print, compare, and order their values.

```haskell
data CardSuit = Clubs | Diamonds | Hearts | Spades
  deriving (Show, Eq, Ord)

data FaceValues
  = Two | Three | Four | Five | Six | Seven | Eight
  | Nine | Ten | Jack | Queen | King | Ace
  deriving (Show, Eq, Ord)
```

## Summary
In this lecture, we explored the foundations of Haskell data types, pattern matching, and type classes. We discussed representing shapes using data types and performed operations on them. We also covered recursive data types, combining data types, and type classes in Haskell. By understanding these concepts, we can build more complex and powerful programs using Haskell's functional programming paradigm.