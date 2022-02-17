# Operators

Rant has several built-in arithmetic, logic, and comparison operators.

Throughout this page, the abbreviations RHS (right-hand side) and LHS (left-hand side) will be used to refer to binary operands.

## Arithmetic operators

### Addition

`+` *(binary infix operator)*

Returns the sum of the operands.

```rant
2 + 2
# -> 4
```

### Subtraction

`-` *(binary infix operator)*

Subtracts RHS from LHS and returns the result.

```rant
10 - 1
# -> 9
```

### Multiplication

`*` *(binary infix operator)*

Returns the product of the operands.

```rant
5 * 5
# -> 25
```

### Division

`/` *(binary infix operator)*

Divides LHS by RHS and returns the result.

```rant
48 / 16
# -> 3
```

### Modulo

`%` *(binary infix operator)*

Gets the remainder from dividing LHS by RHS and returns the result.

```rant
10 % 4
# -> 2
```

### Exponentiation

`**` *(binary infix operator)*

Raises LHS to the RHS power and returns the result.

```rant
2 ** 16
# -> 65536
```

### Negation

`@neg` *(unary prefix operator)*

Gets the negated value of the operand and returns the result.

```rant
<$x = 123>
@neg <x>
# -> -123
```

Note: you may also use the minus (`-`) symbol when negating numbers (e.g. `-123`).

## Logic operators

### Logical AND

`&` *(binary infix operator)*

Returns `@true` if both operands are `@true`.
Returns `@false` if both operands are `@false`, or if one is `@true` and the other `@false`.

More generally: returns RHS if both LHS and RHS are truthy; otherwise, returns the first falsy value.

This operator is short-circuiting: if LHS is falsy, RHS will not be evaluated.

```rant
# Logical AND using booleans
@true & @true    # -> @true
@true & @false   # -> @false
@false & @true   # -> @false
@false & @false  # -> @false

# Logical AND using truthiness
2 & 1            # -> 1
1 & 2            # -> 2
1 & 0            # -> 0
0 & 2            # -> 0
0 & <>           # -> 0
<> & 0           # -> <>
```

### Logical OR

`|` *(binary infix operator)*

Returns `@true` if one or both operands are `@true`.
Returns `@false` if both operands are `@false`.

More generally: returns LHS if LHS is truthy; otherwise, returns RHS.

This operator is short-circuiting: if LHS is truthy, RHS will not be evaluated.

```rant
# Logical OR using booleans
@true | @true     # -> @true
@true | @false    # -> @true
@false | @true    # -> @true
@false | @false   # -> @false

# Logical OR using truthiness
2 | 1             # -> 2
1 | 2             # -> 1
1 | 0             # -> 1
0 | 2             # -> 2
0 | <>            # -> <>
<> | 0            # -> 0
```

> **Syntax note**
>
> In a block context, `|` will be treated as an element separator.
> To use it as an OR operator, enclose your expression in parentheses first.
> ```rant
> foo | bar         # Logical OR
> {foo | bar}       # Separates two block elements
> {(foo | bar)}     # Logical OR
> ```

### Logical NOT

`@not` *(unary prefix operator)*

Returns `@false` if the operand is truthy; otherwise, returns `@true`.

```rant
# Logical NOT using booleans
@not @true  # -> @false
@not @false # -> @true

# Logical NOT using truthiness
@not 1      # -> @false
@not 0      # -> @true
```

### Logical XOR

`^` *(binary infix operator)*

Returns `@true` if exactly *one* of the two operands is truthy; otherwise, returns `@false`. 

```rant
# Logical XOR using booleans
@true ^ @true    # -> @true
@true ^ @false   # -> @true
@false ^ @true   # -> @true
@false ^ @false  # -> @false

# Logical XOR using truthiness
2 ^ 1            # -> @false
1 ^ 2            # -> @false
1 ^ 0            # -> @true
0 ^ 2            # -> @true
0 ^ <>           # -> @false
<> ^ 0           # -> @false
```

## Comparison operators

### Equality

`@eq` *(binary infix operator)*

Returns `@true` if LHS is equal to RHS; otherwise, returns `@false`.

```rant
1 @eq 1     # -> @true
1 @eq 1.0   # -> @true
0 @eq 1     # -> @false
1 @eq "1"   # -> @false
```

### Inequality

`@neq` *(binary infix operator)*

Returns `@true` if LHS is not equal to RHS; otherwise, returns `@false`.

```rant
1 @neq 1    # -> @false
1 @neq 1.0  # -> @false
0 @neq 1    # -> @true
1 @neq "1"  # -> @true
```

### Greater than

`@gt` *(binary infix operator)*

Returns `@true` if LHS is greater than RHS; otherwise, returns `@false`.

```rant
1 @gt 1     # -> @false
1 @gt 2     # -> @false
2 @gt 1     # -> @true
```

### Less than

`@lt` *(binary infix operator)*

Returns `@true` if LHS is less than RHS; otherwise, returns `@false`.

```rant
1 @gt 1     # -> @false
1 @gt 2     # -> @true
2 @gt 1     # -> @false
```

### Greater than or equal

`@ge` *(binary infix operator)*

Returns `@true` if LHS is greater than or equal to RHS; otherwise, returns `@false`.

```rant
1 @gt 1     # -> @true
1 @gt 2     # -> @false
2 @gt 1     # -> @true
```

### Less than or equal

`@le` *(binary infix operator)*

Returns `@true` if LHS is less than or equal to RHS; otherwise, returns `@false`.

```rant
1 @gt 1     # -> @true
1 @gt 2     # -> @true
2 @gt 1     # -> @false
```


## Precedence

Operators with higher precedence are evaluated before those with lower precedence.
The table below lists operator sets in order of descending precedence.
Operators in the same row have the same precedence.

| Operators                  | Category       |
|----------------------------|----------------|
| `@not`, `@neg`             | Prefix         |
| `**`                       | Exponential    |
| `*`, `/`, `%`              | Multiplicative |
| `+`, `-`                   | Additive       |
| `@lt`, `@le`, `@gt`, `@ge` | Relational     |
| `@eq`, `@neq`              | Equality       |
| `&`                        | Conjunctive    |
| `^`                        | Logical XOR    |
| `|`                        | Disjunctive    |