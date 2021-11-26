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

To represent the lack of a value, Rant has the `empty` type, which has only one possible value, represented by the literal `<>`.

```rant
<$nothing = <>>   # i.e. <$nothing>
[type:<nothing>]  # empty
```

## The `bool` type

The two boolean values are represented by the keywords `@true` and `@false`.

## Type inference for expressions

In order to resolve type ambiguities, Rant makes a few basic assumptions:

### Integers

Any number token without a decimal place becomes an `int`.

```rant
[type:123]  # int
```

### Floats

Any number token with a decimal place becomes a `float`.

```rant
[type:123.0]  # float
```

### Top-level text

Any expression containing top-level text (i.e. not in a collection) evaluates to a string.

Whitespace at the start or end of an expression is ignored.

```rant
# Since there are fragments and whitespace, it's a string
[type:99 bottles of beer]  # string

# Since there is whitespace between the numbers, the value is still a string
[type:99 99]  # string
```

### Multiple values in a sequence

A sequence will evaluate to a string if the following are true:

1. There are multiple values in the expression
2. At least one value is non-empty
3. The sequence is not all lists or all maps

When these conditions are met, all values printed by the sequences are converted to their string representations and concatenated.

```rant
# Even though they are all integer tokens, they are treated as text
[type:10 20 30 40 50]  # string
```

#### Multiple lists

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

#### Multiple maps

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

#### Empties

Expressions containing only empty literals evaluate to a single empty.

Expressions containing nothing also evaluate to an empty.

```rant
[type:<><>]     # empty
[type:<>]       # empty
[type:]         # empty
```