# @is* keywords

{{ #include _proposal_msg.md }}


Sequences can be configured to perform various boolean operations by prefixing them with any of several special @is-keywords. Each printed value acts as a separate operand; whitespace is ignored.

## Short-circuiting

Some operations are "short-circuiting"-- meaning that Rant may not evaluate the entire sequence in the scope if the result can be determined early. For example, if the first operand of a short-circuiting AND operation evaluates to @false, we know that the result will be @false, so we can skip evaluating the rest of the operands.

## Eagerness

The `+` token can be placed after the operator keyword (e.g. `@isany+`) to disable short-circuiting and make the sequence eagerly evaluated.

## @isany

The `@isany` keyword creates a short-circuiting boolean OR expression.

### Truth table

| `@isany A B`     | `A = @true` | `A = @false` |
|------------------|:-----------:|:------------:|
| **`B = @true`**  |   `@true`   |   `@true`    |
| **`B = @false`** |   `@true`   |   `@false`   |


## @isall

The `@isall` keyword creates a short-circuiting boolean AND expression.
Its complement is `@isntall`.

### Truth table

| `@isall A B`     | `A = @true` | `A = @false` |
|------------------|:-----------:|:------------:|
| **`B = @true`**  |   `@true`   |   `@false`   |
| **`B = @false`** |  `@false`   |   `@false`   |

## @isntall

The `@isntall` keyword creates a short-circuiting boolean NAND expression.

### Truth table

| `@isntall A B`   | `A = @true` | `A = @false` |
|------------------|:-----------:|:------------:|
| **`B = @true`**  |  `@false`   |   `@true`    |
| **`B = @false`** |   `@true`   |   `@true`    |

## @isnone

The `@isnone` keyword creates a short-circuiting boolean NOR expression.
Its complement is `@isany`.

### Truth table

| `@isnone A B`    | `A = @true` | `A = @false` |
|------------------|:-----------:|:------------:|
| **`B = @true`**  |  `@false`   |   `@false`   |
| **`B = @false`** |  `@false`   |   `@true`    |

## @isone

The `@isone` keyword creates a short-circuiting boolean XOR expression.

### Truth table

| `@isone A B`     | `A = @true` | `A = @false` |
|------------------|:-----------:|:------------:|
| **`B = @true`**  |  `@false`   |   `@true`    |
| **`B = @false`** |   `@true`   |   `@false`   |

## @ismany

The `@ismany` keyword creates a short-circuiting expression that evaluates to `@true` if more than one of the operands evaluates to `@true`; otherwise, it evaluates to `@false`.

### Truth table

| `@ismany A B C`              | `A = @true` | `A = @false` |
|------------------------------|:-----------:|:------------:|
| **`B = @false, C = @false`** |  `@false`   |   `@false`   |
| **`B = @true, C = @false`**  |   `@true`   |   `@false`   |
| **`B = @false, C = @true`**  |   `@true`   |   `@false`   |
| **`B = @true, C = @true`**   |   `@true`   |   `@true`    |

## @issame

The `@issame` keyword creates a short-circuiting equality expression.
Its complement is `@isdiff`.

Although the truth table shows boolean inputs, this operation accepts all types.

### Truth table

| `@issame A B C`              | `A = @true` | `A = @false` |
|------------------------------|:-----------:|:------------:|
| **`B = @false, C = @false`** |  `@false`   |   `@true`    |
| **`B = @true, C = @false`**  |  `@false`   |   `@false`   |
| **`B = @false, C = @true`**  |  `@false`   |   `@false`   |
| **`B = @true, C = @true`**   |   `@true`   |   `@false`   |


## @isdiff

The `@isdiff` keyword creates a short-circuiting inequality expression.
Its complement is `@issame`.

Although the truth table shows boolean inputs, this operation accepts all types.

### Truth table

| `@isdiff A B C`              | `A = @true` | `A = @false` |
|------------------------------|:-----------:|:------------:|
| **`B = @false, C = @false`** |   `@true`   |   `@false`   |
| **`B = @true, C = @false`**  |   `@true`   |   `@true`    |
| **`B = @false, C = @true`**  |   `@true`   |   `@true`    |
| **`B = @true, C = @true`**   |  `@false`   |   `@true`    |