# Standard Library: Collection functions

### [assoc: keys; values]
&rarr; `map`

Creates a map from a list of keys and a list of values.
Each key in `keys` will be matched with the value at the same index in `values`.

Raises a runtime error if the lists are not the same length.

#### Example

```rant
# Generate a map of the "Big Five" personality traits
# with random rating values that add up to 50
<$personality = 
  [assoc:
    (ope; con; ext; agr; neu);
    [shred: 50; 5; [rand: 1; 10]] # Use random variance to reduce trait deviation
  ]
>

# Print the values
[whitespace-fmt:verbatim]
"Openness to experience:"   <personality/ope>\n
"Conscientiousness:"        <personality/con>\n
"Extraversion:"             <personality/ext>\n
"Agreeableness:"            <personality/agr>\n
"Neuroticism:"              <personality/neu>\n


##
  EXAMPLE OUTPUT:

  Openness to experience:   7
  Conscientiousness:        11
  Extraversion:             5
  Agreeableness:            12
  Neuroticism:              15
##
```

### [clear: collection]

Removes all elements from a list or map.

#### Errors

Causes a runtime error if `collection` is not a list or map.

### [collect: values*]
&rarr; `list`

Returns a `list` containing the arguments.

### [filter: list; predicate]
&rarr; `list`

Runs a predicate function against all items in a list and returns another list containing only the values that the predicate returned `true` on.

The predicate function must accept a single parameter and return a `bool` value.

#### Examples

##### Filter a list of numbers by only those divisible by 3
```rant
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10; 11; 12)>
<$multiples-of-three = [filter: <numbers>; [?:x] { [is-factor: <x>; 3] }]>
[join: ,\s; <multiples-of-three>]
# -> 3, 6, 9, 12
```

##### Filter a list of numbers by only odd numbers
```rant
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10; 11; 12)>
# `is-odd` is a function, so we can simply pass it in as the predicate!
<$odd-numbers = [filter: <numbers>; <is-odd>]>
[join: ,\s; <odd-numbers>]
# -> 1, 3, 5, 7, 9, 11
```

##### Filter a list of words to only those that are 3 letters or less
```rant
<$words = [split: "the quick brown fox jumps over the lazy dog";\s]>
<$short-words = [filter: <words>; [?:word] { [le: [len: <word>]; 3] }]>
[join: \s; <short-words>]
# -> the fox the dog
```

### [index-of: list; element]
&rarr; `int` or `empty`

Returns the index of the first occurrence of `element` in `list`.
If no match is found, returns `~`.

#### Examples

```rant
<$letters = (A; A; B; C; C; D; E)>
[index-of: <letters>; A |> assert-eq: 0]
[index-of: <letters>; C |> assert-eq: 3]
[index-of: <letters>; E |> assert-eq: 6]
[index-of: <letters>; F |> assert-eq: ~]
```

### [join: separator; list]
&rarr; `any*`

Prints the elements of a list in order separated by the `separator` value.

### [last-index-of: list; element]
&rarr; `any`

Returns the index of the last occurrence of `element` in `list`.
If no match is found, returns `~`.

```rant
<$letters = (A; A; B; C; C; D; E)>
[last-index-of: <letters>; A |> assert-eq: 1]
[last-index-of: <letters>; C |> assert-eq: 4]
[last-index-of: <letters>; E |> assert-eq: 6]
[last-index-of: <letters>; F |> assert-eq: ~]
```

### [map: list; map-func]
&rarr; `list`

Applies a function to each item in a list and returns another list with the results in the same order.

The predicate function must accept a single parameter, but can return anything.

#### Example

```rant
# Multiple each element of a list by 10
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10)>
<$tens = [map: <numbers>; [?:x] { [mul: <x>; 10] }]>
[join: ,\s; <tens>]
# -> 10, 20, 30, 40, 50, 60, 70, 80, 90, 100
```

### [oxford-join: comma; conj; comma-conj; list]
&rarr; `any*`

A variant of the `join` function for conveniently formatting comma-separated lists.

Three distinct separator values are required:

* `comma`: the **comma** value, which separates items except for the last two
* `conj`: the **conjunction** value, which is only used to separate items in pairs (lists of 2)
* `comma-conj`: the **comma-conjunction** value, which separates the final two values

These arguments can be used to configure several aspects of list formatting-- namely, the inclusion of 
the [Oxford comma](https://en.wikipedia.org/wiki/Serial_comma) or the choice of conjunction separating the final two items.

The separator values are applied as follows:

* **Lists of 1 item** use no separators.
* **Lists of 2 items** use `conj` to separate the two items.
* **Lists of 3 or more items** separate the final two items with `comma-conj`; all others use `comma`.

#### Examples

##### Print lists with Oxford comma
```rant
<$numbers = ()>
[rep: 5][sep: \n]
{
  [push: <numbers>; [step]]
  [oxford-join: ,\s; \sand\s; ,\sand\s; <numbers>]
}

##
  OUTPUT:

  1
  1 and 2
  1, 2, and 3
  1, 2, 3, and 4
  1, 2, 3, 4, and 5
##
```

##### Print lists without Oxford comma
```rant
<$numbers = ()>
[rep: 5][sep: \n]
{
  [push: <numbers>; [step]]
  [oxford-join: ,\s; \sand\s; \sand\s; <numbers>]
}

##
  OUTPUT:

  1
  1 and 2
  1, 2 and 3
  1, 2, 3 and 4
  1, 2, 3, 4 and 5
##
```

### [push: list; value]

Appends a value to the end of a list.

### [pop: list]
&rarr; `any`

Removes the last value from a list and prints it.

### [insert: collection; value; pos]

Inserts `value` into a list or map at the position `pos`.

If `collection` is a list, `pos` must be an `int`.<br>
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

### [len: obj]
&rarr; `int`

Prints the length of `obj`.

For `string`, this is the number of graphemes; for `list`, `map`, and `range`, the number of elements.
All other value types give a length of 1.

### [remove: collection; pos]

Removes the value at the `pos` from a list or map.

If `collection` is a list, `pos` must be an `int`.<br>
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

### [shuffle: list]

Shuffles the elements of a list in-place.

#### Example

```rant
# Shuffles a list of letters and concatenates them into a single string
<$letters = (A;B;C;D;E;F;G;H;I;J;K;L)>
[shuffle: <letters>]
[join: ; <letters>]

# ~> GKIBCHLEJADF
```

### [shuffled: list]
&rarr; `list`

Creates a shuffled copy of a list.

#### Example

```rant
# Shuffle the words in a string
<$message = "the quick brown fox jumps over he lazy dog">
[join: \s; [shuffled: [split: <message>; \s]]]

# ~> jumps fox quick dog lazy the brown the over
```

### [sift: list; target-size]

Removes random elements from a list in-place until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

#### Example

```rant
# Remove a random element from a list and print the contents at each iteration
<$list = [split: "Sphinx of black quartz, judge my vow."; \s]>
[rep: [len: <list>]]
[sep: \n]
{
  # Print the current list contents
  [join: \s; <list>]
  # Sift the list to n - 1
  [sift: <list>; [sub: [len: <list>]; 1]]
}

##
  EXAMPLE OUTPUT:

  Sphinx of black quartz, judge my vow.
  Sphinx of black quartz, my vow.
  Sphinx of black quartz, vow.
  Sphinx of black vow.
  Sphinx black vow.
  Sphinx vow.
  vow.
##
```

### [sifted: list; target-size]
&rarr; `list`

Returns a copy of a list with random elements removed until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

#### Example

```rant
# Create a random subset of abilities for a character

<$char-traits = (
  berserk;    xray-vision;  speaks-to-bees; 
  vampirism;  flying;       telekinesis; 
  many-legs;  high-jump;    bee-allergy
)>

<$npc = @(
  name = "Foo Bar";
  traits = [sifted: <char-traits>; 2];
)>

# Print character info
<npc/name>: '[join: ,\s; <npc/traits>]

# ~> Foo Bar: speaks-to-bees, many-legs
```

### [squish: list; target-size]

Merges random adjacent elements in a list using addition until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

#### Example

```rant
# Merge random items in a number list
<$numbers = (100; 100; 100; 100; 100; 100; 100; 100; 100; 100)>

# Print the original list
Before: '[join: ,\s; <numbers>]\n

# Squish the list down to 5 elements
[squish: <numbers>; 5]

# Print the modified list
After: '[join: ,\s; <numbers>]\n

##
  EXAMPLE OUTPUT:

  Before: 100, 100, 100, 100, 100, 100, 100, 100, 100, 100
  After: 100, 200, 100, 400, 200
##
```

### [squished: list; target-size]
&rarr; `list`

Returns a copy of a list with random adjacent elements merged using addition until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

### [sort: list]

Sorts the elements of a list in-place in ascending order.

### [sorted: list]
&rarr; `list`

Creates a copy of a list with its elements sorted in ascending order.

### [sum: list]
&rarr; `any`

Adds the elements of a list together from left to right and prints the result.

### [take: collection; pos]
&rarr; `any`

Removes the value at `pos` from a list or map and prints it.

If `collection` is a `list`, `pos` must be an `int`.<br>
If `collection` is a `map`, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

#### Errors

Causes a runtime error if `collection` is a list and the `pos` is out of range.

### [translate: list; map]
&rarr; `list`

Matches each item in a list to a map and returns a list with the corresponding map values. 
Values that have no corresponding key in the map are passed through as-is.

#### Example

```rant
# Constructs a substitution cipher function
[$make-cipher: alphabet] {
  <
    $letters = [split: <alphabet>];
    $sub-letters = [shuffled: <letters>];
    $cipher = [assoc: <letters>; <sub-letters>];
    $cipher-rev = [assoc: <sub-letters>; <letters>];
  >
  # Return cipher functions
  @(
    encode = [?: message] {
      [sum: [translate: [split: <message>]; <cipher>]]
    };
    decode = [?: message] {
      [sum: [translate: [split: <message>]; <cipher-rev>]]
    };
  )
}

# Create a cipher and encode/decode a message
<$cipher = [make-cipher: "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"]>
<$secret-message = "The quick brown fox jumps over the lazy dog.">
<$encoded-message = [cipher/encode: <secret-message>]>
<$decoded-message = [cipher/decode: <encoded-message>]>

# Finally, print the result
Original: \"<secret-message>\"\n
Encoded: \"<encoded-message>\"\n
Decoded: \"<decoded-message>\"\n

##
  EXAMPLE OUTPUT:

  Original: "The quick brown fox jumps over the lazy dog."
  Encoded: "kWj KGvaF QcDiq HDx CGpMJ DOjc AWj Tsyt fDN."
  Decoded: "The quick brown fox jumps over the lazy dog."
##
```

### [zip: list-a; list-b; zip-func]
&rarr; `list`

Returns a new list that combines each pair of items from the two input lists using the specified function.
The lists do not need to be the same length; if there is a difference, it will be made up with empty values.

The `zip-func` must accept two parameters.

#### Examples

```rant
# Dot product
[$dot: a; b] {
  [zip: <a>; <b>; <mul> |> sum]
}

[dot: (1; 2; 3); (4; 5; 6)] # 32
```