# @return

The `@return` charm exits the currently running function and optionally overwrites the function's output with another value.

When `@return` is used without any expression to its right, it returns the current output:
```rant
[%return-output] {
    {foo @return} bar
}

[return-output] # -> foo
```
When an expression comes after `@return` in the same scope, only the value of that expression is returned:
```rant
[%return-value] {
    foo @return bar
}

[return-value] # -> bar
```

Additionally, you can also return from the program scope itself:

```rant
@return foo # -> foo
```