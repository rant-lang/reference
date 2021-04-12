# Standard Library: Boolean functions

## and

```rant

[%and: a; b; c*]

```
&rarr; `bool`

Performs a boolean AND operation on the operands and returns the result.

### Parameters

**`a`** &larr; `bool` <br/>
The left-hand operand.

**`b`** &larr; `bool` <br/>
The right-hand operand.

**`c`** &larr; `bool*` *(optional)* <br/>
Any additional right-hand operands.

## not

```rant

[%not: a]

```
&rarr; `bool`

Returns the inverse of the input boolean value.

### Parameters

**`a`** &larr; `bool` <br/>
The value to invert.

## or

```rant

[%or: a; b; c*]

```
&rarr; `bool`

Performs a boolean inclusive OR operation on the operands and returns the result.

### Parameters

**`a`** &larr; `bool` <br/>
The left-hand operand.

**`b`** &larr; `bool` <br/>
The right-hand operand.

**`c`** &larr; `bool*` *(optional)* <br/>
Any additional right-hand operands.


## xor

```rant

[%xor: a; b]

```
&rarr; `bool`

Performs a boolean XOR operation on the operands and returns the result.

### Parameters

**`a`** &larr; `bool` <br/>
The left-hand operand.

**`b`** &larr; `bool` <br/>
The right-hand operand.