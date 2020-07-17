# Selectors

A **selector** is a block attribute type that controls how a block selects items.

In earlier versions of Rant, they were known as "synchronizers."

```rant
# Create selector `x`
[mksel: x; reverse]
# Set repetitions to a random number in the range [10, 20]
[rep:[n:10;20]]
# Set separator to space
[sep:\s]
# Set selector to `x`
[sel:x]
{A|B|C|D|E|F|G|H}
```