# Text

In Rant, raw text is considered as a combination of two types of tokens: **fragments** and **whitespace**.

Any text is a valid Rant program.

## Fragments

A **fragment** is defined as any sequence of characters that:
1. contains no whitespace,
2. contains no reserved characters (e.g. braces, brackets, etc.)

Rant will output any fragment verbatim.

```rant
# Prints "Hello"
Hello
```

## Whitespace

All sequences of non-breaking whitespace between two fragments in a Rant program are normalized to a single space by default.

Rant is very selective about the whitespace it prints. By default, whitespace included in a Rant program is only printed if it is between any two of the following:
* Fragments
* Numbers
* Getters
* Blocks containing any of the above
* Blocks that satisfy the aforementioned requirement

All other whitespace (including line breaks) is ignored. 
Escape sequences that output whitespace (`\t`, `\s`, etc.) are exempt from this rule and treated like fragments.

> TODO: Add examples

## Hinting

Rant's whitespace rules are quite strict, which can sometimes cause whitespace to be omitted when you actually want it there.

To alleviate this issue, Rant offers a compile-time annotation called a **hint**, represented by the backtick character (<code>`</code>).
When a hint is added before a code element (e.g. a function call), is is referred to as "hinted." 
Rant will treat hinted items like text and include whitespace around them as if they were fragments.

Some program elements are automatically hinted by the compiler:

* Numbers and getters are hinted if there is other text in the same scope.
* Blocks with text are automatically hinted.

```rant
# Implicitly hinted (block contains fragments)
The coin landed on {Heads|Tails}.

# Explicitly hint the function call so the compiler knows it prints something
Your lucky number is `[rand:1;100].
```

## Sinking

Sometimes we want to combine text-like elements in a context where whitespace isn't needed.
Rant may accidentally introduce the whitespace into the output because it thinks it's part of the text. Clearly, that would be a problem.

For these cases, there is a second compile-time annotation called the **sink**, represented by the `~` character, which does the opposite of a hint: 
it tells the compiler that a code element should **not** be treated like text.

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

Now the space is in the output-- not good. To clarify that we don't need the whitespace between the blocks, we can sink one or both blocks:

```rant
{\:|\;} ~{\(|\)}
# :)
# :(
# ;)
# ;(
```

Using sinks where appropriate not only makes your intentions less ambiguous to the compiler, 
but also helps others reading your code to understand when whitespace is explicitly not part of the output.

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

## "Text" vs "string"

It is important to understand that strings and text are two different concepts in Rant:

A string is a sequence of Unicode characters, represented by the `string` type in Rant.

Text is a sequence of fragments, whitespace, and hinted elements in a Rant program.<br/>
When interpreted at runtime, it may not always produce an string identical to the original text, due to whitespace rules and annotations.

**Bottom line:** a string is a value, and text is used to generate a string.