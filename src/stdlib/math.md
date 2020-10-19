# Standard Library: Math functions

### [abs: num]
&rarr; `int` or `float`

Calculates the absolute value of `num`.

#### Errors

Raises an error if `num` is an integer and the absolute value overflows.

### [add: lhs; rhs]
&rarr; `any`

Adds two values.

### [ceil: val]
&rarr; `int`

Gets the smallest integer that is greater than or equal to `val`.

`val` must be a `float`.

### [div: lhs; rhs]
&rarr; `any`

Divides two values.

### [floor: val]
&rarr; `int`

Gets the largest integer that is less than or equal to `val`.

`val` must be a `float`.

### [frac: val]
&rarr; `float`

Gets the fractional part of `val`.

`val` must be a `float`.

### [max: values+]
&rarr; `any`

Returns the largest value in `values`.

Any elements of type `list` in `values` will be expanded to their individual elements
before the maximum value is calculated.

#### Examples

```rant
# Arguments can be single values
[max: 3; 2 & assert-eq: 3]

# Lists are treated as their individual elements
[max: (3; 2) & assert-eq: 3]

# Even alongside single values, lists are still expanded!
[max: 3; (4; -2; 0; 10); 6 & assert-eq: 10]
```

### [min: values+]
&rarr; `any`

Returns the smallest value in `values`.

Any elements of type `list` in `values` will be expanded to their individual elements
before the minimum value is calculated.

#### Examples

```rant
# Arguments can be single values
[min: 3; 2 & assert-eq: 2]

# Lists are treated as their individual elements
[min: (3; 2) & assert-eq: 2]

# Even alongside single values, lists are still expanded!
[min: 3; (4; -2; 0; 10); 6 & assert-eq: -2]
```

### [mod: lhs; rhs]
&rarr; `any`

Gets the modulus of two values.

### [mul: lhs; rhs]
&rarr; `any`

Multiplies two values.

### [mul-add: lhs; rhs; add]
&rarr; `any`

Multiplies two values, then adds another value to the result.

### [neg: n]
&rarr; `any`

Negates a value.

### [recip: n]
&rarr; `any`

Gets the reciprocal of a value.

### [sub: lhs; rhs]
&rarr; `any`

Subtracts two values.

### [sin: x]
&rarr; `float`

Calculates the sine of `x` (in radians).

### [cos: x]
&rarr; `float`

Calculates the cosine of `x` (in radians).

### [tan: x]
&rarr; `float`

Calculates the tangent of `x` (in radians).

### [asin: x]
&rarr; `float`

Calculates the arcsine (in radians) of `x`.

### [acos: x]
&rarr; `float`

Calculates the arccosine (in radians) of `x`.

### [atan: x]
&rarr; `float`

Calculates the arctangent (in radians) of `x`.

### [atan2: y; x]
&rarr; `float`

Calculates the four-quadrant arctangent (in radians) of `y / x`.

### Notes

Returns 0 if `x` or `y` is 0.

### [sqrt: x]
&rarr; `float`

Calculates the square root of `x`.

### [pow: x; y]

Raises `x` to the power of `y`. Both `x` and `y` can be `int` or `float`.

#### Errors

Raises an overflow error if a `x` is an `int` and `x ^ y` causes an overflow.