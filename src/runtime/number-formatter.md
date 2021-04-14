# Number formatter

The **number formatter** enables you to passively apply custom formatting to numbers (`int` and `float`) when printing text.

## Functions

Each scope maintains its own separate number format. To change the number format options, you need to use the `[num-fmt*]` class of functions.

The following functions are available:

| Function                                                             | Desctipyion                                                               |
|----------------------------------------------------------------------|---------------------------------------------------------------------------|
| [`[num-fmt]`](/stdlib/formatting.md#num-fmt)                         | Set multiple format options at once or get a map of all format options    |
| [`[num-fmt-system]`](/stdlib/formatting.md#num-fmt-system)           | Get or set the current numeral system                                     |
| [`[num-fmt-alt]`](/stdlib/formatting.md#num-fmt-alt)                 | Get or set the alternate formatting flag                                  |
| [`[num-fmt-precision]`](/stdlib/formatting.md#num-fmt-precision)     | Get or set the decimal precision                                          |
| [`[num-fmt-padding]`](/stdlib/formatting.md#num-fmt-padding)         | Get or set the padding size for the integral part of the number           |
| [`[num-fmt-upper]`](/stdlib/formatting.md#num-fmt-upper)             | Get or set the uppercase formatting flag                                  |
| [`[num-fmt-endian]`](/stdlib/formatting.md#num-fmt-endian)           | Get or set the endianness for bytewise representations (hex, binary, etc) |
| [`[num-fmt-sign]`](/stdlib/formatting.md#num-fmt-sign)               | Get or set the sign style                                                 |
| [`[num-fmt-infinity]`](/stdlib/formatting.md#num-fmt-infinity)       | Get or set the infinity style                                             |
| [`[num-fmt-group-sep]`](/stdlib/formatting.md#num-fmt-group-sep)     | Get or set the group separator                                            |
| [`[num-fmt-decimal-sep]`](/stdlib/formatting.md#num-fmt-decimal-sep) | Get or set the decimal separator                                          |

## Options

The below table describes each option available in the number formatter.

{{ #include ../_tables/num-fmt-options.md }}

### The `system` option

{{ #include ../_tables/num-fmt-system.md }}

### The `endian` option

{{ #include ../_tables/num-fmt-endian.md }}

### The `sign` option

{{ #include ../_tables/num-fmt-sign.md }}

### The `infinity` option

{{ #include ../_tables/num-fmt-infinity.md }}

## Using [num-fmt]

The `[num-fmt]` function is the simplest way to configure complex formats. 
It enables you to set multiple options at once, or get a map of all current option values.

### Getting current options with [num-fmt]

To get a map of all number format options, just call `[num-fmt]` and omit the `options` parameter:

```rant
[num-fmt]
```

This prints a map with the following fields:

```
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
```

This can be stored in a variable for later use, or modified and passed back into the function.

### Setting options with [num-fmt]

To set options, pass a map to `[num-fmt]` with the fields you're interested in changing. 
This will overwrite only the specified options, leaving all others unchanged.

```rant
# Format numbers as 64-bit hex with 0x prefix
[num-fmt: @(system = hex; alt = @true; padding = 16)]
1000000000\n

# Change another option
[num-fmt-endian: little] 
1000000000\n
```
This produces the output:
```
0x000000003b9aca00
0xca9a3b0000000000
```