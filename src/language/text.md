# Text

In Rant, "text" is defined as a combination of two types of tokens: **fragments** and **whitespace**.

By this definition, any text is a valid Rant program.


## Fragments

A **fragment** is defined as any contiguous sequence of characters that:
1. contains no whitespace,
2. contains no reserved characters (e.g. braces, brackets, etc.)

By default, Rant will print any fragment verbatim.

```rant
# Prints "Hello"
Hello
```


## Whitespace

All sequences of non-breaking whitespace between two fragments or hinted elements on the same line are normalized to a single space character (U+0020) by default.

Rant produces a whitespace token from any contiguous sequence of characters with the `White_Space` Unicode property, 
excluding U+000A (LINE FEED, LF) and U+000D (CARRIAGE RETURN, CR).

Line breaks of the forms (CR), (LF), and (CRLF) are ignored.

Escape sequences that explicitly specify whitespace characters (`\t`, `\s`, etc.) are **always** printed.

### Example

The following example shows some of the ways that Rant can handle whitespace.

```rant
# Space normalization
One space\n
Two  spaces\n
Three   spaces\n
\n

# Indentation
Non-indented text\n
    Indented text\n
\n

# Multiple lines
Water
melon
```

This prints the following output:
```
One space
Two spaces
Three spaces

Non-indented text
Indented text

Watermelon
```


## Hinting

Rant's whitespace rules are quite strict, which can sometimes cause whitespace to be omitted when you actually want it there.

To alleviate this issue, Rant offers a compile-time annotation called a **hint**, represented by the backtick character (<code>`</code>).
When a hint is added before an expression unit (e.g. function call, getter, etc), it is referred to as "hinted." 
Rant will include whitespace around them as appropriate, as if they were fragments.

Some expression units are implicitly hinted, specifically:

* Blocks with text
* Numbers and getters with other text before them in the same expression

**Examples of implicit and explicit hinting**
```rant
# Implicitly hinted (block contains fragments)
The coin landed on {Heads|Tails}.

# Explicitly hint the function call so the compiler knows it's part of the text
Your lucky number is `[rand:1;100].
```

### Auto-hinting

You can also designate variables, parameters, and functions as "auto-hinted" to the compiler.
See the page on [`@text`](/language/keywords/text.md) for more information.


## Sinking

Not all whitespace is meaningful. Some whitespace doesn't serve any function, for example, indents within an expression.
In some cases, Rant may mistake this as printable whitespace. Clearly this would be a problem.

For these cases, there is the **sink**, represented by the `~` character, which does the opposite of a hint: 
it tells the compiler that an expression unit should **not** be treated like text.

For example, suppose we want to randomly output either a smile or frown:
```rant
\:{\(|\)}
# :)
# :(
```

Over time you might expand your code to include more complex branches and you might want to add spaces between the components for readability.

```rant
{\:|\;} {\(|\)}
# : )
# : (
# ; )
# ; (
```

Now the space is in the output&mdash; not good. To clarify that we don't need the whitespace between the blocks, we can sink one or both blocks:

```rant
{\:|\;} ~{\(|\)}
# :)
# :(
# ;)
# ;(
```

Using sinks where appropriate not only makes your intentions less ambiguous to the compiler, 
but also helps others reading your code understand when whitespace is explicitly not part of the output.

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

### Quotation marks in string literals

If you want to put a quotation mark inside of a string literal, just double it up like so:

```rant
"This string literal includes ""quoted"" text"
```


## "Text" vs "string"

It is important to understand that strings and text are two different concepts in Rant:

A string is a sequence of Unicode characters, represented by the `string` type.

Text is a sequence of fragments, whitespace, and hinted elements in a Rant program.<br/>
When interpreted at runtime, it may not always produce a string identical to the original text, due to whitespace rules and annotations.


## TL;DR

> **Quick Recap**
>
> **1.** A fragment is a contiguous series of visible characters.<br/>
> **2.** Whitespace only prints between two fragments on the same line and prints as a single space.<br/>
> **3.** A hint (<code>\`</code>) treats an expression unit like a fragment.<br/>
> **4.** A sink (`~`) treats an expression unit like a non-fragment.<br/>
> **5.** A string literal counts as a single fragment and can contain any characters.<br/>
> **6.** Text is part of your program; a string is the data created from it.<br/>
