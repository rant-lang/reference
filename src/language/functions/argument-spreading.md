# Argument spreading

Argument spreading enables you to deconstruct a list argument into multiple individual arguments.

Rant exposes this functionality through two spread operators: **parametric spread** (`*`), and **temporal spread** (`**`).

## Parametric spread

The **parametric spread operator** lets you use a list to pass multiple arguments at once to a single function call.
This operation is referred to in Rant as "parametric spreading" or simply "spreading."

Spreading is mostly useful for cases where the contents of a list need to be passed to a variadic parameter,
but it will work on any other parameter (required, optional, or variadic).

There are no restrictions on the position of a spread within an argument list;
you can add them to the start, end, middle, or even have multiple spreads sprinkled throughout.
As long as the final argument list meets the requirements of the target function, it "just works."

Argument spreading is performed by prefixing an argument with `*`, as seen below:

```rant
<$extras = (baz; qux)>
[cat: foo; bar; * <extras>; boo]
# -> [cat: foo; bar; baz; qux; boo]
```

Attempting to spread a non-list will simply pass the value as a normal argument.


## Temporal spread

Rant has a second spread operatior, the **temporal spread operator** (`**`), which behaves differently from a parametric spread.

Instead of spreading across parameters, it spreads across time itself:
the target function is called once **for each value** in the temporally spread list argument (known as a "temporal argument"), passing in the current list item as the argument value.
This essentially turns the function call into a loop.

This is best explained with the following example:
```rant
# Simple function that prints tab-separated values with a newline at the end
[%println: cols*] {
    [join: <cols>; \t]\n
}

<%items = (foo; bar; baz)>

NORMAL SPREAD:\n
[println: * <items>]\n
# -> [println: foo; bar; baz]

TEMPORAL SPREAD:\n
[println: ** <items>]\n
# -> [println: foo]
# -> [println: bar]
# -> [println: baz]
```
This produces the following output:
```
NORMAL SPREAD:
foo     bar     baz

TEMPORAL SPREAD:
foo
bar
baz
```

As with parametric spreading, using a temporal spread on a non-list argument simply passes it as a regular argument.

### Multiple temporal arguments

A function call can have more than one temporal argument. When this happens,
Rant will call the function once for each possible combination of values from all temporal arguments.

When iterating through the combinations, Rant will increment the selection for the leftmost temporal argument first. 
When it rolls back over to the first item, the selection of the second temporal argument is incremented, then the third, and so on.
The total number of iterations will be equal to the product of the lengths of all temporal arguments.

The following example demonstrates how this works:

```rant
# Print out every combination (disgusting or not) of two lists of seasonings
[cat: **(salt; pepper; sugar); \t; **(cinnamon; cilantro; basil; cloves); \n]
```

This produces the following output:
```
salt    cinnamon
pepper  cinnamon
sugar   cinnamon
salt    cilantro
pepper  cilantro
sugar   cilantro
salt    basil
pepper  basil
sugar   basil
salt    cloves
pepper  cloves
sugar   cloves
```

### Temporal argument synchronization

In some cases it may be desirable to perform an operation only on elements with matching indices from two or more lists (often called a "zip" operation).
Thankfully, this is easy to do with temporal arguments by adding a **label** to the temporal spread operators you want to synchronize.

To add a label to a temporal spread operator, simply add any sequence of alphanumeric characters, understores, and hyphens between the two `*` characters, like this:

```rant
[cat: *a* (1; 2; 3); *a* (A; B; C); \n]
# -> [cat: 1; A; \n]
# -> [cat: 2; B; \n]
# -> [cat: 3; C; \n]
```

Doing this produces only 3 iterations:
```
1A
2B
3C
```


