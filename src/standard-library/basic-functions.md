# Basic functions

### [alt: a; b+]

Prints the first argument that isn't the empty value `<>`.

### [call: func; args]

Calls the function `func` with the argument list `args`.

#### Errors

Causes a runtime error if either of the following are true:
* `func` isn't a function
* `args` isn't a list

### [seed]

Returns the seed value that the program was run with.

### [type: value]

Returns the name of `value`'s type. The type name can be any of the following:

* `string`
* `float`
* `integer`
* `bool`
* `function`
* `list`
* `map`
* `special`
* `empty`

### [return: value]

Immediately exits the current scope and returns `value` to the caller instead of the current output.

If `[return]` is called without an argument, the output from the function will be returned instead.