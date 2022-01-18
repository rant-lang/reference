# Conditional statements

Conditional statements are constructed using the `@if`, `@elseif`, and `@else` keywords.

## Syntax

**Standalone `@if`**
```rant
@if CONDITION1: {
    # ...
}
```

**`@if`-`@elseif` chaining**
```rant
@if CONDITION1: {
    # ...
} @elseif CONDITION2: {
    # ...
} @elseif CONDITION3: {
    # ...
}
```

**`@if`-`@else` chaining**
```rant
@if @CONDITION1: {
    # do something when <condition> is true
} @else: {
    # do something when <condition> is false
}
```

**`@if`-`@elseif`-`@else` chaining**
```rant
@if CONDITION1: {
    # ...
} @elseif CONDITION2: {
    # ...
} @elseif CONDITION3: {
    # ...
} @else: {
    # ...
}
```

## Truthiness

All condition values are coerced to `bool` using truthiness rules.

The truthiness rules are as follows:

| Data type                        | Evaluation                                      |
|----------------------------------|-------------------------------------------------|
| `bool`                           | Unchanged.                                      |
| `string`, `list`, `map`, `range` | `@true` if nonzero length; otherwise, `@false`. |
| `float`, `int`                   | `@true` if nonzero; otherwise, `@false`.        |
| `empty`                          | Always `@false`.                                |
| `special`, `function`            | Always `@true`.                                 |