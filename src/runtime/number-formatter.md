# Number formatter

The **number formatter** enables you to passively apply custom formatting to numbers (`int` and `float`) when printing text.

## Functions

Each scope maintains its own separate number format. To change the number format options, you need to use the `[num-fmt*]` class of functions.

The following functions are available:

| Function                | Desctipyion                                                               |
|-------------------------|---------------------------------------------------------------------------|
| `[num-fmt]`             | Set multiple format options at once or get a map of all format options    |
| `[num-fmt-system]`      | Get or set the current numeral system                                     |
| `[num-fmt-alt]`         | Get or set the alternate formatting flag                                  |
| `[num-fmt-precision]`   | Get or set the decimal precision                                          |
| `[num-fmt-padding]`     | Get or set the padding size for the integral part of the number           |
| `[num-fmt-upper]`       | Get or set the uppercase formatting flag                                  |
| `[num-fmt-endian]`      | Get or set the endianness for bytewise representations (hex, binary, etc) |
| `[num-fmt-sign]`        | Get or set the sign style                                                 |
| `[num-fmt-infinity]`    | Get or set the infinity style                                             |
| `[num-fmt-group-sep]`   | Get or set the group separator                                            |
| `[num-fmt-decimal-sep]` | Get or set the decimal separator                                          |

## Options

The below table describes each option available in the number formatter.

| Name          |   Type   |     Default     | Description                                                                        |
|---------------|:--------:|:---------------:|:-----------------------------------------------------------------------------------|
| `system`      | `string` |  `west-arabic`  | Numeral system to render numbers in<br/>*(See associated table)*                   |
| `alt`         |  `bool`  |     `false`     | Enables alternate formatting for the selected system                               |
| `precision`   |  `int`   |      `-1`       | Number of decimal places to pad/truncate to; set to -1 to disable                  |
| `padding`     |  `int`   |       `0`       | Minimum number of digits to pad the integral component to                          |
| `upper`       |  `bool`  |     `false`     | Enables current system's uppercase form                                            |
| `endian`      | `string` |      `big`      | Byte order for power-of-two bases (hex, binary...). <br/> *(See associated table)* |
| `sign`        | `string` | `negative-only` | Sign formatting style<br/>*(See associated table)*                                 |
| `infinity`    | `string` |    `keyword`    | Infinity formatting style <br/> *(See associated table)*                           |
| `group-sep`   | `string` |      `""`       | Digit group separator                                                              |
| `decimal-sep` | `string` |      `""`       | Decimal group separator; if not specified, defaults to `"."`                       |

### The `system` option

| Value         | Description                                                         | Example (1234) |
|---------------|---------------------------------------------------------------------|:--------------:|
| `default`     | (Set-only) Same as `west-arabic`                                    |      1234      |
| `west-arabic` | Western Arabic numerals *(default)*                                 |      1234      |
| `east-arabic` | Eastern Arabic numerals                                             |      ١٢٣٤      |
| `persian`     | Persian numerals                                                    |      ۱۲۳۴      |
| `babylonian`  | Babylonian cuneiform numerals. Truncates decimals.                  |   𒌋𒌋 𒌍𒐘    |
| `roman`       | Roman numerals. Truncates decimals.                                 |    mccxxxiv    |
| `hex`         | Hexadecimal (base 16); Floats use IEEE 754 double-precision format. |      4d2       |
| `octal`       | Octal (base 8); Floats use IEEE 754 double-precision format.        |      2322      |
| `binary`      | Binary (base 2); Floats use IEEE 754 double-precision format.       |  10011010010   |

### The `endian` option

| Value     | Description                                                  |
|-----------|--------------------------------------------------------------|
| `default` | (Set-only) Same as `big`                                     |
| `big`     | Specifies big-endian byte order (MSB goes first) *(default)* |
| `little`  | Specifies little-endian byte order (LSB goes first)          |

### The `sign` option

| Value               | Description                                                                        |
|---------------------|------------------------------------------------------------------------------------|
| `default`           | (Set-only) Same as `negative-only`                                                 |
| `negative-only`     | Show a minus on negative numbers; otherwise, nothing.                              |
| `explicit`          | Show a plus on positive numbers (including zero), and a minus on negative numbers. |
| `explicit-non-zero` | Show a plus on positive numbers, nothing on zero, and a minus on negative numbers. |

### The `infinity` option

| Value     | Description                                                                  |
|-----------|------------------------------------------------------------------------------|
| `default` | (Set-only) Same as `keyword`                                                 |
| `keyword` | Uses `-infinity` for negative infinity and `infinity` for positive infinity. |
| `symbol`  | Uses `-∞` for negative infinity and `∞` for positive infinity.               |

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
[num-fmt: @(system = hex; alt = true; padding = 16)]
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