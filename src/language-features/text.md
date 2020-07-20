# Text

In Rant, text is considered as a combination of two types of tokens: **fragments** and **whitespace**.

Any string of text is a valid Rant program.

## Fragments

A **fragment** is defined in Rant as any sequence of characters that:
1. contains no whitespace,
2. contains no reserved characters (e.g. braces, brackets, etc.)

Rant will output any fragment verbatim.

```rant
# Prints "Hello"
Hello
```

## Whitespace

All sequences of whitespace in a Rant program are normalized to a single space by default.

Rant is very selective about the whitespace it prints. By default, whitespace included in a Rant program is only printed if it is between any two of the following:
* Fragments
* Numbers
* Getters
* Blocks containing any of the above
* Blocks that satisfy the aforementioned requirement

All other whitespace (including line breaks) is ignored. Escaped whitespace (`\t`, `\s`, etc.) are exempt from this rule.

> TODO: Add examples

## Hinting

Because Rant's whitespace rules are quite strict, it is sometimes necessary to give the compiler additional information about the structure of your output.

This can be achieved by adding **hints** (symbolized by a `'`) to your code. 
A hint informs the compiler that the next element of code will print to the output, and that the whitespace between it and another printing element should be included.

The following elements are implicitly hinted:

* Numbers
* Variable getters
* Blocks containing at least one fragment, number, getter, hinted element, or nested block that meets this requirement

The act of a block inheriting a hint from its contents is known as "taking the hint."

```rant
# Implicitly hinted (block contains fragments)
The coin landed on {Heads|Tails}.

# Explicitly hint the function call so the compiler knows it prints something
Your lucky number is '[n:1;100].
```

## Sinking

If you want to suppress the output of a code element, you can **sink** it with the `_` operator.

Sinking an element has the opposite effect of hinting: it will be marked as "non-printing" and any whitespace between it and another non-printing element will also be ignored.

Only fragments and numbers cannot be sinked; the `_` character will be interpreted as text in such contexts.

Blocks that are sinked cannot take a hint.

```rant
{Now you see me...}     # Prints like normal
_{Now you don't.}       # Prints nothing
Goodbye _{cruel} world! # Prints "Goodbye world!"
_Fragment               # Prints "_Fragment", as fragments cannot be sinked
```


## String literals

If you want to treat any text as a single fragment, you can wrap it in a string literal using double quotes:

```rant
"    This text is indented"
```

They even work over several lines:

```rant
"This
text
has
several
lines"
```