# Block attributes

### [r: reps]

Sets the repetition count (`__BATTRS/reps`) for the next block to `reps`.
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

### [s: sep]

Sets the separator value (`__BATTRS/sep`) for the next block to `sep`.
The value of `sep` may be a string, number, or function.
If it is a function, it will be called separately for each usage and its return value will be printed.