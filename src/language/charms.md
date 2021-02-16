# Charms

**Charms** are control flow expressions denoted by a **@keyword**.
There are several types of charms for performing different types of operations.

## Syntax

A charm is a right-associative operator composed of any supported keyword, which always starts with the `@` token.
If an expression includes a charm, the charm will consume the rest of the expression.

The currently supported charm keywords are `@return`, `@continue`, `@break`, and `@weight`.

The general syntax is as follows:

```
MAIN EXPRESSION @keyword [CHARM EXPRESSION]
```