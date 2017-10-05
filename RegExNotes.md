# Overview

Notes on using **Regular Expressions**, both in general, and language/tool specific

# References

* [Interactive Tester](https://regexr.com/)

# Basics

## Special Characters

Note that since the following are special characters they must be escaped with a backslash if you want them to be part of the search criteria.

* **\\** - (backslah) escape characters
* **^** - (carret) match occurances at the beginning of a string
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

# Character Classes

## Sets of characters

Use square brackes **\[\]** to match one character from a choice of characters.  Dashes (minus sign) are used to specify a range of characters.

* **\[ae\]** - matches either "a" or "e" as in **gr\[ae]y** which will match either gray or grey.
* **\[3-8\]** - matches a single digit between 3 and 8.
* **\[a-z\]** - match all lowercase letters
* **\[A-Z\]** - match all uppercase letters
* **\[A-Za-z\]** - match all letters
* **\[A-Z0-9\]** - match all uppercase letters and all single digits

## Character class shortcuts

* **\\d** - match a digit 0-9
* **\\w** - match a "word" character, an alphanumeric character plus the underscore.  Word boundaries are separated by whitespace.
* **\\s** - match a whitespace (space or tab)
* **\\D** - match if NOT a digit 0-9
* **\\W** - match if NOT a "word" character, an alphanumeric character plus the underscore.
* **\\S** - match if NOT a whitespace (space or tab)
* **\\s\\S** - match any character (matches whitespace or not whitespace, i.e. everything)

## Non-printable characters

* **\\n** - match the newline character
* **\\r** - match the carriage return (on Windows search for **\\r\\n**)
* **\\t** - match a horizontal tab

## Wildcard character matches

**.** - **gr.y** matches gray and grey, or any other character in the 3rd position
**.+** - **begin.+** matches a string starting with "begin" along with the remainder of the string, so for "The beginning of it all" it will select "beginning of it all"

## Match beginning and ending characters of a word

By combining a character match with the **\\b** word boundary you can match the beginning and ending characters of a word

* **\\be** - match all "e" characters at the beginning of a word
* **e\\b** - match all "e" characters at the end of a word

Note the similarity to

* **\\se** - match all "e" characters the beginning of a word that are proceeded by a whitespace (the white space is included in the match)
* **e\\s** - match all "e" characters at the end of a word followed by a whitespace which is also included in the match

although these don't match those words beginning/ending in punctuation rather than white space, it is also matching two adjacent characters (the word character and the whitespace) rather than just the single character as in the **\\b** examples above.

# Match start and end of strings

* **^** - **^This** matches in "This is a test" since "This" is at the start of the string.
* **^** - **^test** does not match in "This is a test" since "test" is NOT at the start of the string.
* **$** - **test$** matches "This is a test" since the string ends with "test"
* Combined - **^Hi there$** matches the entire 'Hi there" string since it begins with "Hi" and ends with "there"

# Match an entire word with optional characters (ex plural vs non-plural forms)

* **apples?** matches both apple and apples since the "s" is optional
* **colou?r** matches both color and colour
* **auto(mobile)?** - using optional groups of character we can match both "auto" and "automobile"

# Force the matching of an entire word

**test(ing|er|ed)?** - matches the entire word for "test", "testing", "tester", and "tested", but it will also make a partial match on "testee" since it matches "test" within "testee".  To force it to match only if it matches the whole word then do the following:

**test(ing|er|ed)?\\b** - the **\\b** makes sure it only matches if the match ends on the word boundary at the end, therefore it will not make the partial match on "testee" 

# Groups

Allows operations on a group of characters

* **test\(ing|er|ed)?** matches "test", "testing", "tester", "tested".  The "?" says all these endings are optional
* **\[A-Za-z0-9_\]+@\[A-Za-z0-9_\]+\.\(com|net|org\)** - match valid email address in com/net/org domains

Note the **+** (plus) matches one or more characters, causing it to apply to the entire segment of each part of the email address and not just the individual characters

# Quantifiers

* **+** - match one or more characters following the matched token.  **B\w+** matches "Bob", "Bonny" and "Bill", but not "B"
* **\*** - match zero or more characters following the matched token.  **B\w*** matches "Bob", "Bonny" and "Bill", and also matches "B"
* **\{\}** - match **\{3,4\}** if there are 3 to 4 characters in the word following the matched token.  **B\\w\{3,4\}** matches "Bill", "Bonny" and "Bobby", but doesn't match "Bob" since he only has two characters following the matched "B".

