# Standard Library: Formatting functions

## num-fmt

```rant

[%num-fmt: options?; depth?]

```
&rarr; `map | empty`

Gets or sets the number formatting options for the calling scope.

If `options` is not set, prints a map with all current number format options.

### Parameters

**`options`** &larr; `map` *(optional)* <br/>
The options to set. Only overwrites options specified; all others are left unchanged. <br/>
If omitted, the function prints a map containing all current number format options. <br/>
See section below for available options.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).

### Supported keys for `options`

{{ #include ../_tables/num-fmt-options.md }}

### Examples

**Getting the current number format**
```rant
# Print current number format
[num-fmt]
## -> 
@(
    sign = negative-only; 
    infinity = keyword; 
    group-sep = ; 
    endian = big; 
    precision = -1; 
    system = west-arabic; 
    alt = false; 
    padding = 0; 
    upper = false; 
    decimal-sep = ;
)
##
```

**Setting the current number format**
```rant
# Set format to big-endian 64-bit uppercase hex with prefix
[num-fmt: @(system = hex; upper = @true; alt = @true; padding = 16)]

1000000000\n

# -> 0x000000003B9ACA00
```


## num-fmt-system

```rant

[%num-fmt-system: system?; depth?]
```
&rarr; `string | empty`

Gets or sets the number formatter's numeral system.

Shorthand for the `system` option in `[num-fmt]`.

### Parameters

**`system`** &larr; `string` *(optional)* <br/>
The case-insensitive name of the numeral system to use. If omitted, the function prints the current value. <br/>
See section below for available options.


**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).

### Options for `system`

{{ #include ../_tables/num-fmt-system.md }}


## num-fmt-alt

```rant

[%num-fmt-alt: flag?; depth?]

```
&rarr; `bool | empty`

Gets or sets the number formatter's alternate format flag.

Shorthand for the `alt` option in `[num-fmt]`.

### Parameters

**`flag`** &larr; `bool` *(optional)* <br/>
A boolean value indicating whether alternate formatting is enabled.
If omitted, the function prints the current value.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).


## num-fmt-precision

```rant

[%num-fmt-precision: precision?; depth?]

```
&rarr; `int | empty`

Gets or sets the number formatter's decimal precision.

Shorthand for the `precision` option in `[num-fmt]`.

### Parameters

**`precision`** &larr; `int` *(optional)* <br/>
The number of decimal places to pad or truncate numbers to. 
If omitted, the function prints the current value.
Set to -1 to allow unbounded precision.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).


## num-fmt-padding

```rant

[%num-fmt-padding: padding?; depth?]

```
&rarr; `int | empty`

Gets or sets the number formatter's digit padding size.

Shorthand for the `padding` option in `[num-fmt]`.

### Parameters

**`padding`** &larr; `int` *(optional)* <br/>
The padding size to set. If omitted, the function prints the current value.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).


## num-fmt-upper

```rant

[%num-fmt-upper: flag?; depth?]

```
&rarr; `bool | empty`

Gets or sets the number formatter's uppercase formatting flag.

Shorthand for the `upper` option in `[num-fmt]`.

### Parameters

**`flag`** &larr; `bool` *(optional)* <br/>
A boolean value indicating whether uppercase formatting is enabled.
If omitted, the function prints the current value.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).


## num-fmt-sign

```rant

[%num-fmt-sign: sign?; depth?]

```
&rarr; `string | empty`

Gets or sets the number formatter's sign style.

Shorthand for the `sign` option in `[num-fmt]`.

### Parameters

**`sign`** &larr; `string` *(optional)* <br/>
The case-insensitive name of the sign style to use. If omitted, the function prints the current value. <br/>
See section below for available options.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).

### Options for `sign`

{{ #include ../_tables/num-fmt-sign.md }}


## num-fmt-endian

```rant

[%num-fmt-endian: endianness?; depth?]

```
&rarr; `string | empty`

Gets or sets the number format's endianness. This affects the byte order of power-of-two base formats such as `binary` and `hex`.

Shorthand for the `endian` option in `[num-fmt]`.

### Parameters

**`endianness`** &larr; `string` *(optional)* <br/>
The case-insensitive name of the endianness type to use. If omitted, the function prints the current value. <br/>
See section below for available options.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).

### Options for `endianness`

{{ #include ../_tables/num-fmt-endian.md }}

## num-fmt-infinity

```rant

[%num-fmt-infinity: infinity?; depth?]

```
&rarr; `string | empty`

Gets or sets the number formatter's infinity style.

Shorthand for the `infinity` option in `[num-fmt]`.

### Parameters

**`infinity`** &larr; `string` *(optional)* <br/>
The case-insensitive name of the infinity style to use. If omitted, the function prints the current value. <br/>
See section below for available options.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).

### Options for `infinity`

{{ #include ../_tables/num-fmt-infinity.md }}


## num-fmt-group-sep

```rant

[%num-fmt-group-sep: group-sep?; depth?]

```
&rarr; `string | empty`

Gets or sets the number formatter's digit group separator.

Shorthand for the `group-sep` option in `[num-fmt]`.

### Parameters

**`group-sep`** &larr; `string` *(optional)* <br/>
The group separator to use. If omitted, the function prints the current value.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).


## num-fmt-decimal-sep

```rant

[%num-fmt-decimal-sep: decimal-sep?; depth?]

```
&rarr; `string | empty`

Gets or sets the number formatter's decimal separator.

Shorthand for the `decimal-sep` option in `[num-fmt]`.

### Parameters

**`decimal-sep`** &larr; `string` *(optional)* <br/>
The decimal separator to use. 
If the supplied value is a blank string, the formatter falls back to `"."`. 
If omitted, the function prints the current value.

**`depth`** &larr; `int` *(optional)* <br/>
The depth of the scope whose number format to access. Value must be positive. Saturates to main program scope. <br/>
Defaults to 0 (the calling scope).