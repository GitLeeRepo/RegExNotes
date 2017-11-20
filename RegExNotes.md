# Overview

Notes on using **Regular Expressions**, both in general, and language/tool specific

# References

* [Interactive Tester](https://regexr.com/)

# Basics

## Special Characters

Note that since the following are special characters they must be escaped with a backslash if you want them to be part of the search criteria.

* **\\** - (backslah) escape characters
* **^** - (carret) match occurances at the beginning of a string, or for negation when in a character set **\(\[\]\)**
* **$** - (dollar) match occurances at the end of a string
* **.** - (period) matches almost any character except line breaks
* **|** - (pipe) provide conditional "or"
* **?** - (question) the proceeding character is optional
* **\*** - (astricks) select zero or more characters
* **+** - (plus) select one or more characters
* **\(** - (open parenthesis) Begin group
* **\)** - (close parenthesis) End group
* **\[** - (open square bracket) begin character set
* **\{** - (open curly bracket) quantifier

## Expression Delimeters and global expression flag

In many environments the regular expression must be contained within two forward slash (**/**) delimiters, e.g. **/findme/**.  For simplicity the examples here do not include these delimiters.  In addition, if you want the expression to match multiple occurrances you would include the **g** global flag after the last delimiter, e.g. **/findme/g**.  Again, for simplicity in these examples this is not shown.

# Character Classes

## Sets of characters

Use square brackes **\[\]** to match one character from a choice of characters.  Dashes (minus sign) are used to specify a range of characters.

* **\[ae\]** - matches either "a" or "e" as in **gr\[ae]y** which will match either gray or grey.
* **\[3-8\]** - matches a single digit between 3 and 8.
* **\[a-z\]** - match all lowercase letters
* **\[A-Z\]** - match all uppercase letters
* **\[A-Za-z\]** - match all letters
* **\[A-Z0-9\]** - match all uppercase letters and all single digits

### Negation

Uses the carret symbol (**^**) within a character set to indicate anything but this set

* **\[^A-Z\]** - Match any character that is NOT a captial letter
* **\[^a-zA-Z\\.\]** - Match any character that is NOT a letter or a period

## Character class shortcuts

* **\\d** - match a digit 0-9
* **\\w** - match a "word" character, an alphanumeric character plus the underscore.  Word boundaries are separated by whitespace.
* **\\s** - match a whitespace (space or tab)
* **\\D** - match if NOT a digit 0-9
* **\\W** - match if NOT a "word" character, an alphanumeric character plus the underscore.
* **\\S** - match if NOT a whitespace (space or tab)
* **\\s\\S** - match any character (matches whitespace or not whitespace, i.e. everything)
* **\\b** - match a word boundary, either before a word or after a word
* **\\B** - match if NOT a word boundary

## Non-printable characters

* **\\n** - match the newline character
* **\\r** - match the carriage return (on Windows search for **\\r\\n**)
* **\\t** - match a horizontal tab

## Wildcard character matches

* **.** - (period) **gr.y** matches gray and grey, or any other character in the 3rd position
* **.+** - (period plus) **begin.+** matches a string starting with "begin" along with the remainder of the string, so for "The beginning of it all" it will select "beginning of it all"

## Match start and end of strings

* **^** (caret) - **^This** matches in "This is a test" since "This" is at the start of the string.
* **^** (caret) - **^test** does not match in "This is a test" since "test" is NOT at the start of the string.
* **$** (dollar) - **test$** matches "This is a test" since the string ends with "test"
* Combined - **^Hi there$** matches the entire 'Hi there" string since it begins with "Hi" and ends with "there"

## Match beginning and ending characters of a word

While the carret \(**^**\) and dollar sign **$** match the beginning of a string, it is often desireable to match the beginning or ending of words within the string. Where supported you can use the character class shortcuts **\\<** to match the beginning of a word and **\\>** to match the end of a word. Or use **\\b** which seems to be more widely supported.  For example, **grep** supports both **\b** and **\\< \\>** in default mode, but only the **\\b** notation in **-P** Perl mode.

Where supported:

* **\\<book** - will match "book" in "This textbook is a good book", but not the "book" in "textbook"
* **cat\\>** - will match "cat" in "In the cat and bobcat category", "cat" in "bobcat", but not the "cat" in "category"
* **\\<date\\>** - will match "date" in "In the latest update the date format was still dated" but not the "date" in "update" or "dated"

For wider support combining a character match with the **\\b** word boundary you can match the beginning and ending characters of a word

* **\\book** - as above matches "book" but not "textbook"
* **cat\\b** - as above matches "cat", but not "category", it would match the "cat" "bobcat" though
* **\\bdate\\b** - as above matches "date", but not "update" or "dated"

## Match an entire word with optional characters (ex plural vs non-plural forms)

* **apples?** matches both apple and apples since the "s" is optional
* **colou?r** matches both color and colour
* **auto(mobile)?** - using optional groups of character we can match both "auto" and "automobile"

# Groups

Allows operations on a group of characters, for example matching multiple forms of a word

* **test\(ing|er|ed)?** matches "test", "testing", "tester", "tested".  The "?" says all these endings are optional
* **\[A-Za-z0-9_\]+@\[A-Za-z0-9_\]+\\.\(com|net|org\)** - match valid email address in com/net/org domains
* **\\w+@\\w+\\.\(com|net|org\)** - same as email example above but using character class shortcuts insead

Note that the above email example handle simple emails of the form "name@company.domain", but not "first.last@divison.company.domain".  They also allow partial matches, so in the case of "first.last@company.domain" it will match "last@company.domain" which is of course wrong and not the actual email address this.  To address these issues a more complicate version is needed:

* **^\(\(\(\\w+\\.\)+\)?\\w+@\\w+\\.((\\w+\\.\)+\)?\(com|net|org\)\)$**

## Captured groups

Whenever you enclose a portion of the expression in parenthesis, by default you create a captured group that is part of the result.  In the [Interactive Tester](https://regexr.com/) app you access each capture group by **$#** where # is the group number from left to right, outer to inner.  The **^\(\(\(\\w+\\.\)+\)?\\w+@\\w+\\.((\\w+\\.\)+\)?\(com|net|org\)\)$** expression has 6 groups (just count the left parenthesis), with $6 containing the **\(com|net|org\)** capture group.

Captured groups can be used for extracting substrings from within the original result, or for creating back references (see below). 

## Capturing vs Non-Capturing groups

To prevent a group from being captured use **?:** immediately inside the group(s) you want to make non-capturing and they will be excluded.  So making two of the groups non-capturing in the prior expression now looks like **^\(\(?:\(\\w+\\.\)+\)?\\w+@\\w+\\.(?:(\\w+\\.\)+\)?\(com|net|org\)\)$**.  Now the the **\(com|net|org\)** capture group is $4 rather than $6.

As mentioned  captured groups can be used for extracting substrings or back references.  Use non-captured groups (with the **?:**) when you are only interested in grouping and not extracting substrings.

## Back references

Back references can be use to reference captured groups within the search itself which is useful for repeating patterns

* **B\(ill\) \(is\) \\1 and needs a p\\1 th\\2 morning** - uses **\\1** to reference the first **\(ill\)**  group and **\\2** to reference the second **\(is\)** group to match the entire string "Bill is ill and needs a pill this morning"
* **<\(\w+\)\(.+\)?>.+<\\/\\1>** - can be used to match opening and closing HTML/XML tags.  This will match `<h1 id="3">My Heading</h1>`, `<div>My Div...</div>`, and `<form method="POST"><input type="text"></form>`.  This is useful here since placing a **\\w+** on the end instead of the **\\1** would match any closing tag, not just the matching tag at the beginning.

## Language and environment support

As mention, the [Interactive Tester](https://regexr.com/) uses the **$#** format to identify the capture group.  This is also used in Perl, vi, sed & awk.

In JavaScript these captured groups are returned as part of the result array returned from the str.match(regExp) method.  The first (index zero) contains the entired matched result while indexes 1 through n contain the captured groups.  Other environments such as vi, sed and awk use **/#** after the expression to indicate which capture group number you want.

Python, Java, and C# use object notation (matchObj.Groups(#) in Java and C#) and matchObj.group(#) in Plython.

## Named capture groups

Depending on the environment you can have up to 99 capture groups, included **named capture groups** specified by **?<name>** in the group being named.

# Quantifiers

* **+** - match one or more characters following the matched token.  **B\w+** matches "Bob", "Bonny" and "Bill", but not "B"
* **\*** - match zero or more characters following the matched token.  **B\w*** matches "Bob", "Bonny" and "Bill", and also matches "B"
* **\{\}** - match **\{3,4\}** if there are 3 to 4 characters in the word following the matched token.  **B\\w\{3,4\}** matches "Bill", "Bonny" and "Bobby", but doesn't match "Bob" since he only has two characters following the matched "B".

# Application Support

## Unix/Linux commands

### grep

Note that many of the regular expressions using the syntax in these notes do not work in **grep** by default.  However, by providing the **-P** for Perl arguement they do work (from a handful of examples I tried).  For example:

```bash
grep -P '^## S(et|how) email$' GitCommandNotes.md
```

returns

```
## Set email
## Show email
```

While without the **-P** it returns nothing, and:

```bash
grep -P '^##?.+email$' GitCommandNotes.md
```

returns:

```
# Config global user and email
## Set email
## Show email
```

While again, without the **-P** it returns nothing


