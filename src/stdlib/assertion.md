# Assertion

### [assert: condition; message?]

Asserts that `condition` is true.

If `condition` is `false`, raises a runtime error; if `true`, does nothing.

The message displayed in the runtime error can be customized by passing a string to `message`. 

#### Examples

```rant
# does absolutely nothing
[assert: true]

# [assertion error] assertion failed: condition was false
[assert: false]

# [assertion error] ooooops!
[assert: false; "ooooops!"] 
```

### [assert-eq: actual; expected; message?]

Asserts that `expected` and `actual` are equal.

Like `[assert]`, a custom error message can be provided.

### [assert-neq: actual; unexpected; message?]

Asserts that `unexpected` and `actual` are not equal.

Like `[assert]`, a custom error message can be provided.