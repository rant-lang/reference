# Standard Library: Attributes & Control flow

### [count-attrs]
&rarr; `int`

Prints the current size of the attribute frame stack.

### [else]

Marks the next block as conditional and causes it to resolve iff the last block was conditional and its condition evaluated to false.

### [else-if: condition]

Marks the next block as conditional and causes it to resolve iff the following are true:
* `condition` is true
* The last block was conditional and its condition evaluated to false

### [if: condition]

Marks the next block as conditional and causes it to resolve iff `condition` is true.

### [mksel: selector-mode]
&rarr; `special`

Creates and returns a selector with the specified mode.

### Selector modes

|Mode name      |Description                                                                                |
|---------------|-------------------------------------------------------------------------------------------|
|`random`       |Selects a random element each time.                                                        |
|`one`          |Selects the same, random element each time.                                                |
|`forward`      |Selects in a wrapping sequence from first to last.                                         |
|`reverse`      |Selects in a wrapping reverse sequence from last to first.                                 |
|`deck`         |Selects each element once in a random sequence, then reshuffles.                           |
|`deck-loop`    |Selects each element once in a wrapping random sequence, without reshuffling.              |
|`deck-clamp`   |Selects each element once in a random sequence, repeating the final element.               |
|`forward-clamp`|Selects from first to last, then repeats the last element.                                 |
|`reverse-clamp`|Selects from last to first, then repeats the first element.                                |
|`ping`         |Selects from first to last, switching directions when a boundary is reached.               |
|`pong`         |Selects from last to first, switching directions when a boundary is reached.               |
|`no-double`    |Selects a random element each time, ensuring the same element never repeats twice in a row.|

### [pipe: pipe-func]

Sets the pipe function for the next block.

The function passed to `pipe-func` must accept a single parameter (the element callback) in order to run properly.

### [push-attrs]

Pushes a new attribute frame onto the attribute frame stack, overriding the previous one.

### [pop-attrs]

Removes the topmost attribute frame from the attribute frame stack, handing control back to the previous one.

#### Errors

Popping the last attribute frame results in a runtime error.

### [rep: reps]

Sets the repetition count for the next block to `reps`.
The value of `reps` must either be a non-negative `int` or one of the special modes listed below.

### Special rep modes

|Mode name      |Description                                                                        |
|---------------|-----------------------------------------------------------------------------------|
|`once`         |Run the block only once. (default behavior)                                        |
|`forever`      |Repeat the next block until explicitly stopped.                                    |
|`all`          |Repeat as many times as there are elements in the  next block.                     |

#### Examples

```rant
# Print the fragment 3 times
[rep:3]{ha}
# hahaha
```

```rant
# Print the fragment between 3 and 8 times
[rep:[num:3;8]]{ha}
# hahahaha
# hahahahahahaha
# hahaha
# hahahahaha
# ...
```

### [sel: selector]

Sets the selector for the next block. 

The `selector` parameter can accept either a selector state object created via `[mksel]`, or a selector mode string (see `[mksel]` documentation for available modes).

#### Examples

```rant
# Pass in an existing selector object so its state persists between uses
<%fwd = [mksel:forward]>
[sel:<fwd>]
[rep:all]
[sep:\s]
{
  A | B | C | D
}
```

```rant
# Create a temporary selector using [mksel]
[sel:[mksel:forward]]
[rep:all]
[sep:\s]
{
  A | B | C | D
}
```

```rant
# Automatically create a temporary selector from a mode name
[sel:forward]
[rep:all]
[sep:\s]
{
  A | B | C | D
}
```

### [sep: separator]

Sets the separator value for the next block to `separator`.
The value of `separator` may be a string, number, or function.
If it is a function, it will be called separately for each usage and its return value will be printed.

#### Examples

```rant
# Print comma-separated list of numbers 1-10
[rep:10][sep:,\s]{[step]}

##
  Output:
  1, 2, 3, 4, 5, 6, 7, 8, 9, 10
##
```

```rant
# Print list of numbers 1-10 separated by random sequence of spaces and newlines
[rep:10][sep:*{\n|\s}]{[step]}

##
  Output:
  1 2 3
  4 5 6 7 8
  9
  10
##
```