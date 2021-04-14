# Standard Library: Verification functions

## is-some

```rant

[%is-some: value] 

```
&rarr; `bool`

Returns `@true` if `value` is any non-`empty` type.

### Paraneters

**`value`** &larr; `any` <br/>
The value to check.


## is-between

```rant

[%is-between: value; a; b]

```
&rarr; `bool`

Returns `@true` if `value` is bewteen `a` and `b` (both inclusive).

### Parameters

**`value`** &larr; `any` <br/>
The value to check.

**`a`** &larr; `any` <br/>
The first bound.

**`b`** &larr; `any` <br/>
The second bound.


## is-bool

```rant

[%is-bool: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `bool`.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-empty

```rant

[%is-empty: value]

```
&rarr; `bool`

Returns `@true` if `value` is `~`.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-even

```rant

[%is-even: number]

```
&rarr; `bool`

Returns `@true` if `number` is an even number.

### Parameters

**`number`** &larr; `int | float` <br/>
The number to check.


## is-float

```rant

[%is-float: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `float`.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-int

```rant

[%is-int: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `int`.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-nan

```rant

[%is-nan: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `float` and equal to NaN (Not a Number).

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-number

```rant

[%is-number: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `int` or `float`.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-odd

```rant

[%is-odd: number]

```
&rarr; `bool`

Returns `@true` if `number` is an odd number.

### Parameters

**`value`** &larr; `any` <br/>
The value to check.


## is-string

```rant

[%is-string: value]

```
&rarr; `bool`

Returns `@true` if `value` is of type `string`.


### Parameters

**`value`** &larr; `any` <br/>
The value to check.