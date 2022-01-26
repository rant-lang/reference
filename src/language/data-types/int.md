# The `int` type

The `int` type represents a signed 64-bit integer.

## Range

The `int` type covers the range between -9,223,372,036,854,775,808 and 9,223,372,036,854,775,807.

## Coercion to `float`

The following operations will always produce a `float` value as the result, even if one of the operands is an `int`:

1. Performing any math operation, such as addition, between an `int` value and a `float` value
1. Raising an `int` value to a negative power, even if the exponent is also an `int`
1. Summing `int` and `float` values implicitly through a multi-part expression