# Overview

Notes on using **Regular Expressions**, both in general, and language/tool specific

# References

* [Interactive Tester](https://regexr.com/)

# Basics

## Special Characters

Note that since the following are special characters they must be escaped with a backslash if you want them to be part of the search criteria.

* **\\** -
* **^** - (carret) match occurances at the beginning of a string
* **$** - (dollar) match occurances at the end of a string
* **.** - (period) matches almost any character except line breaks
* **|** -
* **?** - (question) the proceeding character is optional
* **\*** -
* **+** -
* **\(** -
* **\)** -
* **\[** -
* **\{** -

# Character Classes

## Sets of characters

Use square brackes **\[\]** to match one character from a choice of characters.  Dashes (minus sign) are used to specify a range of characters.

* **\[ae\]** - matches either "a" or "e" as in **gr\[ae]y** which will match either gray or grey.
* **\[3-8\]** - matches a single digit between 3 and 8.
* **\[a-z\]** - match all lowercase letters
* **\[A-Z\]** - match all uppercase letters
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

## Match beginning and ending characters of a word

By combining a character match with the **\\b** word boundary you can match the beginning and ending characters of a word

* **\\be** - match all "e" characters at the beginning of a word
* **e\\b** - match all "e" characters at the end of a word

Note the similarity to

* **\\se** - match all "e" characters the beginning of a word that are proceeded by a whitespace (the white space is included in the match)
* **e\\s** - match all "e" characters at the end of a word followed by a whitespace which is also included in the match

but these don't match those words ending in punctuation rather than white space, it is also matching two adjacent characters (the word character and the whitespace)


# Match start and end of strings

* **^** - **^This** matches in "This is a test" since "This" is at the start of the string.
* **^** - **^test** does not match in "This is a test" since "test" is NOT at the start of the string.
* **$** - **test$** matches "This is a test" since the string ends with "test"
* Combined - **^Hi there$** matches the entire 'Hi there" string since it begins with "Hi" and ends with "there"


