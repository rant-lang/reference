# Assertion

## assert

```rant

[%assert: condition; message?]

```

Verifies that `condition` is true before continuing program execution.

If `condition` is `false`, raises a runtime error; if `true`, does nothing.

The message displayed in the runtime error can be customized by passing a string to `message`. 

### Parameters

**`condition`** &larr; `bool` <br/>
The condition to check.

**`message`** &larr; `string` *(optional)* <br/>
The error message to display if the condition is not satisfied.

### Examples

```rant
# does absolutely nothing
[assert: true]

# [assertion error] assertion failed: condition was false
[assert: false]

# [assertion error] ooooops!
[assert: false; "ooooops!"] 
```

## assert-eq

```rant

[%assert-eq: actual; expected; message?]

```

Verifies that `expected` and `actual` are equal before continuing program execution.

Like `[assert]`, a custom error message can be provided.

### Parameters

**`actual`** &larr; `any` <br/>
The actual value to test.

**`expected`** &larr; `any` <br/>
The expected value to test against.

**`message`** &larr; `string` <br/>
The error message to display if the condition is not satisfied.


## assert-neq

```rant

[%assert-neq: actual; unexpected; message?]

```

Verifies that `unexpected` and `actual` are not equal before continuing program execution.

Like `[assert]`, a custom error message can be provided.

### Parameters

**`actual`** &larr; `any` <br/>
The actual value to test.

**`unexpected`** &larr; `any` <br/>
The unexpected value to test against.

**`message`** &larr; `string` <br/>
The error message to display if the condition is not satisfied.