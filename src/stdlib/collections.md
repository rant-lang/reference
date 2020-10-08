# Standard Library: Collection functions

### [assoc: keys; values]

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

### [join: separator; list]

Prints the elements of a list in order separated by the `separator` value.

### [min: list]

Prints the smallest value of a list.

### [max: list]

Prints the largest value of a list.

### [push: list; value]

Appends a value to the end of a list.

### [pop: list]

Removes the last value from a list and prints it.

### [insert: collection; value; pos]

Inserts `value` into a list or map at the position `pos`.

If `collection` is a list, `pos` must be an integer.<br>
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

### [len: obj]

Prints the length of `obj` as an integer.

For strings, this is the number of bytes; for lists and maps, this is the number of elements.
All other value types give a length of 0.

### [remove: collection; pos]

Removes the value at the `pos` from a list or map.

If `collection` is a list, `pos` must be an integer.<br>
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

[shuffle:<letters>]
[join:;<letters>]
# ~> GKIBCHLEJADF
```

### [shuffled: list]

Creates a shuffled copy of a list.

### [sift: list; target-size]

Removes random elements from a list in-place until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

### [sifted: list; target-size]

Returns a copy of a list with random elements removed until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

### [squish: list; target-size]

Merges random adjacent elements in a list using addition until the number of elements in the list reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function does nothing.

### [squished: list; target-size]

Returns a copy of a list with random adjacent elements merged using addition until the number of elements in the list copy reaches `target-size`.
If the number of elements in the list is less than or equal to `target-size`, this function simply returns an exact copy of the original list.

### [sort: list]

Sorts the elements of a list in-place in ascending order.

### [sorted: list]

Creates a copy of a list with its elements sorted in ascending order.

### [sum: list]

Adds the elements of a list together from left to right and prints the result.

### [take: collection; pos]

Removes the value at `pos` from a list or map and prints it.

If `collection` is a list, `pos` must be an integer.<br>
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

#### Errors

Causes a runtime error if `collection` is a list and the `pos` is out of range.

### [translate: list; map]

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

