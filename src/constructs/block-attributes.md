# Block attributes

**Block attributes** are a set of constructs that control various aspects of block behavior.
There are several block attributes available that the user can set via the standard library.

## Repetitions

By setting the repetitions attribute, you can control how many times the next encountered block will run.
This attribute is set with the `[rep]` function.

### Example

```rant
[rep:10]
{ [rep-n]\n }
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

The selector attribute controls how Rant chooses which branch of the block to take. A selector can be reused for several blocks to coordinate their behavior.

Selectors require slightly more setup, as they are actually persistent state machines that must be created with a separate function before use.
They must be assigned a name, which is then used to refer to it when applying it to blocks.

In most cases, selector states are considered global objects. However, you can limit their scope using **attribute frames**, discussed later.

### Example

```rant
# Print every element of the block in a random order with no duplicates

[mksel:a;deck]  # Create a "deck" selector
[sel:a]         # Apply the selector
[rep-each]      # Set repetitions
[sep:,\s]       # Set separator
{A|B|C|D|E|F|G|H}

# Output
# F, C, E, G, B, H, D, A
```

## Attribute frames

The Rant runtime maintains a stack of "attribute frames", which store block attributes.
The resolver always reads attributes from the topmost frame in the attribute frame stack. 
This stack can be used to limit the scope of block attributes.

The attribute frame stack can be accessed with the `[af-*]` class of functions.