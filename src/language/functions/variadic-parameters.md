# Variadic parameters

Functions support variadic parameters with the special symbols `*` and `+`.

A `*` parameter is optional and defaults to an empty list, while a `+` parameter is required and must contain at least one element.

Functions may only have up to one variadic parameter, and it must appear last in the signature.

```rant
[$how-many: items*] {
    [len: <items>]
}

[how-many: foo; bar; baz] # Outputs "3"
```