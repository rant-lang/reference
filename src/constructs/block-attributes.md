# Block attributes

**Block attributes** are a set of constructs that control various aspects of block behavior.

## Variables

All block attributes are stored in a map variable called `__BATTRS`, which is created in the current local variable scope as soon as any block attribute is assigned.

`__BATTRS` may contain the following keys:

|Key|Type|Description|
|---|----|-----------|
|`reps`|`integer`|Repetitions|
|`rep-special`|`string` \| `none`|Special repetition type; see below.|
|`sep`|`integer` \| `float` \| `string`|Separator|
|`sel`|`map`||


Possible values for `__BATTRS/rep-special`:

|Value|Description|
|-----|-----------|
|`"all"`|Run as many times as there are elements in the block.|
|`"forever"`|Repeat forever.|