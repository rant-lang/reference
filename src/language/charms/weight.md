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
        # Negative weight values have a weight of 1 / |w * 10|
        "rare" @weight -1
        |
        # Elements with a weight of 0 are never selected.
        # If all elements have weights of 0, the last element is selected.
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

## Limitations

Weights are currently only used by default block selection, and will be ignored by custom selectors.