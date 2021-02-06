# Standard Library: Conversion functions

### [float: value]
&rarr; `float` or `empty`

Attempts to convert `value` to a `float` value and returns the result.
If the conversion fails, returns `empty` value.

### [int: value]
&rarr; `int` or `empty`

Attempts to convert `value` to an `int` value and returns the reuslt.
If the conversion fails, returns `empty` value.

### [string: value]
&rarr; `string` or `empty`

Attempts to convert `value` to a `string` value and returns the result.
If the conversion fails, returns `empty` value.

### [list: value]
&rarr; `list` or `empty`

Attempts to convert `value` to a `list` and returns the result.
If the conversion fails, returns `empty` value.

**From `string`**

Passing a `string` value into this function returns a `list` of the string's graphemes.

```rant
<%letters = [list: "hello"]>
[assert-eq: <letters>; (h; e; l; l; o)]
```

#### From `list`

Passing a `list` value into this function returns a shallow copy of it.
This is equivalent to calling `[copy]` on the list.

#### From `range`

Passing a `range` value into this function returns a list of the range's elements in order.

```rant
<%seq = [range: 0; 5 |> list]>
[assert-eq: <seq>; (0; 1; 2; 3; 4)]
```