# Collections

Rant's variable system has 4 collection types: `list`, `map`, `string`, and `range`.

## List

The `list` type represents a mutable, resizable, ordered collection of zero or more values.

Lists are initialized using a pair of parentheses containing the list elements, separated by semicolons:

```rant
# A pair of parentheses is treated like an empty list
<$empty-list = ()>

# Initialize a list with one empty element
<$one-empty = (~)>

# Create a list of numbers
<$lucky-numbers = (1; 2; 3; 5; 7; 11; 13;)>

# Create a list of lists
<$important-lists = ((A; B; C); (D; E; F))>

# Trailing semicolons are allowed!
<$powers-of-two = (1; 2; 4; 8; 16;)>
```

### List indexing

List indices start at 0 and can be accessed by adding the index to the accessor path.

You can also use negative indices to access items relative to the end of a list, starting from -1 and going down.

```rant
# Create a list
<$list = (1;2;3;4;5;6;7;8;9)>

# Get first item
<list/0>\n      # 1

# Get second item
<list/1>\n      # 2

# Get last item
<list/-1>\n     # 9

# Get second to last item
<list/-2>\n     # 8

# Change third item from 3 to -3
<list/2 = -3>
<list/2>        # -3
```

## Map

The `map` type represents an unordered, mutable, resizable collection of zero or more key-value pairs, where each key is a unique string.

Map keys are always coerced to strings; if you try to access a map using a non-string key, the key will be automatically coerced to a string before use.

Maps use similar syntax to lists, but with some extra requirements:

* The `@` symbol must appear before the opening `(` to identify the collection as a map.
* Each element must be a key-value pair, with the key and value separated by an `=` symbol.

Map keys come in two flavors:
* **Static keys:** Evaluated at compile-time. They must be identifiers or string literals.
* **Dynamic keys:** Evaluated at run-time. They must be blocks.

```rant
# Create an empty map
<$empty-map = @()>

# Create a map with various value types
<$secret-key = occupation>
<$person = @(
    name = John;
    age = 25;
    "favorite color" = {red|green|blue};
    {<secret-key>} = programmer
)>
```

## Range

The `range` type represents a linear series of integers parameterized by three values:

1. an inclusive **start** bound,
2. an exclusive **end** bound,
3. the **interval** between values in the range.

As such, very large ranges can be stored, indexed, and enumerated without needing to pre-allocate all possible values in memory.

Ranges are created with the built-in `[range]` function:

```rant
# Print numbers 0 through 4
[cat: **[range: 0; 5]; \n]

##
  Output:
  0
  1
  2
  3
  4
##
```

Backwards ranges are possible, too; just use a start bound larger than the end bound:

```rant
# Print numbers 4 through 0
[cat: **[range: 4; -1]; \n]

##
  Output:
  4
  3
  2
  1
  0
##
```

By default, `[range]` uses an interval of 1, but you can change this by adding a third argument:

```rant
# Print every second number between 0 and 9
[cat: **[range: 0; 10; 2]; \n]

##
  Output:
  0
  2
  4
  6
  8
##
```

## Retrieving values from collections

Variable accessors can access individual elements in lists and maps by using the access operator `/`.

```rant
<$person = @(
    name = Bob;
    age = 30;
    hobbies = (programming;hiking)
)>

name = <person/name>\n
age = <person/age>\n
hobbies = [join: <person/hobbies>; ,\s]

##
    Output:

    name = Bob
    age = 30
    hobbies = programming, hiking
##
```

Additionally, a variable access path does not need to be made out of entirely constants. You can use a block to resolve to a key or index.

**Map example**

```rant
<$my-map = @(
    a = foo; b = bar; c = baz
)>

<my-map/{{a|b|c}}>
# Outputs "foo", "bar", or "baz"
```

**List example**
```rant
<$my-list = (foo;bar;baz)>

<my-list/0>             # "foo"
<my-list/1>             # "bar"
<my-list/2>             # "baz"
<my-list/{[rand:0;2]}>   # "foo", "bar", or "baz"
```

## Supported operations

Some collections can be mutated (modified), while others are read-only. Some can be sliced but not spliced. 
Below is a breakdown of which operations each collection type supports:


|Type      |Read     |Write    |Slice    |Splice   |
|:--------:|:-------:|:-------:|:-------:|:-------:|
|`list`    |&#x1f7e2;|&#x1f7e2;|&#x1f7e2;|&#x1f7e2;|
|`map`     |&#x1f7e2;|&#x1f7e2;|&#x1f534;|&#x1f534;|
|`string`  |&#x1f7e2;|&#x1f534;|&#x1f7e2;|&#x1f534;|
|`range`   |&#x1f7e2;|&#x1f534;|&#x1f7e2;|&#x1f534;|

<p></p>

|Legend                                            |
|:------------------------------------------------:|
|&#x1f7e2; = supported; &#x1f534; = not supported  |


## Collection auto-concatenation

Multiple collections of the same type are automatically concatenated or merged when printed alone in the same sequence.
This significantly reduces the amount of boilerplate required when generating collections with varying amount of elements, or elements that are conditionally included.

### Examples

```rant
# List auto-concatenation
[assert-eq: (A)(B); (A; B)]
```

```rant
# Probabilistic list generation
<%strange-list = { (A; B) | (C; D) } { (E; F) | (G; H) }>
##
<strange-list> will be one of:
  * (A; B; E; F)
  * (A; B; G; H)
  * (C; D; E; F)
  * (C; D; G; H)
##
```

```rant
# Automatically combine two maps
<%data = 
    @(
        foo = 1
    )
    @(
        bar = 2
    )
>

[assert-eq: <data/foo?>; 1]
[assert-eq: <data/bar?>; 2]
```