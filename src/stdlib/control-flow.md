# Standard Library: Attributes & Control flow

## copy-attrs

```rant

[%copy-attrs]

```

Pushes a new attribute frame with identical contents to the previous top frame.


## count-attrs

```rant

[%count-attrs]

```
&rarr; `int`

Prints the current size of the attribute frame stack.


## else

```rant

[%else]

```

Marks the next block as conditional and causes it to resolve iff the last block was conditional and its condition evaluated to false.


## else-if

```rant

[%else-if: condition]

```

Marks the next block as conditional and causes it to resolve iff the following are true:
* `condition` is `@true`
* The last block was conditional and its condition evaluated to `@false`

### Parameters

**`condition`** &larr; `bool` <br/>
The condition to check.


## if

```rant

[%if: condition]

```

Marks the next block as conditional and causes it to resolve iff `condition` is `@true`.


## mksel

```rant

[%mksel: selector-mode]

```

&rarr; `special`

Creates and returns a selector with the specified mode.

### Parameters

**`selector-mode`** &larr; `string` <br/>
The mode to assign to the created selector.

### Options for `selector-mode`

{{ #include ../_tables/selector-modes.md }}


## mut

```rant

[%mut: mutator-func]

```

Sets the mutator function for the next block.

The function passed to `mutator-func` must accept a single parameter (the element callback) in order to run properly.

### Parameters

**`mutator-func`** &larr; `function | empty` <br/>
The mutator function to assign.


## push-attrs

```rant

[%push-attrs]

```

Pushes a new attribute frame onto the attribute frame stack, overriding the previous one.


## pop-attrs

```rant

[%pop-attrs]

```

Removes the topmost attribute frame from the attribute frame stack, handing control back to the previous one.


### Errors

Attempting to pop the last attribute frame will raise a runtime error.



## rep

```rant

[%rep: reps]

```

Sets the repetition count for the next block to `reps`.
The value of `reps` must either be a non-negative `int` or one of the special modes listed below.

### Parameters

**`reps`** &larr; `int | string` <br/>
The repetition count or mode to set. If a string, it must match one of the below mode names.

### Mode options for `reps`

|Mode name      |Description                                                                        |
|---------------|-----------------------------------------------------------------------------------|
|`once`         |Run the block only once. (default behavior)                                        |
|`forever`      |Repeat the next block until explicitly stopped.                                    |
|`all`          |Repeat as many times as there are elements in the  next block.                     |

### Examples

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

```rant
# Print a random card from each suit
[rep: all] 
[sel: deck]
[pipe: [?: e] ({A|2|3|4|5|6|7|8|9|J|Q|K}[e])]
{ ♥ | ♣ | ♠ | ♦ }
# ~> (8♣; 2♦; 6♥; Q♠)
```

## sel

```rant

[%sel: selector]

```

Sets the selector for the next block. 

The `selector` parameter can accept either a selector state object created via `[mksel]`, or a selector mode (in which case it will create a single-use selector of that mode).

### Parameters

**`selector`** &larr; `special | string` <br/>
The selector or selector mode to use. 
If it's a `string`, it has to be one of the selector modes accepted by `[mksel]`.

### Examples

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

## sep

```rant

[%sep: separator]

```

Sets the separator value for the next block to `separator`.
The value of `separator` may be of any type.

### Parameters

**`separator`** &larr; `any` <br/>
The separator value. If it is a `function`, it will be called separately for each usage and its return value will be printed.


### Examples

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
[rep:10][sep:[?]{{\n|\s}}]{[step]}

##
  Output:
  1 2 3
  4 5 6 7 8
  9
  10
##
```