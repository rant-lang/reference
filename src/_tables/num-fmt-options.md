| Name          |   Type   |     Default     | Description                                                                        |
|---------------|:--------:|:---------------:|:-----------------------------------------------------------------------------------|
| `system`      | `string` |  `west-arabic`  | Numeral system to render numbers in<br/>*(See associated table)*                   |
| `alt`         |  `bool`  |     `false`     | Enables alternate formatting for the selected system                               |
| `precision`   |  `int`   |      `-1`       | Number of decimal places to pad/truncate to; set to -1 to disable                  |
| `padding`     |  `int`   |       `0`       | Minimum number of digits to pad the integral component to                          |
| `upper`       |  `bool`  |     `false`     | Enables current system's uppercase form                                            |
| `endian`      | `string` |      `big`      | Byte order for power-of-two bases (hex, binary...). <br/> *(See associated table)* |
| `sign`        | `string` | `negative-only` | Sign formatting style<br/>*(See associated table)*                                 |
| `infinity`    | `string` |    `keyword`    | Infinity formatting style <br/> *(See associated table)*                           |
| `group-sep`   | `string` |      `""`       | Digit group separator                                                              |
| `decimal-sep` | `string` |      `""`       | Decimal group separator; if not specified, defaults to `"."`                       |