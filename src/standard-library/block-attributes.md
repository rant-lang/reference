# Block attributes

### [af-push]

Pushes a new attribute frame onto the attribute frame stack, overriding the previous one.

### [af-pop]

Removes the topmost attribute frame from the attribute frame stack, handing control back to the previous one.

#### Errors

Popping the last attribute frame results in a runtime error.

### [af-count]

Prints the current size of the attribute frame stack.

### [mksel: selector-type]

Creates and returns a selector of the specified type.

### Selector types

|Type name      |Description                                                                  |
|---------------|-----------------------------------------------------------------------------|
|`one`          |Selects the same, random element each time.                                  |
|`forward`      |Selects each element in a wrapping sequence from left to right.              |
|`reverse`      |Selects each element in a wrapping reverse sequence from right to left.      |
|`deck`         |Selects each element once in a random sequence, then reshuffles.             |
|`deck-loop`    |Selects each element once in a wrapping random sequence, without reshuffling.|
|`deck-clamp`   |Selects each element once in a random sequence, repeating the final element. |
|`forward-clamp`|Selects each element from left to right, then repeats the right-most element.|
|`reverse-clamp`|Selects each element from right to left, then repeats the left-most element. |
|`no-double`    |Ensures that no one element index is selected twice in a row.                |

### [rep: reps]

Sets the repetition count for the next block to `reps`.
The value of `reps` must be non-negative.

#### Example

```rant
# Print the fragment 3 times
[r:3]{ha}
# hahaha

# Print the fragment between 3 and 8 times
[r:[n:3;8]]{ha}
# hahahaha
# hahahahahahaha
# hahaha
# hahahahaha
# ...
```

### [sel: selector]

Sets the selector for the next block.

### [sep: separator]

Sets the separator value for the next block to `separator`.
The value of `separator` may be a string, number, or function.
If it is a function, it will be called separately for each usage and its return value will be printed.
