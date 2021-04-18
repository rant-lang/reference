# Standard Library: Conversion functions

## float

```rant

[%float: value]

```
&rarr; `float | empty`

Attempts to convert `value` to a `float` value and returns the result.
If the conversion fails, returns `empty` value.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## int

```rant

[%int: value]

```
&rarr; `int | empty`

Attempts to convert `value` to an `int` value and returns the result.
If the conversion fails, returns `empty` value.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## string

```rant

[%string: value]

```
&rarr; `string | empty`

Attempts to convert `value` to a `string` value and returns the result.
If the conversion fails, returns `empty` value.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.


## list

```rant

[%list: value]

```
&rarr; `list | empty`

Attempts to convert `value` to a `list` and returns the result.
If the conversion fails, returns `empty` value.

### Parameters

**`value`** &larr; `any` <br/>
The input value to convert.

### Conversion behavior

**From `string`**

Passing a `string` value into this function returns a `list` of the string's graphemes.

```rant
<%letters = [list: "hello"]>
[assert-eq: <letters>; (h; e; l; l; o)]
```

**From `list`**

Passing a `list` value into this function returns a shallow copy of it.
This is equivalent to calling `[copy]` on the list.

**From `range`**

Passing a `range` value into this function returns a list of the range's elements in order.

```rant
<%seq = [range: 0; 5 |> list]>
[assert-eq: <seq>; (0; 1; 2; 3; 4)]
```