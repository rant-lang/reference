# Optional parameters

A function parameter can be made optional using the `?` modifier after the parameter name; this means that the caller is not required to pass an argument to it.

When an optional parameter is omitted, the variable won't exist in the function body; as a result, accessing it can fail, causing an error.
To prevent this from happening, you need to use a [fallback expression](/language/accessors/fallbacks.md) to provide a default value.

> Please note that all optional parameters must appear after all required parameters, and before any variadic parameter;
> breaking this order will cause a compiler error.

```rant
# Generates a map for a pet with a name and species (defaults to "dog")
[$gen-pet: name; species?] {
    @(
        name = <name>;
        species = <species ? "dog">; # Fallback to "dog" if species is undefined
    )
}
```