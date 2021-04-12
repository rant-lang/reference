# Standard Library: String functions

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