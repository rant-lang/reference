# The `map` type

The `map` type represents an unordered, mutable, resizable collection of zero or more key-value pairs, where each key is a unique string.

Map keys are always coerced to strings; if you try to access a map using a non-string key, the key will be automatically coerced to a string before use.

Map initializers are similar to list initializers, but the contents must begin with a double-colon (`::`).

Map keys come in two flavors:
* **Static keys:** Evaluated at compile-time. They must be identifiers or string literals.
* **Dynamic keys:** Evaluated at run-time. They must be blocks.

```rant
# Create an empty map
<$empty-map = (::)>

# Create a map with various value types
<$secret-key = occupation>
<$location = US>

(::
    # Regular keys and values
    name = Alex;
    age = 25;

    # Shorthand for `location = <location>`
    <location>;

    # String literals can specify keys that aren't valid identifiers
    "favorite color" = {red|green|blue};

    # An expression can also provide the key
    {<secret-key>} = painter
)
```