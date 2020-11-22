# Matching an Email Regex

## Summary

This tutorial will break down the components of a regex, also known as a regular expression, of matching an email. Additionally, a brief tutorial on regular expressions is included to help iterate what each component is responsible for in a regex search.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Putting it all together](#putting-it-all-together)

## Regex Components

### Anchors

Anchors allow you to choose whether or not a regex matches the beginning or end of a string. For example:

* `^` - Matches at the 'start' of the string the regex pattern is applied to.
* `$` - Matches at the 'end' of the string the regex pattern is applied to.

### Quantifiers

Quantifiers specify how many instances of a character, group, or character class must be present in the input for a match to be found. For example:

* `x*` - 	
Matches the preceding item "x" 0 or more times. For example, /bo*/ matches "boooo" in "A ghost booooed" and "b" in "A bird warbled", but nothing in "A goat grunted".

* `x+` - 	
Matches the preceding item "x" 1 or more times. Equivalent to {1,}. For example, /a+/ matches the "a" in "candy" and all the "a"'s in "caaaaaaandy".

* `x?` - 	
Matches the preceding item "x" 0 or 1 times. For example, /e?le?/ matches the "el" in "angel" and the "le" in "angle."

If used immediately after any of the quantifiers *, +, ?, or {}, makes the quantifier non-greedy (matching the minimum number of times), as opposed to the default, which is greedy (matching the maximum number of times).

* `x{n}` - Where "n" is a positive integer, matches exactly "n" occurrences of the preceding item "x". For example, /a{2}/ doesn't match the "a" in "candy", but it matches all of the "a"'s in "caandy", and the first two "a"'s in "caaandy".

* `x{n,}` - Where "n" is 0 or a positive integer, "m" is a positive integer, and m > n, matches at least "n" and at most "m" occurrences of the preceding item "x". For example, /a{1,3}/ matches nothing in "cndy", the "a" in "candy", the two "a"'s in "caandy", and the first three "a"'s in "caaaaaaandy". Notice that when matching "caaaaaaandy", the match is "aaa", even though the original string had more "a"s in it.

### OR Operator

The 'Or' operater, also known as alternation, is the term in a regular expression that is actually a simple 'OR.' For example:

* `|` - Match a string that has any anterior characters followed by the characters on the left or right of the vertical bar.

* `[]` - Matches a string that has any characters without any characters within the brackets.

### Character Classes

Character classes distinguish kinds of characters such as, distinguishing between letters and digits. For example:

* `\d` - Matches a single character that is a digit.
* `\w` - Matches a word character (alphanumeric character plus underscore).
* `\s` - Matches a whitespace character (includes tabs and line breaks).
* `.` - Matches any character.

### Flags

Flags are optional parameters that we can add to a plain expression to make it search in a different way. For example:

* `g` - (global) - does not return after the first match, restarting the subsequent searches from the end of the previous match
* `m` - (multi-line) - when enabled ^ and $ will match the start and end of a line, instead of the whole string
* `i` - (insensitive) - makes the whole expression case-insensitive (for instance /aBc/i would match AbC)

### Grouping and Capturing

Grouping and Capturing. For example:

* `()` - Creates a capture group.
* `(?:)` - Disables the capturing group.
* `(?<>)` - Puts a name to the group.

### Bracket Expressions

Bracket Expressions are characters enclosed by a bracket matching any single character within the brackets. For example:

* `[]` - Matches a string.
* `[x-x]` - Matches a string.
* `[]%` - Matches the string inside the brackets before a `%` sign.
* `[^]` - Matches any string that has not a letter from within the brackets (negation of expression).

### Greedy and Lazy Match

Greedy and/or Lazy Matching are quantifies that expand the match as far as possible through the text. For example:

* `* + {}` -  Matches any character one or more times included inside < and >, expanding as needed.

### Boundaries

Boundaries perform a "whole words only" search. For example:

* `\b ` -  Represents an anchor like caret (it is similar to $ and ^) matching positions where one side is a word character (like \w) and the other side is not a word character (for instance it may be the beginning of the string or a space character)

* `\B` - Negotion of '\b' and matches all positions where \b doesn’t match and could be if we want to find a search pattern fully surrounded by word characters.

### Back-references

Back-references will look at the match found in the indicated capture group, and ensure that the location of the back reference matches exactly. For example:

* `([abc])\1 ` - Using \1 it matches the same text that was matched by the first capturing group.
* `([abc])([de])\2\1` - We can use \2 (\3, \4, etc.) to identify the same text that was matched by the second (third, fourth, etc.) capturing group.
* `(?<foo>[abc])\k<foo>` - We put the name foo to the group and we reference it later (\k<foo>). The result is the same of the first regex.

### Look-ahead and Look-behind

Look-ahead and look-behing matches everything, in any context, and then filter by context in the loop. For example:

* `d(?=r)` - Matches a 'd' only if is followed by 'r,' but 'r' will not be part of the overall regex match.
* `(?<=r)d` - Matches a 'd' only if is preceded by an 'r,' but 'r' will not be part of the overall regex match.

### Putting it all together

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{3})$/
```
* `/^` - Start of string, or start of line in multi-line pattern
* `([a-z0-9_\.-]+)` - will match for first word which can have `a-z`, `A-Z`, `0-9`, and the `_\.-` characters.
* `\@` - will match the special character `@`
* `([a-zA-Z0-9]+)` - will match the word that is the domain name after '@'
* `\.` - will match the `period (.)`.
* `[a-z\.]{2,6}` - will match the final last word of the email and include the top-level domain name (.com, .org, .info, .de, etc.).
* `$` - End of string, or end of line in multi-line pattern.

## Author

This Gist was created by, Vu Tang, who is currently a student attending a bootcamp class at UofA.

[Link to Github profile](https://github.com/vutanguofa)
