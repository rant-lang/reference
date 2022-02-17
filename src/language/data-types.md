# Data Types

Rant has a dynamic type system, which means that variables also don't have to contain a specific type;
for example, you can initialize a variable with an integer, and later change it to a string (and vice versa).

Rant's type system supports the following data types:

| Type name  | Description                                         | Pass type |
|------------|-----------------------------------------------------|-----------|
| `string`   | Sequence of UTF-8 characters                        | by-value  |
| `int`      | 64-bit signed integer                               | by-value  |
| `float`    | 64-bit double-precision float                       | by-value  |
| `bool`     | Boolean value                                       | by-value  |
| `list`     | List of values                                      | by-ref    |
| `tuple`    | Tuple of values                                     | by-ref    |
| `map`      | String-keyed collection of values                   | by-ref    |
| `range`    | Indexable range of integers with optional interval  | by-value  |
| `function` | Function/closure                                    | by-ref    |
| `selector` | Handle to a selector                                | by-ref    |
| `nothing`  | Unit type representing "null" value                 | by-value  |

## Integer literals

Any number literal without a decimal place is known as an **integer literal**.

An integer literal produces a value of type `int`.

```rant
[type: 123]  # int
```

## Real literals

Any number literal with a decimal place is known as a **real literal**. 

A real literal produces a value of type `float`.

```rant
[type: 123.0]  # float
```

## Collections

Rant's variable system has five collection types: `list`, `tuple`, `map`, `string`, and `range`.

Some collections can be mutated (modified), while others are read-only. Some can be sliced but not spliced. 
Below is a breakdown of which operations each collection type supports:


|   Type   |   Read    |   Write   |   Slice   |  Splice   |
|:--------:|:---------:|:---------:|:---------:|:---------:|
|  `list`  | &#x1f7e2; | &#x1f7e2; | &#x1f7e2; | &#x1f7e2; |
| `tuple`  | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
| `string` | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
| `range`  | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
|  `map`   | &#x1f7e2; | &#x1f7e2; | &#x1f534; | &#x1f534; |

<p></p>

|Legend                                            |
|:------------------------------------------------:|
|&#x1f7e2; = supported; &#x1f534; = not supported  |

## Type inference for multi-part expressions

At the end of an expression, Rant adds each printed value together from left to right into a single value that is printed to the caller.

In order to resolve type ambiguities, Rant follows a few rules when concatenating various types:


### Expressions with strings

If an expression contains a string, fragment, or hinted element, the combined value from the left as well as every value on the right will be coerced to a string.

```rant
# Since there are fragments and whitespace, it's a string
[type: 99 bottles of beer]  # string
```

### Multiple numbers

If the start of an expression is a series of numbers, they will be added together:

```rant
3
0.14
# -> 3.14
```


### Multiple lists and tuples

For any expression that only contains lists and/or tuples, the following rules apply:

* An expression that prints multiple lists will return a single list containing the elements of all the original lists in the same order.
* An expression that prints multiple tuples will return a single tuples containing the elements of all the original lists in the same order.
* An expression that prints one or more tuples and one or more lists will return a single list containing the elements of all the original tuples and lists in the same order.


**Multiple lists in an expression**
```rant
(: 1; 2) (: 3; 4) 
# -> (: 1; 2; 3; 4)
```

**Multiple tuples in an expression**
```rant
(1; 2) (3; 4) 
# -> (1; 2; 3; 4)
```

**Mixed tuples and lists in an expression**
```rant
(1; 2) (: 3; 4) (5; 6) (: 7; 8)
# -> (: 1; 2; 3; 4; 5; 6; 7; 8)
```

**Joining lists with a repeater**
```rant
[rep:10] {
    (: [step])
}
# -> (: 1; 2; 3; 4; 5; 6; 7; 8; 9; 10)
```

**Joining tuples with a repeater**
```rant
[rep:10] {
    ([step];)
}
# -> (1; 2; 3; 4; 5; 6; 7; 8; 9; 10)
```

### Nothings

Printing nothing does nothing. Empty expressions return nothing.

```rant
[type:<><>]     # nothing
[type:<>]       # nothing
[type:]         # nothing
```