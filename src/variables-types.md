# Variables & Data Types

Variables enable you to store and retrieve values.

Rant is a dynamically-typed language, which means that variables don't have to contain a specific type;
for example, you can initialize a variable with an integer, and later change it to a string (and vice versa).

Rant has the following data types:

|Type name |Description                                        |Pass type|
|----------|---------------------------------------------------|---------|
|`string`  |Sequence of UTF-8 characters                       |by-value |
|`int`     |64-bit signed integer                              |by-value |
|`float`   |64-bit double-precision float                      |by-value |
|`bool`    |Boolean value                                      |by-value | 
|`range`   |Indexable range of integers with optional interval |by-value |
|`empty`   |Unit type representing "null" value                |by-value |
|`function`|Function/closure                                   |by-ref   |
|`list`    |List of values                                     |by-ref   |
|`map`     |String-keyed collection of values                  |by-ref   |
|`special` |Handle to internal runtime data, such as a selector|by-ref   |

## The `empty` type

To represent the lack of a value, Rant has the `empty` type, 
which has only one possible value, represented in Rant by the literal `<>` (referred to as "emptyval").

Printing emptyval will have no effect on the output.

```rant
<$nothing = <>>   # i.e. <$nothing>
[type:<nothing>]  # empty
```

## The `bool` type

The two boolean values are represented by the keywords `@true` and `@false`.

### Integers

Any number literal without a decimal place becomes an `int`.

```rant
[type:123]  # int
```

### Floats

Any number literal with a decimal place becomes a `float`.

```rant
[type:123.0]  # float
```

## Type inference for multi-part expressions

At the end of an expression, Rant adds each printed value together from left to right into a single value that is printed to the caller.

In order to resolve type ambiguities, Rant follows a few rules when concatenating various types:


### Expressions with strings

If an expression contains a string, fragment, or hinted element, the combined value from the left as well as every value on the right will be coerced to a string.

```rant
# Since there are fragments and whitespace, it's a string
<$s = 99 bottles of beer> # -> "99 bottles of beer"
[type:<s>]  # string
```

### Multiple numbers

If the start of an expression is a series of numbers, they will be added together:

```rant
3
0.14
# -> 3.14
```

### Multiple lists

A sequence that is entirely made of lists will return a single list containing the concatenation of the input lists.

```rant
(1; 2) (3; 4) # same as (1; 2; 3; 4)
```

This rule also applies when the sequence contains any expression that returns a list:

```rant
[rep:10] {
    ([step])
}
# returns (1; 2; 3; 4; 5; 6; 7; 8; 9; 10)
```

### Multiple maps

A sequence that is entirely made of maps will return a single map containing the key/value pairs of the input maps. 
Duplicate keys are overwritten by newer values.

```rant
<%my-map = 
    @(a = 1)
    @(b = 2)
>
# returns @(a = 1; b = 2)
```

As with list sequences, this also applies with expressions that return maps:

```rant
[rep:3]{
    @( {item_[step]} = [step] )
}
# returns @(item_1 = 1; item_2 = 2; item_3 = 3)
```

### Empties

Expressions containing only empties evaluate to a single emptyval.

Expressions containing nothing also evaluate to emptyval.

```rant
[type:<><>]     # empty
[type:<>]       # empty
[type:]         # empty
```