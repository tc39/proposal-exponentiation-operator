# Exponentiation Operator

## Stage 0

Performs exponential calculation on operands. Same algorithm as `%MathPow%(x, y)`

- Commonly used in albegra, geometry, physics and robotics.
- Nice to have "inline" operator

## Prior Art

- Python
  - `math.pow(x, y)`
  - `x ** y`
- CoffeeScript
  - `x ** y`
- F#
  - `x ** y`
- Ruby
  - `x ** y`
- Perl
  - `x ** y`
- Lua, Basic, MATLAB, etc.
  - `x ^ y`


## Usage


```js
// x ** y

let squared = 2 ** 2;
// same as: 2 * 2

let cubed = 2 ** 3;
// same as: 2 * 2 * 2

```

```js
// x **= y

let a = 2;
a **= 2;
// same as: a = a * a;



let b = 3;
b **= 3;
// same as: b = b * b * b;

```

## Grammar

```
ExponentiationExpression : 
  UnaryExpression[?Yield]
  UnaryExpression[?Yield] ** ExponentiationExpression[?Yield]

MultiplicativeExpression[Yield] :
  ExponentiationExpression[?Yield]
  MultiplicativeExpression[?Yield] MultiplicativeOperator ExponentiationExpression[?Yield]

MultiplicativeOperator : one of
  * / %
  
AssignmentOperator : one of
  =
  *=
  /=
  %=
  +=
  -=
  <<=
  >>=
  >>>=
  &=
  ^=
  |=
  **=
```

## Grammar Delta

```diff
+ ExponentiationExpression : 
+   UnaryExpression[?Yield]
+   UnaryExpression[?Yield] ** ExponentiationExpression[?Yield]

MultiplicativeExpression[Yield] :
-   UnaryExpression[?Yield]
+   ExponentiationExpression[?Yield]
  MultiplicativeExpression[?Yield] MultiplicativeOperator UnaryExpression[?Yield]

MultiplicativeOperator : one of
  * / %

AssignmentOperator : one of
  =
  *=
  /=
  %=
  +=
  -=
  <<=
  >>=
  >>>=
  &=
  ^=
  |=
+   **=
```

## Status

Implemented as option in Traceur 

https://github.com/google/traceur-compiler/pull/1216


## Reviewed By: 

- Erik Arvidsson
- Dmitry Lomov

