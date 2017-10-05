# Overview

Notes on using **Regular Expressions**, both in general, and language/tool specific

# References

* [Interactive Tester](https://regexr.com/)

# Basics

## Special Characters

Note that since the following are special characters they must be escaped with a backslash if you want them to be part of the search criteria.

* **\\** -
* **^** -
* **$** -
* **.** - (period) matches almost any character except line breaks
* **|** -
* **?** -
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

## Non-printable characters

* **\\n** - match the newline character
* **\\r** - match the carriage return (on Windows search for **\\r\\n**)
* **\\t** - match a horizontal tab

## Wildcard character match

**.** - **gr.y** matches gray and grey, or any other character in the 3rd position

## Match start and end of strings

* **^** - **^T** matches "This is a test" since "T" is at the start, but **^t** won't match since the "t" in "test" is not at the start
* **$** - **$t** matches "This is a test" since the string ends with a "t"


