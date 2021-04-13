# Depth Operator

The **depth operator** can be applied to variable getters to retrieve the number of scope boundaries between the getter and the target variable's definition.

This operator is generally intended for more advanced use cases, such as allowing module authors to make cross-scope access code (such as that for setting formatting options) more maintainable.

## Syntax
The depth operator is denoted by the `&` token. It may be placed at the end of a variable name in a non-dynamic variable getter.
When this operator is present on a variable name, the getter will print the stack "depth" of the variable:

```rant
<%foo = bar>
<foo&> # 0
```
This simply prints `0`, because the depth getter is at the same scope level as the definition of `foo`.

Let's look at a couple more examples that introduce nesting:

```rant
<%marker>   # Since we're just using this constant to measure depth, it can be left empty
{ <marker&> }\n
{{ <marker&> }}\n
{{ [cat: <marker&>] }}\n
```
This prints the following:
```
1
2
3
```
In the first getter, there is one scope (the block) between it and the variable, so it prints `1`. The second getter is inside two blocks, so it prints `2`.

The third example shows two different kinds of scopes: two block scopes and an argument scope. Since these are all on the call stack when the getter runs, it prints `3`.

## Remarks

A basic depth getter can still capture its target variable into a function, which can produce confusing results:

```rant
<%MARKER>
[%measure] {
    <MARKER&>
}

# This should print 1... right?
[measure]
```
This prints:
```
0
```
(Wait, what?)

This happens because `MARKER` is captured into `[measure]` as a local variable, and is thus redeclared in the main `[measure]` scope.
Since the depth getter is also at this scope level, we get a result of 0 instead of 1.

Thankfully, this is easy to fix: just descope the getter and it will no longer capture:

```rant
<%MARKER>
[%measure] {
    <^MARKER&> # Now with descope
}

[measure] # Should print 1
```
Barring unexpected cosmic rays, this should now work as expected and print `1`.
