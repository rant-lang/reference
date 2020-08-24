# Variables

Rant programs can define and use variables of several types.

Because Rant is a dynamically-typed langauge, variables have no type constraints; the type of a variable is determined by the type of its current value.

## Value types

Rant currently supports nine value types:

|Type name |Description                                        |Pass type|
|----------|---------------------------------------------------|---------|
|`string`  |Sequence of UTF-8 characters                       |by-value |
|`integer` |64-bit signed integer                              |by-value |
|`float`   |64-bit double-precision float                      |by-value |
|`bool`    |Boolean value                                      |by-value | 
|`function`|Function/closure                                   |by-ref   |
|`list`    |List of values                                     |by-ref   |
|`map`     |String-keyed collection of values                  |by-ref   |
|`special` |Handle to internal runtime data, such as a selector|by-ref   |
|`empty`   |Unit type representing "null" value                |by-value |

## Basic syntax

All variable access operations are enclosed in angle brackets.

Variable accessors have three subtypes: **definitions**, **assignments**, and **getters**.

### Definition

Defining a variable creates it in the current scope, but may not necessarily initialize it with a value.

All variable definitions begin with the `$` symbol.

```rant
# Define a variable `name` but leave it empty (value is `<>`)
<$name>

# Define a variable `name` and assign it the string "Nick"
<$name = Nick>
```

### Assignment

Variable assignments include a variable name and value separated by a `=` symbol.

```rant
# Overwrite value on existing variable `name`
<name = Nicholas>
```

### Getters

A variable getter only requires the name and adds the variable's value to the output.

Attempting to retrieve a variable that does not exist results in a runtime error.

```rant
# Get value of `name` (note the lack of '$')
My name is <name>. # Prints "My name is Nicholas."
```


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

## Implicit type coercion

In order to resolve type ambiguities, Rant follows a few rules to infer types for certain kinds of values:

#### A number without a decimal place becomes an integer

```rant
<$val = 123>
[type:<val>]  # integer
```

#### A number with a decimal place becomes a float

```rant
<$val = 123.0>
[type:<val>]  # float
```

#### Any value containing fragments or whitespace is always coerced to a string

```rant
<val = 99 bottles of beer>
# Since there are fragments and whitespace, it's a string
[type:<val>]  # string

<val = 99 99>
# Since there is whitespace between the numbers, the value is still a string
[type:<val>]  # string
```

#### Multiple values of any type are always coerced to a single string, as long as one of the values isn't `<>`
```rant
<$val = 10 20 30 40 50>
# Even though they are all integer tokens, they are treated as text
[type:<val>]  # string
```

#### Multiple empties are coerced to a single `<>`
```rant
[type:<><>]   # empty
```


### Overriding variables from a parent scope

Variables in a parent scope can be non-destructively overridden in child scopes by defining a variable of the same name.

```rant
# Define variable `a` in parent scope
<$a = foo>
a = <a>\n
{
    # Define another variable `a` in child scope
    # Parent variable is not affected
    <$a = bar>
    a = <a>\n
}
# Parent variable takes over after child scope exits
a = <a>

##
    Output:

    a = foo
    a = bar
    a = foo
##
```