# Collection Access

An accessor can operate on specific elements of collections (lists, maps, strings, and ranges) using an **access path**.

An access path is made up of one or more **access path components**, of which there are several types: **indices**, **keys**, **dynamic keys**, and **slices**.
These are separated by the path separator token `/`.

## Indexing

Accessing elements in ordered collections (lists, strings, and ranges) is known as **indexing**.
All Rant collections use "zero-based indexing"; in other words, the first element starts at index 0, the second at index 1, and so on.

```rant
<%numbers = (: 1; 3; 5; 7; 9)>

# Set the first number to 1
<numbers/0 = 100>

# Get the first number
<numbers/0> # -> 100
```

Negative indices are relative to the end of the collection. This means `-1` represents the last element, `-2` the penultimate element, and so on.

```rant
<%msg = "hello">
Last char: <msg/-1>\n # same as <msg/4> or <msg/{[sub: [len: <msg>]; 1]}>

# Last char: o
```

## Keying

Accessing elements in maps is known as **keying**. 
Simply specify the desired map key after the `/` to access the map element with that key:

```rant
<%citizen = (::
    name = "Steve";
    age = 50;
    mood = "angry";
)>

# Set <citizen/age> to 150
<citizen/age = 150>

<citizen/name>\n    # -> Steve
<citizen/age>\n     # -> 150
<citizen/mood>\n    # -> angry
```

Keys follow the same naming rules as variables, unless specified as a dynamic key (see below).

## Dynamic keys

Where an index or key must be calculated at runtime, a dynamic key may be used. Dynamic keys are single-element blocks that returns an `int` or `string`.

```rant
<%fruits = (apple; orange; banana; tomato)>

<fruits/{ [len: <fruits> |> sub: 1 |> rand: 0; []] }> # returns a random fruit
```

The value of a dynamic key must be compatible with the type of collection being accessed: for example, a `string` cannot be used to index a `list`, but an `int` can be used to key a `map` because its conversion to a string is infallible (in other words, all `int` values have a valid `string` conversion).

### Dynamic key type compatibility


|Collection type|Key is `string`|Key is `int`|
|:-------------:|:-------------:|:----------:|
|`list`  |🔴|🟢|
|`tuple` |🔴|🟢|
|`range` |🔴|🟢|
|`string`|🔴|🟢|
|`map`   |🟢|🟠|

<p></p>

|Legend                                    |
|:----------------------------------------:|
|🟢 = valid; 🟠 = coerced; 🔴 = invalid|

## Slicing

Accessing a contiguous range of elements in an ordered collection is known as **slicing**. 
Slices can be fully-bounded (having start + end points), half-bounded (having a start or end point but not both), or unbounded (all elements).

When you get a slice of a collection, the accessor returns a new copy of the collection containing the slice contents.

Slice notation takes the following forms:

```rant
# fully-bounded
<my-list/2:5>   # get all elements between index 2 (inclusive) and index 5 (exclusive)

# start-bounded
<my-list/2:>    # get all emements starting at index 2 (inclusive)

# end-bounded
<my-list/:5>    # get all elements until index 5 (exclusive)

# unbounded
<my-list/:>     # get all elements (equivalent to a shallow-clone)
```

#### Splicing

You can also set a slice on mutable collection types, an operation also known as **splicing**:

```rant
<$my-list = (: 1; 2; 3)>
<my-list/1:2 = (: a; b)> # the splice value doesn't have to be the same size!
<my-list/3:4 = (c; d)> # the splice value can also be a tuple!
<my-list> # -> (: 1; a; b; 3)
```

#### Dynamic slices

Slices also support dynamic bounds; just replace any slice bound index with a single-element block that returns an `int` value.

```rant
<%message = "fantastic">
[rep: [len: <message>]]
{
    # Use the current block iteration number to slice the message
    <message/:{[step]}>\n
}
```
This produces the following output:
```
f 
fa
fan
fant
fanta
fantas
fantast
fantasti
fantastic
```

## Nested access paths

Access paths can be nested. This means if you have an array in a map and you want to access an element of that array, you most certainly can; just add another component to the path.

```rant
<%arrays = (::
    odd-numbers = (: 1; 3; 5; 7; 9);
    even-numbers = (: 0; 2; 4; 6; 8);
)>

# Get the last element of <arrays/odd-numbers>
<arrays/odd-numbers/-1>
```