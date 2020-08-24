# Collection functions

### [join: separator; list]

Prints the elements of a list in order separated by the `separator` value.

### [push: list; value]

Adds a value to the end of a list.

### [pop: list]

Removes the last value from a list and prints it.

### [insert: collection; value; pos]

Inserts `value` into a list or map at the position `pos`.

If `collection` is a list, `pos` must be an integer.<br>
If `collection` is a map, `pos` may be either an integer or string.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

### [remove: list; index]

Removes the value at the specified index from a list.

### [take: list; index]

Removes the value at the specified index from a list and prints it.

#### Errors

Causes a runtime error if the index is out of range or the `list` is not a list.

### [clear: list]

Removes all elements from a list.

### [len: obj]

Prints the length of `obj` as an integer.

For strings, this is the number of bytes; for lists and maps, this is the number of elements.
All other value types give a length of 0.