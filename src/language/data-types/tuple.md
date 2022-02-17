# The `tuple` type

The `tuple` type represents an immutable, ordered collection of zero or more values.

```rant
()          # Empty tuple
(1;)        # Trailing semicolon required on 1-tuples
(1; 2)      # Trailing semicolon optional on tuples with arity greater than 1
(1; 2; 3)  
```