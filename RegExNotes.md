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
* **.** -
* **|** -
* **?** -
* **\*** -
* **+** -
* **\(** -
* **\)** -
* **\[** -
* **\{** -

# Character Classes

Use square brackes **\[\]** to match one character from a choice of characters.  Dashes (minus sign) are used to specify a range of characters.

* **\[ae\]** - matches either "a" or "e" as in **gr\[ae]y** which will match either gray or grey.
* **\[3-8\]** - matches a single digit between 3 and 8.
* **\[a-z\]** - match all lowercase letters
* **\[A-Z\]** - match all uppercase letters
* **\[A-Z0-9\]** - match all uppercase letters and all single digits
