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
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

### [remove: collection; pos]

Removes the value at the `pos` from a list or map.

If `collection` is a list, `pos` must be an integer.<br>
If `collection` is a map, `pos` may be any non-empty value.

#### Errors

Causes a runtime error if any of the following are true:
* `collection` is not a list or map
* `pos` is an unsupported type for the provided collection
* `collection` is a list and `pos` is out of range

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

### [clear: collection]

Removes all elements from a list or map.

#### Errors

Causes a runtime error if `collection` is not a list or map.

### [len: obj]

Prints the length of `obj` as an integer.

For strings, this is the number of bytes; for lists and maps, this is the number of elements.
All other value types give a length of 0.