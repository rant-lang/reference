# Collections

Rant's variable system has two collection types: **lists** and **maps**.

## Lists

Lists are resizable arrays of values. They may contain multiple types of values.

Lists are initialized using a pair of parentheses containing the list elements, separated by semicolons:

```rant
# A pair of parentheses is treated like an empty list
<$empty-list = ()>

# Initialize a list with one empty element
<$one-empty = (<>)>

# Create a list with two empty elements
<$two-empty = (;)> # Short for (<>;<>)

# Create a list of numbers
<$lucky-numbers = (1; 2; 3; 5; 7; 11; 13)>

# Create a list of lists
<$important-lists = ((A; B; C); (D; E; F))>
```

## Maps

Maps are un-ordered collections of key-value pairs, where each key is unique.
Map keys are always strings: even if you try to use a non-string as a map key, it will be automatically converted to a string first.

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

Variable accessors can also access individual elements in lists and maps by using the access operator `/`.

```rant
<$person = @(
    name = Bob;
    age = 30;
    hobbies = (programming;hiking)
)>

name = <person/name>\n
age = <person/age>\n
hobbies = [join:<person/hobbies>;,\s]

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

<my-map/{a|b|c}>
# Outputs "foo", "bar", or "baz"
```

**List example**
```rant
<$my-list = (foo;bar;baz)>

<my-list/0>             # "foo"
<my-list/1>             # "bar"
<my-list/2>             # "baz"
<my-list/{[n:0;2]}>     # "foo", "bar", or "baz"
```