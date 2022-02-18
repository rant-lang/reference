# Standard Library: String functions

## char

```rant

[%char: code]

```
&rarr; `string?`

Prints the Unicode character represented by the Unicode code point `code`. 
If `code` doesn't correspond to a valid character, prints nothing.

### Parameters

**`code`** &larr; `int` <br/>
The Unicode code point representing the character to print.


## lines

```rant

[%lines: str]

```
&rarr; `list`

Splits string `str` by line feed characters (0x0A, `\n`) and returns a list of the results.

### Parameters

**`str`** &larr; `string` <br/>
The input string.


## lower

```rant

[%lower: str]

```
&rarr; `string`

Converts string `str` to lowercase and returns the result.

### Parameters

**`str`** &larr; `string` <br/>
The input string.

## ord

```rant

[%ord: ch]

```
&rarr; `int`

Prints the Unicode code point of the specified character as an `int` value.
If an empty string is passed, prints nothing.

### Parameters

**`ch`** &larr; `string` <br/>
The input string that provides the character. This can be any length; the function only uses the first code point in the string.

### Example

```rant
[ord: \s]
# -> 32
```


## ord-all

```rant

[%ord-all: str]

```
&rarr; `list`

Prints a list of `int` values containing the Unicode code points contained in `str`.

### Parameters

**`str`** &larr; `string` <br/>
The input string.

### Example

```rant
# Prints a list of hex values of each code point from the input string
[%as-unicode-hex: str] {
  [cat: **[ord-all: <str>] 
    |> cat: [num-fmt: (:: system = hex; upper = @true)] U\+[] 
    |> tuple
  ]
}

[as-unicode-hex: 👨‍👩‍👦‍👦]
# -> (U+1F468; U+200D; U+1F469; U+200D; U+1F466; U+200D; U+1F466)
```


## split

```rant

[%split: str; sep?]

```
&rarr; `list`

Splits the input text by `sep` into a list of strings. If `sep` is omitted, splits into characters.

### Parameters

**`str`** &larr; `string` <br/>
The input string.

**`sep`** &larr; `string` *(optional)* <br/>
The delimiter to split on. If omitted, the string will be split into individual characters.


## seg

```rant

[%seg: str; size]

```
&rarr; `list`

Segments the input text into a list of strings of `size` length.

### Parameters

**`str`** &larr; `string` <br/>
The input string.

**`size`** &larr; `int` <br/>
The size of the segments to produce.


## upper

```rant

[%upper: str]

```
&rarr; `string`

Converts string `str` to uppercase and returns the result.