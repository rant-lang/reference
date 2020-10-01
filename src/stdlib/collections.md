# Standard Library: Collection functions

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

### [shuffled: list]

Creates a shuffled copy of a list.

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