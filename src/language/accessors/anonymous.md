# Anonymous Accessors

It is common to store a value, such as a list, in a variable before accessing its contents. 
However, you can also access elements on inline values directly using an **anonymous accessor**.

To create an anonymous accessor, replace the variable name in the accessor with an expression enclosed in `()`. 
Write the rest of your access path as normal.

Both getters and setters can be made anonymous; however, anonymous setters must include at least one index or key.

### Example 1

```rant
# Create two lists
<$list1 = (:1;2;3;4;5;6;7;8)>
<$list2 = (:a;b;c;d;e;f;g;h)>

# Create a function that returns one of two lists
[$get-either-list]{{<list1>|<list2>}}

# Call [get-random-list] and get the 4th item (index 3) of the returned list
<([get-either-list])/3> # Returns either '4' or 'd'
```

### Example 2

```rant
# Get the first letter of a string literal
<("hello")/0> # Returns 'h'
```