# Standard Library: Conversion functions

## to-float

```rant

[%to-float: value]

```
&rarr; `float | nothing`

Attempts to convert `value` to a `float` value and prints the result.
If the conversion fails, prints nothing.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## to-int

```rant

[%to-int: value]

```
&rarr; `int | nothing`

Attempts to convert `value` to an `int` value and prints the result.
If the conversion fails, prints nothing.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## to-string

```rant

[%to-string: value]

```
&rarr; `string | nothing`

Attempts to convert `value` to a `string` value and prints the result.
If the conversion fails, prints nothing.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## to-list

```rant

[%to-list: value]

```
&rarr; `list | nothing`

Attempts to convert `value` to a `list` and prints the result.
If the conversion fails, prints nothing.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.

### Conversion behavior

**From `string`**

Passing a `string` value into this function returns a `list` of the string's graphemes.

```rant
<%letters = [to-list: "hello"]>
[assert-eq: <letters>; (: h; e; l; l; o)]
```

**From `list`**

Passing a `list` value into this function prints a shallow copy of it.
This is equivalent to calling `[copy]` on the list.

**From `range`**

Passing a `range` value into this function prints a list of the range's elements in order.

```rant
<%seq = [range: 0; 5 |> to-list]>
[assert-eq: <seq>; (: 0; 1; 2; 3; 4)]
```

## to-tuple

```rant

[%to-tuple: value]

```
&rarr; `tuple | nothing`

Attempts to convert a value to a `tuple` and prints the result.
If the conversion fails, prints nothing.