# String

The `string` type represents an immutable, ordered collection of zero or more characters (graphemes).

```rant
# Text is dynamically converted to a string
This text will become a string.

# String literals are exact string values
"    This will be indented."
```

## Indexing and slicing

Strings can be indexed and sliced just like other ordered collections. 

When you index a string, it will return another string containing just that character:

```rant
<@text $a = "example">

"text:"         <a>\n
"indexed:"      <a/0>\n
"sliced:"       <a/1..-1>\n

# text: example
# indexed: e
# sliced: xampl
```