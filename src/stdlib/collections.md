# Standard Library: Collection functions

## assoc

```rant

[%assoc: keys; values]

```
&rarr; `map`

Creates a map from a list of keys and a list of values.
Each key in `keys` will be matched with the value at the same index in `values`.

### Parameters

**`keys`** &larr; `list` <br/>
The keys to store in the map.

**`values`** &larr; `list` <br/>
The values to associate with the keys.

### Errors

Raises a runtime error if the lengths of `keys` and `values` do not match.

### Example

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


## clear

```rant

[%clear: collection]

```

Removes all elements from a list or map.

### Parameters

**`collection`** &larr; `list | map` <br/>
The collection to clear.

### Errors

Causes a runtime error if `collection` is not a list or map.


## collect

```rant

[%collect: values*]

```
&rarr; `list`

Prints a `list` containing the arguments.

### Parameters

**`values`** &larr; `any*` <br/>
The values to store in the list.


## filter

```rant

[%filter: list; predicate]

```
&rarr; `list`

Runs a predicate function against all items in a list and returns another list containing only the values that the predicate returned `@true` on.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`predicate`** &larr; `function -> bool` <br/>
The predicate to run against each element in the input list.

> **Parameters for `predicate`**
>
> **`item`** &larr; `any` <br/>
> The current item to be checked.

### Examples

#### Filter a list of numbers by only those divisible by 3
```rant
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10; 11; 12)>
<$multiples-of-three = [filter: <numbers>; [?:x] { [is-factor: <x>; 3] }]>
[join: <multiples-of-three>; ,\s]
# -> 3, 6, 9, 12
```

#### Filter a list of numbers by only odd numbers
```rant
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10; 11; 12)>
# `is-odd` is a function, so we can simply pass it in as the predicate!
<$odd-numbers = [filter: <numbers>; <is-odd>]>
[join: <odd-numbers>; ,\s]
# -> 1, 3, 5, 7, 9, 11
```

#### Filter a list of words to only those that are 3 letters or less
```rant
<$words = [split: "the quick brown fox jumps over the lazy dog";\s]>
<$short-words = [filter: <words>; [?:word] { [le: [len: <word>]; 3] }]>
[join: <short-words>; ,\s]
# -> the fox the dog
```


## index-of

```rant

[%index-of: list; value]

```
&rarr; `int | empty`

Returns the index of the first occurrence of `value` in `list`.
If no match is found, returns `<>`.

### Parameters

**`list`** &larr; `list` <br/>
The list to search.

**`value`** &larr; `any` <br/>
The value to search for.

### Examples

```rant
<$letters = (A; A; B; C; C; D; E)>
[index-of: <letters>; A |> assert-eq: 0]
[index-of: <letters>; C |> assert-eq: 3]
[index-of: <letters>; E |> assert-eq: 6]
[index-of: <letters>; F |> assert-eq: <>]
```


## join

```rant

[%join: list; separator?]

```
&rarr; `any*`

Prints the elements of a list in order separated by the `separator` value.

### Parameters

**`list`** &larr; `list` <br/>
The list whose elements to print.

**`separator`** &larr; `any` *(optional)* <br/>
The separator to print between each element.


## last-index-of

```rant

[%last-index-of: list; value]

```
&rarr; `any`

Returns the index of the last occurrence of `value` in `list`.
If no match is found, returns `<>`.

### Parameters

**`list`** &larr; `list` <br/>
The list to search.

**`value`** &larr; `any` <br/>
The value to search for.

### Example

```rant
<$letters = (A; A; B; C; C; D; E)>
[last-index-of: <letters>; A |> assert-eq: 1]
[last-index-of: <letters>; C |> assert-eq: 4]
[last-index-of: <letters>; E |> assert-eq: 6]
[last-index-of: <letters>; F |> assert-eq: <>]
```


## map

```rant

[%map: list; map-func]

```
&rarr; `list`

Calls the supplied function on each item in a list and returns another list with the results in the same order.

### Parameters

**`list`** &larr; `list` <br/>
The list whose values to map.

**`map-func`** &larr; `function -> any` <br/>
The function to map the values with.

> **Parameters for `map-func`** <p>
> 
> **`item`** &larr; `any` <br/>
> The current item to map.

### Example

```rant
# Multiple each element of a list by 10
<$numbers = (1; 2; 3; 4; 5; 6; 7; 8; 9; 10)>
<$tens = [map: <numbers>; [?:x] { [mul: <x>; 10] }]>
[join: ,\s; <tens>]
# -> 10, 20, 30, 40, 50, 60, 70, 80, 90, 100
```


## oxford-join

```rant

[%oxford-join: comma; conj; comma-conj; list]

```
&rarr; `any*`

A variant of the `join` function for conveniently formatting comma-separated lists.

### Parameters

**`comma`** &larr; `any` <br/>
The **comma** value. Separates all items except for the last 2. Unused in lists of 2 items or less.

**`conj`** &larr; `any` <br/>
The **conjunction** value. Only used to separate items in lists of exactly 2 values.

**`comma-conj`** &larr; `any` <br/>
The **comma-conjunction** value. Separates the final 2 values in lists with more than 2 values.

### Remarks

These arguments can be used to configure several aspects of list formatting-- namely, the inclusion of 
the [Oxford comma](https://en.wikipedia.org/wiki/Serial_comma) or the choice of conjunction separating the final two items.

The separator values are applied as follows:

* **Lists of 1 item** use no separators.
* **Lists of 2 items** use `conj` to separate the two items.
* **Lists of 3 or more items** separate the final two items with `comma-conj`; all others use `comma`.

### Examples

#### Print lists with Oxford comma
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

#### Print lists without Oxford comma
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


## push

```rant

[%push: list; value]

```

Appends a value to the end of a list.

### Parameters

**`list`** &larr; `list` <br/>
The list to modify.

**`value`** &larr; `any` <br/>
The value to add to the end of `list`.


## pop

```rant

[%pop: list]

```
&rarr; `any`

Removes the last value from a list and prints it.

### Parameters

**`list`** &larr; `list` <br/>
The list to modify.


## insert

```rant

[%insert: collection; value; pos]

```

Inserts `value` into a list or map at the position `pos`.

If `collection` is a list, `pos` must be an `int`.<br>
If `collection` is a map, `pos` may be any non-empty value.

### Parameters

**`collection`** &larr; `list | map` <br/>
The collection to modify.

**`value`** &larr; `any` <br/>
The value to add to `collection`.

**`pos`** &larr; `some` <br/>
The location at which to insert the value. <br/>
For lists, this is the index; for maps, this is the key.

### Errors

Raises an error if `pos` is out of range or not the correct type for the provided collection.


## len

```rant

[%len: value]

```
&rarr; `int`

Prints the length of `value`.

For `string`, this is the number of graphemes; for `list`, `map`, and `range`, the number of elements.
All other value types give a length of 1.

### Parameters

**`value`** &larr; `any` <br/>
The value whose length to retrieve.


## remove

```rant

[%remove: collection; pos]

```

Removes the value at the `pos` from a list or map.

If `collection` is a list, `pos` must be an `int`.<br>
If `collection` is a map, `pos` may be any non-empty value.

### Parameters

**`collection`** &larr; `list | map` <br/>
The collection to modify.

**`pos`** &larr; `some` <br/>
The location of the value to remove. Must be of type `int` for lists.

### Errors

Raises an error if `pos` is an unsupported type for the provided collection.


## rev

```rant

[%rev: collection]

```
&rarr; `list | string | block | range`

Prints a reversed copy of the input collection.

### Parameters

**`collection`** &larr; `list | string | block | range` <br/>
The collection to reverse.

### Example

```rant
[rev: (foo; bar)]
# -> (bar; foo)
```


## shuffle

```rant

[%shuffle: list]

```

Shuffles the elements of a list in-place.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

### Cost

Where \\(n\\) = the length of `list`:

**Time complexity**<br/>\\(O(n)\\)<br/>

**RNG complexity**<br/>\\(n - 1\\)<br/>

### Example

```rant
# Shuffles a list of letters and concatenates them into a single string
<$letters = (A;B;C;D;E;F;G;H;I;J;K;L)>
[shuffle: <letters>]
[join: <letters>]

# ~> GKIBCHLEJADF
```


## shuffled

```rant

[%shuffled: list]

```
&rarr; `list`

Creates a shuffled copy of a list.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

### Example

```rant
# Shuffle the words in a string
<$message = "the quick brown fox jumps over he lazy dog">
[join: \s; [shuffled: [split: <message>; \s]]]

# ~> jumps fox quick dog lazy the brown the over
```


## sift

```rant

[%sift: list; target-size]

```

Removes random elements from a list in-place until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`target-size`** &larr; `int` <br/>
The maximum number of elements to reduce the `list` to.

### Example

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


## sifted

```rant

[%sifted: list; target-size]

```
&rarr; `list`

Returns a copy of a list with random elements removed until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`target-size`** &larr; `int` <br/>
The maximum number of elements to reduce the `list` to.

### Example

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
<npc/name>: `[join: ,\s; <npc/traits>]

# ~> Foo Bar: speaks-to-bees, many-legs
```


## squish

```rant

[%squish: list; target-size]

```

Merges random adjacent elements in a list using addition until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`target-size`** &larr; `int` <br/>
The maximum number of elements to reduce the list to.

### Example

```rant
# Merge random items in a number list
<$numbers = (100; 100; 100; 100; 100; 100; 100; 100; 100; 100)>

# Print the original list
Before: `[join: ,\s; <numbers>]\n

# Squish the list down to 5 elements
[squish: <numbers>; 5]

# Print the modified list
After: `[join: ,\s; <numbers>]\n

##
  EXAMPLE OUTPUT:

  Before: 100, 100, 100, 100, 100, 100, 100, 100, 100, 100
  After: 100, 200, 100, 400, 200
##
```


## squished

```rant

[%squished: list; target-size]

```
&rarr; `list`

Returns a copy of a list with random adjacent elements merged using addition until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`target-size`** &larr; `int` <br/>
The maximum number of elements to reduce the list copy to.


## sort

```rant

[%sort: list]

```

Sorts the elements of a list in-place in ascending order.

### Parameters

**`list`** &larr; `list` <br/>
The input list.


## sorted

```rant

[%sorted: list]

```
&rarr; `list`

Creates a copy of a list with its elements sorted in ascending order.

### Parameters

**`list`** &larr; `list` <br/>
The input list.


## sum

```rant

[%sum: list]

```
&rarr; `any`

Adds the elements of a list together from left to right and prints the result.


## take

```rant

[%take: collection; pos]

```
&rarr; `any`

Removes the value at `pos` from a list or map and prints it.

### Parameters

**`collection`** &larr; `list | map` <br/>
The input collection.

**`pos`** &larr; `some` <br/>
The location of the value to take. 
If `collection` is a `list`, this argument must be an `int`.

### Errors

Raises an error if `pos` is not a valid location in the collection.


## translate

```rant

[%translate: list; map]

```
&rarr; `list`

Matches each item in a list to a map and returns a list with the corresponding map values. 
Values that have no corresponding key in the map are passed through as-is.

### Parameters

**`list`** &larr; `list` <br/>
The input list.

**`map`** &larr; `map` <br/>
A map associating items in `list` with their replacements.

### Example

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


## zip

```rant

[%zip: list-a; list-b; zip-func]

```
&rarr; `list`

Returns a new list that combines each pair of items from the two input lists using the specified function.
The lists do not need to be the same length; if there is a difference, it will be made up with empties.

### Parameters

**`list-a`** &larr; `list` <br/>
A list containing the left-hand values of the zip.

**`list-b`** &larr; `list` <br/>
A list containing the right-hand values of the zip.

**`zip-func`** &larr; `function -> any` <br/>
A function that prints a new value for each corresponding pair of values from `list-a` and `list-b`.
> **Parameters for `zip-func`**
>
> **`a`** &larr; `any` <br/>
> The current value from `list-a`.
>
> **`b`** &larr; `any` <br/>
> The current value from `list-b`.


### Examples

```rant
# Dot product
[$dot: a; b] {
  [zip: <a>; <b>; <mul> |> sum]
}

[dot: (1; 2; 3); (4; 5; 6)] # 32
```