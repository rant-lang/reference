# Collections

Rant's variable system has five collection types: `list`, `tuple`, `map`, `string`, and `range`.

## Comparison

Some collections can be mutated (modified), while others are read-only. Some can be sliced but not spliced. 
Below is a breakdown of which operations each collection type supports:


|   Type   |   Read    |   Write   |   Slice   |  Splice   |
|:--------:|:---------:|:---------:|:---------:|:---------:|
|  `list`  | &#x1f7e2; | &#x1f7e2; | &#x1f7e2; | &#x1f7e2; |
| `tuple`  | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
| `string` | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
| `range`  | &#x1f7e2; | &#x1f534; | &#x1f7e2; | &#x1f534; |
|  `map`   | &#x1f7e2; | &#x1f7e2; | &#x1f534; | &#x1f534; |

<p></p>

|Legend                                            |
|:------------------------------------------------:|
|&#x1f7e2; = supported; &#x1f534; = not supported  |

