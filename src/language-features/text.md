# Text

In Rant, text is considered as a combination of two types of tokens: **fragments** and **whitespace**.

Any string of text is a valid Rant program.

## Fragments

A fragment is defined as a contiguous series of any characters that:
1. are not whitespace,
2. do not contain any reserved characters (e.g. braces, brackets, etc.)

Rant will output any fragment verbatim.

```rant
# Prints "Hello"
Hello
```

## Whitespace

Any continguous series of whitespace characters between two fragments (including line breaks) is normalized to a single space by default.
Any other whitespace is ignored.

To illustrate this behavior, consider the following Rant snippet:

```rant
The
 Quick
  Brown
   Fox
    Jumps
     Over
      The
       Lazy
        Dog.
```

By default, Rant will print this as `The Quick Brown Fox Jumps Over The Lazy Dog.`
Whitespace printing behavior can be customized through formatting functions (discussed later).

## String literals

If you want to treat any string as a single fragment, you can wrap it in a string literal using double quotes:

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