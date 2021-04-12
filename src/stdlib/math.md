# Standard Library: Math functions


## abs

```rant

[%abs: num]

```
&rarr; `int | float`

Prints the absolute value of `num`.

### Parameters

**`num`** &larr; `int | float` <br/>
The input number.

### Errors

Raises an error if `num` is an integer and the absolute value overflows.


## add

```rant

[%add: lhs; rhs]

```
&rarr; `any`

Adds two values and prints the sum.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand of the addition.

**`rhs`** &larr; `any` <br/>
The right-hand operand of the addition.


## ceil

```rant

[%ceil: val]

```
&rarr; `int`

Prints the smallest integer that is greater than or equal to `val`.

### Parameters

**`val`** &larr; `float` <br/>
The input number.


## div

```rant

[%div: lhs; rhs]

```
&rarr; `any`

Divides two values and prints the quotient.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand (dividend).

**`rhs`** &larr; `any` <br/>
The right-hand operand (divisor).


## floor

```rant

[%floor: val]

```
&rarr; `int`

Prints the largest integer that is less than or equal to `val`.

### Parameters

**`val`** &larr; `float` <br/>
The input number.


## frac

```rant

[%frac: val]

```
&rarr; `float`

Prints the fractional part of `val`.

### Parameters

**`val`** &larr; `float` <br/>
The input number.


## max

```rant

[%max: values+]

```
&rarr; `any`

Returns the largest value in `values`.

Any elements of type `list` in `values` will be expanded to their individual elements
before the maximum value is calculated.

### Parameters

**`values`** &larr; `any+` <br/>
The input values.

### Examples

```rant
# Arguments can be single values
[max: 3; 2 |> assert-eq: 3]

# Lists are treated as their individual elements
[max: (3; 2) |> assert-eq: 3]

# Even alongside single values, lists are still expanded!
[max: 3; (4; -2; 0; 10); 6 |> assert-eq: 10]
```


## min

```rant

[%min: values+]

```
&rarr; `any`

Returns the smallest value in `values`.

Any elements of type `list` in `values` will be expanded to their individual elements
before the minimum value is calculated.

### Parameters

**`values`** &larr; `any+` <br/>
The input values.

### Examples

```rant
# Arguments can be single values
[min: 3; 2 |> assert-eq: 2]

# Lists are treated as their individual elements
[min: (3; 2) |> assert-eq: 2]

# Even alongside single values, lists are still expanded!
[min: 3; (4; -2; 0; 10); 6 |> assert-eq: -2]
```


## mod

```rant

[%mod: lhs; rhs]

```
&rarr; `any`

Gets the modulus of two values.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand (dividend).

**`rhs`** &larr; `any` <br/>
The right-hand operand (divisor).


## mul

```rant

[%mul: lhs; rhs]

```
&rarr; `any`

Multiplies two values and prints the product.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand.

**`rhs`** &larr; `any` <br.>
The right-hand operand.


## mul-add

```rant

[%mul-add: lhs; rhs; add]

```
&rarr; `any`

Multiplies two values, then adds another value to the result.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand of the multiplication.

**`rhs`** &larr; `any` <br/>
The right-hand operand of the multiplication.

**`add`** &larr; `any` <br/>
The value to add to the product.


## neg

```rant

[%neg: val]

```
&rarr; `any`

Negates a value and prints it.

### Parameters

**`val`** &larr; `any` <br/>
The input value.


## recip

```rant

[%recip: n]

```
&rarr; `any`

Gets the reciprocal of a value.


## sub

```rant

[%sub: lhs; rhs]

```
&rarr; `any`

Prints the difference between two values.

### Parameters

**`lhs`** &larr; `any` <br/>
The left-hand operand of the subtraction.

**`rhs`** &larr; `any` <br/>
The right-hand side of the subtraction.


## sin

```rant

[%sin: x]

```
&rarr; `float`

Calculates the sine of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input value, in radians.


## cos

```rant

[%cos: x]

```
&rarr; `float`

Calculates the cosine of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input value, in radians.


## tan

```rant

[%tan: x]

```
&rarr; `float`

Calculates the tangent of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input value, in radians.


## asin

```rant

[%asin: x]

```
&rarr; `float`

Calculates the arcsine (in radians) of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input sine value.


## acos

```rant

[%acos: x]

```
&rarr; `float`

Calculates the arccosine (in radians) of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input cosine value.


## atan

```rant

[%atan: x]

```
&rarr; `float`

Calculates the arctangent (in radians) of `x`.

### Parameters

**`x`** &larr; `float` <br/>
The input tangent value.


## atan2

```rant

[%atan2: y; x]

```
&rarr; `float`

Calculates the four-quadrant arctangent (in radians) of \\(\frac{y}{x}\\).

Returns 0 if `x` or `y` is 0.

### Parameters

**`y`** &larr; `float` <br/>
The input tangent's numerator.

**`x`** &larr; `float` <br/>
The input tangent's denominator.


## sqrt

```rant

[%sqrt: x]

```
&rarr; `float`

Calculates the square root of `x`.

### Parameters

**`x`** &larr; `int | float` <br/>
The input value.


## pow

```rant

[%pow: x; y]

```
&rarr; `int | float`

Calculates \\(x^y\\) and prints the result. Both `x` and `y` can be `int` or `float`.

### Parameters

**`x`** &larr; `int | float` <br/>
The base number.

**`y`** &larr; `int | flaot` <br/>
The exponent to raise `x` to.

### Errors

Raises an overflow error if a `x` is an `int` and `x ^ y` causes an overflow.