| Value         | Description                                                         | Example (1234) |
|---------------|---------------------------------------------------------------------|:--------------:|
| `default`     | (Set-only) Same as `west-arabic`                                    |      1234      |
| `west-arabic` | Western Arabic numerals *(default)*                                 |      1234      |
| `east-arabic` | Eastern Arabic numerals                                             |      ١٢٣٤      |
| `persian`     | Persian numerals                                                    |      ۱۲۳۴      |
| `babylonian`  | Babylonian cuneiform numerals. Truncates decimals.                  |   𒌋𒌋 𒌍𒐘    |
| `roman`       | Roman numerals. Truncates decimals.                                 |    mccxxxiv    |
| `hex`         | Hexadecimal (base 16); Floats use IEEE 754 double-precision format. |      4d2       |
| `octal`       | Octal (base 8); Floats use IEEE 754 double-precision format.        |      2322      |
| `binary`      | Binary (base 2); Floats use IEEE 754 double-precision format.       |  10011010010   |
| `alpha`       | Latin alphabetical ordinals; identical to Excel column numbers      |      aul       |