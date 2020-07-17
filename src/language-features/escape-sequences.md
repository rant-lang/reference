# Escape sequences

It will, of course, be necessary to sometimes print reserved characters, or characters that cannot be typed on a standard keyboard.
To this end, Rant offers escape sequences.

## Character escape sequences

Any reserved (and most non-reserved) characters can be printed by prefixing each one with a backslash character:

```rant
\{This text will print with braces around it\}
```

## Special escape sequences

Certain characters are not interpreted verbatim when escaped, and instead have special meaning.
Here's a list of them:

|Escape sequence|Output character|
|---------------|----------------|
|`\r`|Carriage return (U+000D)|
|`\n`|Line feed (U+000A)|
|`\s`|Space (U+0020)|
|`\t`|Tab (U+0009)|
|`\0`|Null character (U+0000)|
|`\xXX`|UTF-8 character code _[See below]_|

## Unicode escape sequences

Escape sequences can also be used to print characters by their Unicode code point in hexicedimal format:

```rant
\xE4    # 'ä'
```