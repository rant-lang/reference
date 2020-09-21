# Standard Library: General functions

### [alt: a; b+]

Prints the first argument that isn't the empty value `<>`.

### [call: func; args]

Calls the function `func` with the argument list `args`.

#### Errors

Causes a runtime error if either of the following are true:
* `func` isn't a function
* `args` isn't a list

### [nop: args*]

Does absolutely nothing. Intended as a convenience function for use as a default/placeholder callback.

### [require: module-name]

Imports the module with the specified name.

### [resolve: block]

Resolves the specified block.

#### Errors

Causes a runtime error if the provided value is not a block.

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