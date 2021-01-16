# Attributes

**Attributes** are special runtime settings that modify block behavior, such as how many times a block repeats or how it selects which element to run.

Attributes are set by calling the standard library's **attribute functions** and stored in the program's **attribute stack**.
Each frame of the attribute stack stores a full set of attributes.

When a block resolves, it consumes attributes from the topmost attribute frame and replaces them with their default values.

Frames can be added to and removed from the attribute stack using `[push-attrs]` and `[pop-attrs]`.

## Repetitions

By setting the repetitions attribute, you can control how many times the next encountered block will run.
This attribute is set with the `[rep]` function.

### Example

```rant
[rep:10]{[step]\n}
# Output:
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
```

## Separator

The separator attribute controls what is printed between each block repetition.
It is set using the `[sep]` function.

### Example

```rant
[rep:4][sep:" and "]
It just keeps {going}...

# Output:
# It just keeps going and going and going and going...
```

## Selector

The selector attribute controls how Rant chooses which branch of a block to take. It does this using a special state machine object, which must be created separately but can be shared between blocks to coordinate their behavior.

### Example

```rant
# Print every element of the block in a random order with no duplicates

<$s=[mksel:deck]>  # Create a "deck" selector
[sel:<s>]          # Apply the selector
[rep:all]          # Set repetitions
[sep:,\s]          # Set separator
{A|B|C|D|E|F|G|H}

# Output
# F, C, E, G, B, H, D, A
```

## Pipe

The pipe attribute allows the user to supply a function (known as the "pipe function") that is called in place of each iteration of the block.
The pipe function accepts the current block element as a callback parameter, which it can then call to produce output for that iteration.

This is extremely useful for applying filters or post-processing to a block at a per-iteration level.

```rant
[rep: all]
[sep: \n]
[pipe: [?:elem] { [elem]! }] # Just adds an exclamation point
[mksel: forward & sel]
{
    One | Two | Three | Four | Five | Six | Seven | Eight | Nine | Ten
}
```