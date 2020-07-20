# Variables

Rant programs can define and use variables of several types.

Because Rant is a dynamically-typed langauge, variables have no type constraints; the type of a variable is determined by the type of its current value.

## Value types

Rant supports eight value types:

|Type name|Description|Rant API|
|---------|-----------|--------|
|`string`|Sequence of UTF-8 characters|`RantValue::String(&str)`|
|`integer`|64-bit signed integer|`RantValue::Integer(i64)`|
|`float`|64-bit double-precision float|`RantValue::Float(f64)`|
|`bool`|Boolean value|`RantValue::Bool(bool)`|
|`function`|Function/closure|`RantValue::Function(...)`|
|`list`|List of values|`RantValue::List(Rc<Vec<RantValue<'a>>>)`|
|`map`|String-keyed collection of values|`RantValue::Map(Rc<RantMap<'a>>)`||
|`none`|Null value|`RantValue::None`|

> TODO: Finalize equivalent Rust RantValue types

## Basic syntax

All variable access operations are enclosed in angle brackets.

Variable accessors have three subtypes: **definitions**, **assignments**, and **getters**.

### Definition

Defining a variable creates it in the current scope, but may not necessarily initialize it with a value.

All variable definitions begin with the `$` symbol.

```rant
# Define a variable `name` but leave it empty (value is `none`)
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


## The `none` type

To represent the lack of a value, Rant has the `none` type, which has only one possible value, represented as the token `<>`.

```rant
<$nothing = <>>   # i.e. <$nothing>
[type:<nothing>]  # none
```

## Boolean values

The two boolean values are accessed through the reserved getters `<true>` and `<false>`.
These variable names are reserved and evaluated at compile time.

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

#### Multiple `<>` values are coerced to `<>`
```rant
[type:<><>]   # none
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