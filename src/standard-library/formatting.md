# Formatting

### [whitespace-fmt: mode?; custom-value?]

Gets or sets the whitespace normalization mode.
This does not affect whitespace in escape sequences and string literals.

Passing no arguments to this function will simply get the current mode.

#### Formatting modes

|Mode        |Description                                                                    |
|------------|-------------------------------------------------------------------------------|
|`default`   |_(Default)_ Normalizes all whitespace to a single ASCII space character (0x20).|
|`verbatim`  |Prints all printable whitespace as it appears in the code.                     |
|`ignore-all`|Ignores all printable whitespace.                                              |
|`custom`    |Replaces all whitespace sequences with the `custom-value` argument.            |

#### Example

```rant
[whitespace-fmt: default] The quick brown fox    jumps over the lazy dog.
# Output: The quick brown fox jumps over the lazy dog.

[whitespace-fmt: verbatim] The quick brown fox    jumps over the lazy dog.
# Output: The quick brown fox    jumps over the lazy dog.

[whitespace-fmt: ignore-all] The quick brown fox    jumps over the lazy dog.
# Output: Thequickbrownfoxjumpsoverthelazydog.

[whitespace-fmt: custom; ...\s] The quick brown fox    jumps over the lazy dog.
# Output: The... quick... brown... fox... jumps... over... the... lazy... dog.
```