# The `range` type

The `range` type represents a closed range of integers characterized by three values:

1. an inclusive **start** bound,
2. an exclusive **end** bound,
3. the **interval** between values in the range.

As such, very large ranges can be stored, indexed, and enumerated without needing to pre-allocate all possible values in memory.

Ranges are created with the built-in `[range]` function:

```rant
# Print numbers 0 through 4
[cat: **[range: 0; 5]; \n]

##
  Output:
  0
  1
  2
  3
  4
##
```

Backwards ranges are possible, too; just use a start bound larger than the end bound:

```rant
# Print numbers 4 through 0
[cat: **[range: 4; -1]; \n]

##
  Output:
  4
  3
  2
  1
  0
##
```

By default, `[range]` uses an interval of 1, but you can change this by adding a third argument:

```rant
# Print every second number between 0 and 9
[cat: **[range: 0; 10; 2]; \n]

##
  Output:
  0
  2
  4
  6
  8
##
```