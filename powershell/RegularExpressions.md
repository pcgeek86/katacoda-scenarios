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

### Match Results

The `-match` operator only tells you if there was or wasn't a match. It doesn't actually return the matched value. PowerShell has a special "automatic" variable called `$matches` that is populated after a successful `-match`. Let's take a look at how this works.

```
PS > 'Hello, my name is Trevor. Is your name Tyler?' -match '(T\w+)'
True
PS > $Matches

Name                           Value
----                           -----
0                              Trevor
```

You might have noticed that `Tyler` was not matched, even though it does match our regular expression. That's beacuse the `-match` operator only returns the first match.

### Multiple Matches

If you want to return _all_ of the matching elements in a string, there a couple of different methods. 

You can use the `Matches` method of the `System.Text.RegularExpressions.Regex` class, or you can use the built-in `Select-String` command. The `[regex]` nomenclature is a [PowerShell type accelerator](https://devblogs.microsoft.com/scripting/use-powershell-to-find-powershell-type-accelerators/) for the `System.Text.RegularExpressions.Regex` class, which simply requires less typing.

```
PS > $reg = [regex]'T\w+'
PS > $reg.Matches('Hello, my name is Trevor. Is your name Tyler?')
```

Here's how you would accomplish the same task using the `Select-String` command.

```
PS > $MatchList = Select-String -InputObject 'Hello, my name is Trevor. Is your name Tyler?' -Pattern 'T\w+' -AllMatches
PS > $MatchList.Matches
```

### References

https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/select-string
https://stackoverflow.com/questions/1703061/powershell-match-operator-and-multiple-groups
