# @weight

The `@weight` charm assigns a weight value to the block element it is placed within.

## Usage

When writing a block with randomized selection, you may sometimes want to make some elements more or less likely to be selected.
This is where `@weight` comes in: by adding the `@weight` charm to a block element, you can specify the probability of it being selected.

The below snippet demonstrates the effect of block weights by generating a list of 20 random items of different rarities.

```rant
[rep:20][sep:\n]
{
    {
        # Larger weights are more likely to be selected
        "boring" @weight 2
        |
        # Unweighted elements have a default weight of 1
        "common"
        |
        # Smaller weights are less likely to be selected
        "uncommon" @weight 0.5
        |
        # Expressions can be used to assign weights dynamically
        "rare" @weight [randf: 0.05; 0.1]
        |
        # Elements with a weight of 0 are never selected.
        # If all elements have weights of 0, the block will not run.
        "unused" @weight 0
    } {herb|fungus|potion|poison|mineral|book}
}
```

The output will look something like this:

```
boring poison
boring fungus
boring poison
boring herb
boring mineral
common poison
boring mineral
boring fungus
common poison
uncommon fungus
common fungus
boring book
common herb
common potion
common herb
boring herb
rare book
uncommon mineral
common potion
common mineral
```

As you can see, "boring" and "common" items are by far the most frequently picked, while "uncommon" and "rare" items tend to occur much less frequently; 
"unused" items, on the other hand, never appear due to their weight of 0.

### Evaluation

When a weighted block resolves, it evaluates all weights in the order they appear before running any elements.
The weight values are retained until the block finishes resolving. For repeaters, all iterations use the same weights.

### Valid weight values

Weight values can be any number (`int` or `float`), other "weight-like" value, or an expression that evaluates to one of these;
there are, however, special cases where some values are handled differently:

* Negative weights are clamped to 0.
* Positive infinity, negative infinity, and NaN also default to 0.
* `~` produces a weight of 1.
* `@true` and `@false` produce weights of 1 and 0, respectively.

## Limitations

Weights are currently only used by default block selection and will be ignored by custom selectors.