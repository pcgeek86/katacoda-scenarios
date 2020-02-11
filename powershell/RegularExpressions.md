When you need to process arbitrary text, and search for patterns, there's arguably no better way to do it than regular expressions. While regular expressions are an advanced and often confusing topic, they are incredibly powerful. We'll look at the basics of regular expression matching here.

### Basic Text Matching

In the following example, we are looking for the pattern on the right-hand side of the `-match` operator, inside the string on the left-hand side of the `-match` operator. Because the string `I like bacon` contains the expression `ba`, the result is a boolean `$true`.

```
PS > 'I like bacon' -match 'ba'
True
```

### Matching the Start of a String

To match the beginning of a string, use the caret character in your regular expression `^`. Notice how the string that starts with `Hefeweizen` matches the regular expression `^hef`, but the string starting with `stouts` does not. You might also notice that by default, regular expressions are case-insensitive, meaning that `^hef` will match both `Hef` and `hef`.

```
PS > 'Hefeweizens are tasty beers.' -match '^hef'
True
PS > 'Stouts are tasty beers, but hefeweizens are my favorite.' -match '^hef'
False
```