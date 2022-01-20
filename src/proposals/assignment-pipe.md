# Assignment pipe

{{ #include _proposal_msg.md }}

Quite often we may want to call a function and store its return value in a variable. This requires an accessor.

What if we could set the variable inside the function call? The **assignment pipe** operator makes this possible.

## Syntax

The assignment pipe is another pipe operator. It must appear at the end of the call chain.
It is followed by a variable or other destination.

```rant
# With setter
<$n = [rand: 1; 100]>

# With assignment pipe
[rand: 1; 100 > $n]
```

When a function call has an assignment pipe, the call does not print anything and is automatically sinked by the compiler.