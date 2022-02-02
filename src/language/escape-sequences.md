# Escape sequences

Some scripts may need to print characters reserved by the language, or characters that cannot be typed on a standard keyboard layout.
To help with this, Rant offers **escape sequences**.

## Character escapes

Any reserved character can be printed by prefixing it with `\`:

```rant
\{This text will print with braces around it\}
```

## Special escapes

Certain characters are not interpreted verbatim when escaped, and instead have special meaning.
Here's a list of them:

| Escape sequence | Output character                     |
|-----------------|--------------------------------------|
| `\\`            | Backslash                            |
| `\n`            | Line feed (U+000A)                   |
| `\r`            | Carriage return (U+000D)             |
| `\s`            | Space (U+0020)                       |
| `\t`            | Tab (U+0009)                         |
| `\0`            | Null character (U+0000)              |
| `\xXX`          | Byte escape _[See below]_            |
| `\uXXXX`        | 16-bit Unicode escape _[See below]_  |
| `\UXXXXXXXX`    | 32-bit Unicode escape _[See below]_  |
| `\U(XXXXXXXX)`  | Unsized Unicode escape _[See below]_ |

### Unicode escapes

Escape sequences can also be used to specify arbitrary Unicode characters by their hexadecimal form:

```rant
# Byte escape
\xE4    # 'ä'

# 16-bit Unicode escape
\u2705 # ✅

# 32-bit Unicode escape
\U0001F602 # 😂

# Unsized Unicode escape (1-8 digits)
\U(1f629)\U(1f44c) # 😩👌
```