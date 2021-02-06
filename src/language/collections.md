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

# Create a list with two empty elements
<$two-empty = (;)> # Short for (~;~)

# Create a list of numbers
<$lucky-numbers = (1; 2; 3; 5; 7; 11; 13)>

# Create a list of lists
<$important-lists = ((A; B; C); (D; E; F))>
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