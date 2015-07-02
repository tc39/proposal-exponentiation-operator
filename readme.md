# Exponentiation Operator

## Status

- Currently at **Stage 2**, with implementation agreement from SpiderMonkey and V8.
- Implemented in Traceur 


## Notes

- The _Exponentiation Operator_ should come before _Multiplicative Operators_ in clause 12, which means _Multiplicative Operators_ move from 12.6 to 12.7.
- Adds %Math.pow% to Well-Known Intrinsics Table


#### 12.6 Exponentiation Operator

  **Syntax**
  
  _ExponentiationExpression_ : 
    _UnaryExpression_[?Yield]
    _UnaryExpression_[?Yield] `**` _ExponentiationExpression_[?Yield]

##### 12.6.1 Static Semantics: IsFunctionDefinition

  _ExponentiationExpression_ : _UnaryExpression_  `**` _ExponentiationExpression_
  
  1. Return **false**.

##### 12.6.2 Static Semantics: IsValidSimpleAssignmentTarget

  _ExponentiationExpression_ : _UnaryExpression_  `**` _ExponentiationExpression_
  
  1. Return **false**.

##### 12.6.3 Runtime Semantics: Evaluation

  _ExponentiationExpression_ : _UnaryExpression_  `**` _ExponentiationExpression_

  1. Let _left_ be the result of evaluating _UnaryExpression_.
  1. Let _lValue_ be GetValue(_left_).
  1. ReturnIfAbrupt(_lValue_).
  1. Let _right_ be the result of evaluating _ExponentiationExpression_.
  1. Let _rValue_ be GetValue(_right_).
  1. Let _base_ be ToNumber(_lValue_).
  1. ReturnIfAbrupt(_base_).
  1. Let _exponent_ be ToNumber(_rValue_).
  1. ReturnIfAbrupt(_exponent_).
  1. Return %Math.pow%(_base_, _exponent_).


(Move _Multiplicative Operators_ to 12.7)



#### Grammar Additions

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



## Informative

- Commonly used in albegra, geometry, physics and robotics.
- Nice to have "inline" operator

#### Prior Art

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


#### Usage


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


#### Grammar Delta

```diff
+ ExponentiationExpression : 
+   UnaryExpression[?Yield]
+   UnaryExpression[?Yield] ** ExponentiationExpression[?Yield]

MultiplicativeExpression[Yield] :
-   UnaryExpression[?Yield]
+   ExponentiationExpression[?Yield]
-   MultiplicativeExpression[?Yield] MultiplicativeOperator UnaryExpression[?Yield]
+   MultiplicativeExpression[?Yield] MultiplicativeOperator ExponentiationExpression[?Yield]


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

Implementation Progress
  - Traceur
  - Babel
  - V8 (https://code.google.com/p/v8/issues/detail?id=3915)
  - SpiderMonkey (https://bugzilla.mozilla.org/show_bug.cgi?id=1135708)




## Reviewers

- Erik Arvidsson
- Dmitry Lomov
- Cait Potter
- Jason Orendorff
