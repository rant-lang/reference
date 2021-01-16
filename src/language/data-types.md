# Data types

Rant has 10 built-in data types:

|Type name |Description                                        |Pass type|
|----------|---------------------------------------------------|---------|
|`string`  |Sequence of UTF-8 characters                       |by-value |
|`int`     |64-bit signed integer                              |by-value |
|`float`   |64-bit double-precision float                      |by-value |
|`bool`    |Boolean value                                      |by-value | 
|`function`|Function/closure                                   |by-ref   |
|`list`    |List of values                                     |by-ref   |
|`map`     |String-keyed collection of values                  |by-ref   |
|`block`   |Stored block                                       |by-ref   |
|`special` |Handle to internal runtime data, such as a selector|by-ref   |
|`empty`   |Unit type representing "null" value                |by-value |

## The `empty` type

To represent the lack of a value, Rant has the `empty` type, which has only one possible value, represented by the token `~`.

```rant
<$nothing = ~>    # i.e. <$nothing>
[type:<nothing>]  # empty
```

## Boolean values

The two boolean values are represented by the keywords `true` and `false`.
These keywords can still be used as fragments when not used alone, as their string representations are simply `"true"` and `"false"`;
however, if they are passed on their own and need to be strings, you will need to put them in a string literal.

## Type inference for expressions

In order to resolve type ambiguities, Rant makes a few basic assumptions:

#### Integers

Any number token without a decimal place becomes an `int`.

```rant
[type:123]  # int
```

#### Floats

Any number token with a decimal place becomes a `float`.

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

A sequence will evaluate to a string if the following are true:

1. There are multiple values in the expression
2. At least one value is non-empty
3. The sequence is not all lists or all maps

When these conditions are met, all values printed by the sequences are converted to their string representations and concatenated.

```rant
# Even though they are all integer tokens, they are treated as text
[type:10 20 30 40 50]  # string
```

#### Lists

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

#### Maps

A sequence that is entirely made of maps will return a single map containing the key/value pairs of the input maps. 
Any duplicate keys are overwritten.

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
    @(item_{[step]}) = [step]
}
# returns @(item_1 = 1; item_2 = 2; item_3 = 3)
```

#### Empties

Expressions containing only empties evaluate to the empty value.

Expressions containing nothing also evaluate to the empty value.

```rant
[type:~~]       # empty
[type:~]        # empty
[type:]         # empty
```