# Standard Library: General functions

## alt

```rant

[%alt: a; b+]

```
&rarr; `any` or `empty`

Prints the first argument that isn't the empty value `~`. If all arguments are `~`, prints `~`.

### Parameters

**`a`** &larr; `any` <br/>
The first value to check.

**`b`** &larr; `any+` <br/>
The rest of the values to check.


## call

```rant

[%call: func; args]

```
&rarr; `any` or `empty`

Calls the function `func` with the argument list `args`.

### Parameters

**`func`** &larr; `function` <br/>
The function to call.

**`args`** &larr; `list` <br/>
The arguments to pass to the function.


## cat

```rant

[%cat: values*]

```
&rarr; `any*`

Prints the provided arguments in order.

### Parameters

**`values`** &larr; `any*` <br/>
The values to print.


## copy

```rant

[%copy: value]

```
&rarr; `any`

Returns a shallow clone of `value`.

### Parameters

**`value`** &larr; `any` <br/>
The value to clone.


## either

```rant

[%either: condition; true-val; false-val]

```
&rarr; `any`

Returns `true-val` if `condition` is `@true`, or `false-val` if `condition` is `@false`.

### Parameters

**`condition`** &larr; `bool` <br/>
The boolean value to use to select the output.

**`true-val`** &larr; `any` <br/>
The value to print if `condition` is true.

**`false-val`** &larr; `any` <br/>
The value to print if `condition` is false.

## irange

```rant

[%irange: a; b?; step?]

```
&rarr; `range`

Creates a new **inclusive** `range` with the specified bounds and step value.

* If `a` and `b` are present, range will start at `a` (inclusive) and end at `b` (inclusive).
* If `a` is present but `b` is omitted, range will start at 0 (inclusive) and end at `a` (inclusive).

The `step` value determines the spacing of the range values and must be a positive integer. A step value of 0 defaults to 1.

The `step` value does not affect the first value in the range and is only applied on subsequent values.

### Parameters

**`a`** &larr; `int` <br/>
The starting (inclusive) bound. Used as the ending (inclusive) bound if `b` is omitted.

**`b`** &larr; `int` *(optional)* <br/>
The ending (inclusive) bound.

**`step`** &larr; `int` *(optional)* <br/>
The absolute difference between adjacent values in the range.

## fork

```rant

[%fork: seed?]

```

Forks (overrides) the current RNG with a new RNG seeded by both the old RNG's seed and the specified seed.
If no seed is provided, a random one is generated.

### Parameters

**`seed`** &larr; `int | string` *(optional)* <br/>
The seed value to branch with.


### Example

```rant
# Entangles {yee|woo} with {haw|hoo}, i.e. forces them both to pick the same index

[fork:a]{yee|woo}[unfork]-
[fork:a]{haw|hoo}[unfork]!

# Output is either "yee-haw!" or "woo-hoo!"
```

## nop

```rant

[%nop: args*]

```

Does absolutely nothing. Intended as a convenience function for use as a default/placeholder callback.

### Parameters

**`args`** &larr; `any*` <br/>
The arguments to unceremoniously toss into a bottomless void, never to be seen again.


## range

```rant

[%range: a; b?; step?]

```
&rarr; `range`

Creates a new **exclusive** `range` with the specified bounds and step value.

* If `a` and `b` are present, range will start at `a` (inclusive) and end at `b` (exclusive).
* If `a` is present but `b` is omitted, range will start at 0 (inclusive) and end at `a` (exclusive).

The `step` value determines the spacing of the range values and must be a positive integer. A step value of 0 defaults to 1.

The `step` value does not affect the first value in the range and is only applied on subsequent values.

### Parameters

**`a`** &larr; `int` <br/>
The starting (inclusive) bound. Used as the ending (exclusive) bound if `b` is omitted.

**`b`** &larr; `int` *(optional)* <br/>
The ending (exclusive) bound.

**`step`** &larr; `int` *(optional)* <br/>
The absolute difference between adjacent values in the range.

## require

```rant

[%require: module-path]

```

Imports the module at the specified relative path and assigns it to a local variable with a name matching the file name.

Rant requires module files to have the `.rant` extension in order to load them; as such, it is not necessary to supply the file extension in the path.

### Parameters

**`module-path`** &larr; `string` <br/>
The path to the module to load.

### Example

```rant
# Import module `my-module`
[require: my-module]

# Call `hello-world` function in `my-module`
[my-module/hello-world]
```

## resolve

```rant

[%resolve: block]

```
&rarr; `any` or `empty`

Resolves the specified block.

### Parameters

**`block`** &larr; `block` <br/>
The block to resolve.

## seed

```rant

[%seed]

```
&rarr; `int`

Prints the seed value of the currently active runtime RNG.

## type

```rant

[%type: value]

```
&rarr; `string`

Returns the name of `value`'s type. The type name can be any of the following:

* `string`
* `float`
* `int`
* `bool`
* `function`
* `list`
* `map`
* `special`
* `empty`

### Parameters

**`value`** &larr; `any` <br/>
The value whose type name to retrieve.


## unfork

```rant

[%unfork]

```

Removes the last RNG created by `[fork]` and resumes use of the previous RNG.