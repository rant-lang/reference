# Data types

Rant has 10 built-in data types:

|Type name |Description                                        |Pass type|
|----------|---------------------------------------------------|---------|
|`string`  |Sequence of UTF-8 characters                       |by-value |
|`integer` |64-bit signed integer                              |by-value |
|`float`   |64-bit double-precision float                      |by-value |
|`bool`    |Boolean value                                      |by-value | 
|`function`|Function/closure                                   |by-ref   |
|`list`    |List of values                                     |by-ref   |
|`map`     |String-keyed collection of values                  |by-ref   |
|`block`   |Stored block                                       |by-ref   |
|`special` |Handle to internal runtime data, such as a selector|by-ref   |
|`empty`   |Unit type representing "null" value                |by-value |

## The `empty` type

To represent the lack of a value, Rant has the `empty` type, which has only one possible value, represented by the token `<>`.

```rant
<$nothing = <>>   # i.e. <$nothing>
[type:<nothing>]  # empty
```

## Boolean values

The two boolean values are represented by the keywords `true` and `false`.
These keywords can still be used as fragments when not used alone, as their string representations are simply `"true"` and `"false"`;
however, if they are passed on their own and need to be strings, you will need to put them in a string literal.

## Type inference for expressions

In order to resolve type ambiguities, Rant makes a few basic assumptions:

#### Integers

Any number token without a decimal place becomes an integer.

```rant
[type:123]  # integer
```

#### Floats

Any number token with a decimal place becomes a float.

```rant
[type:123.0]  # float
```

#### Top-level fragments or whitespace

Any expression containing top-level text (i.e. not in a collection) evaluates to a string.

Whitespace at the start or end of an expression is ignored.

```rant
# Since there are fragments and whitespace, it's a string
[type:99 bottles of beer]  # string

# Since there is whitespace between the numbers, the value is still a string
[type:99 99]  # string
```

#### Multiple values in a sequence

If there are multiple values in an expression and at least one is non-empty, it evaluates to a string.

```rant
# Even though they are all integer tokens, they are treated as text
[type:10 20 30 40 50]  # string
```

#### Empties

Expressions containing only empties evaluate to the empty value.

Expressions containing nothing also evaluate to the empty value.

```rant
[type:<><>]     # empty
[type:<>]       # empty
[type:]         # empty
```