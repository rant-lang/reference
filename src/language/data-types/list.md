# List

The `list` type represents a mutable, resizable, ordered collection of zero or more values.

Lists are initialized using a pair of parentheses containing the list elements, separated by semicolons:

```rant
# A pair of parentheses is treated like an empty list
<$empty-list = (:)>

# Initialize a list with one element set to <>
<$one-nothing = (: <>)>

# Create a list of numbers
<$lucky-numbers = (: 1; 2; 3; 5; 7; 11; 13;)>

# Create a list of lists
<$important-lists = (: (: A; B; C); (: D; E; F))>

# Trailing semicolons are allowed!
<$powers-of-two = (: 1; 2; 4; 8; 16;)>
```

## List indexing

List indices start at 0 and can be accessed by adding the index to the accessor path.

You can also use negative indices to access items relative to the end of a list, starting from -1 and going down.

```rant
# Create a list
<$list = (: 1; 2; 3; 4; 5; 6; 7; 8; 9)>

# Get first item
<list/0>\n      # 1

# Get second item
<list/1>\n      # 2

# Get last item
<list/-1>\n     # 9

# Get second to last item
<list/-2>\n     # 8

# Change third item from 3 to -3
<list/2 = -3>
<list/2>        # -3
```