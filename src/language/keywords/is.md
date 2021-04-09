# @is* keywords

Blocks can be used to perform various boolean operations by prefixing them with any of several special @is-keywords. Each element of the attached block acts as a separate operand.

## Short-circuiting

Some operations are "short-circuiting"-- meaning that Rant may not evaluate all of the expressions in the block if the result can be determined early. For example, if the first operand of a short-circuiting AND operation evaluates to false, we know that the result will be false, so we can skip evaluating the rest of the operands.

## Eagerness

The `@each` modifier keyword can be placed after the `@is*` keyword to disable short-circuiting; this behavior is known as "eager evaluation."

## @isany

The `@isany` keyword creates a short-circuiting boolean OR expression.

### Truth table

| <code>@isany {A &vert; B}</code> | `A = true` | `A = false` |
|----------------------------------|:----------:|:-----------:|
| **`B = true`**                   |   `true`   |   `true`    |
| **`B = false`**                  |   `true`   |   `false`   |


## @isall

The `@isall` keyword creates a short-circuiting boolean AND expression.
Its complement is `@isntall`.

### Truth table

| <code>@isall {A &vert; B}</code> | `A = true` | `A = false` |
|----------------------------------|:----------:|:-----------:|
| **`B = true`**                   |   `true`   |   `false`   |
| **`B = false`**                  |  `false`   |   `false`   |

## @isntall

The `@isntall` keyword creates a short-circuiting boolean NAND expression.

### Truth table

| <code>@isntall {A &vert; B}</code> | `A = true` | `A = false` |
|------------------------------------|:----------:|:-----------:|
| **`B = true`**                     |  `false`   |   `true`    |
| **`B = false`**                    |   `true`   |   `true`    |

## @isnone

The `@isnone` keyword creates a short-circuiting boolean NOR expression.
Its complement is `@isany`.

### Truth table

| <code>@isnone {A &vert; B}</code> | `A = true` | `A = false` |
|-----------------------------------|:----------:|:-----------:|
| **`B = true`**                    |  `false`   |   `false`   |
| **`B = false`**                   |  `false`   |   `true`    |

## @isone

The `@isone` keyword creates a short-circuiting boolean XOR expression.

### Truth table

| <code>@isone {A &vert; B}</code> | `A = true` | `A = false` |
|----------------------------------|:----------:|:-----------:|
| **`B = true`**                   |  `false`   |   `true`    |
| **`B = false`**                  |   `true`   |   `false`   |

## @ismany

The `@ismany` keyword creates a short-circuiting expression that evaluates to `true` if more than one of the operands evaluates to `true`; otherwise, it evaluates to `false`.

### Truth table

| <code>@ismany {A &vert; B &vert; C}</code> | `A = true` | `A = false` |
|--------------------------------------------|:----------:|:-----------:|
| **`B = false, C = false`**                 |  `false`   |   `false`   |
| **`B = true, C = false`**                  |   `true`   |   `false`   |
| **`B = false, C = true`**                  |   `true`   |   `false`   |
| **`B = true, C = true`**                   |   `true`   |   `true`    |

## @issame

The `@issame` keyword creates a short-circuiting equality expression.
Its complement is `@isdiff`.

Although the truth table shows boolean inputs, this operation accepts all types.

### Truth table

| <code>@issame {A &vert; B &vert; C}</code> | `A = true` | `A = false` |
|--------------------------------------------|:----------:|:-----------:|
| **`B = false, C = false`**                 |  `false`   |   `true`    |
| **`B = true, C = false`**                  |  `false`   |   `false`   |
| **`B = false, C = true`**                  |  `false`   |   `false`   |
| **`B = true, C = true`**                   |   `true`   |   `false`   |


## @isdiff

The `@isdiff` keyword creates a short-circuiting inequality expression.
Its complement is `@issame`.

Although the truth table shows boolean inputs, this operation accepts all types.

### Truth table

| <code>@isdiff {A &vert; B &vert; C}</code> | `A = true` | `A = false` |
|--------------------------------------------|:----------:|:-----------:|
| **`B = false, C = false`**                 |   `true`   |   `false`   |
| **`B = true, C = false`**                  |   `true`   |   `true`    |
| **`B = false, C = true`**                  |   `true`   |   `true`    |
| **`B = true, C = true`**                   |  `false`   |   `true`    |