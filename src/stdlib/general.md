# Standard Library: General functions

### [alt: a; b+]
&rarr; `any` or `empty`

Prints the first argument that isn't the empty value `~`. If all arguments are `~`, prints `~`.

### [call: func; args]
&rarr; `any` or `empty`

Calls the function `func` with the argument list `args`.

#### Errors

Causes a runtime error if either of the following are true:
* `func` isn't a function
* `args` isn't a list

### [copy: value]
&rarr; `any`

Returns a shallow clone of `value`.

### [either: condition; true-val; false-val]
&rarr; `any`

Returns `true-val` if `condition` is `true`, or `false-val` if `condition` is `false`.

`condition` must be of type `bool`.

### [fork: seed?]

Forks (overrides) the current RNG with a new RNG seeded by both the old RNG's seed and the specified seed.
If no seed is provided, a random one is generated.

The seed value must be an `integer` or `string`.

#### Errors

Causes a runtime error if `seed` is neither an `integer` nor `string`.

#### Example

```rant
# Entangles {yee|woo} with {haw|hoo}, i.e. forces them both to pick the same index

[fork:a]{yee|woo}[unfork]-
[fork:a]{haw|hoo}[unfork]!

# Output is either "yee-haw!" or "woo-hoo!"
```

### [nop: args*]

Does absolutely nothing. Intended as a convenience function for use as a default/placeholder callback.

### [require: module-path]

Imports the module at the specified relative path and assigns it to a local variable with a name matching the file name.

Rant requires module files to have the `.rant` extension in order to load them; as such, it is not necessary to supply the file extension in the path.

#### Example

```rant
# Import module `my-module`
[require: my-module]

# Call `hello-world` function in `my-module`
[my-module/hello-world]
```

### [resolve: block]
&rarr; `any` or `empty`

Resolves the specified block.

#### Errors

Causes a runtime error if the provided value is not a block.

### [seed]
&rarr; `integer`

Returns the seed value that the program was run with.

### [type: value]
&rarr; `string`

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

### [unfork]

Removes the last RNG created by `[fork]` and resumes use of the previous RNG.