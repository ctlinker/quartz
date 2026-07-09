---
title: Regex Cheatsheet
tags:
  - cheatsheet
publish: true
---
# Regular Expressions (Regex) Cheat Sheet

> A **Regular Expression (Regex)** is a pattern used to search, validate, extract, or replace text.

Example:

```regex
\d+
```

Matches one or more digits.

---

# Literal Characters

Most characters match themselves.

|Regex|Matches|
|---|---|
|`cat`|`cat`|
|`hello`|`hello`|
|`.`|Any character (except newline by default)|
|`\.`|A literal `.`|
|`\*`|`*`|
|`\\`|`\`|

---

# Character Classes

Match one character from a set.

|Regex|Meaning|
|---|---|
|`[abc]`|`a`, `b`, or `c`|
|`[a-z]`|Lowercase letters|
|`[A-Z]`|Uppercase letters|
|`[0-9]`|Digits|
|`[A-Za-z]`|Letters|
|`[A-Za-z0-9]`|Alphanumeric|
|`[^abc]`|Anything except `a`, `b`, or `c`|
|`[^0-9]`|Not a digit|

---

# Shorthand Character Classes

|Regex|Meaning|
|---|---|
|`.`|Any character|
|`\d`|Digit (`0-9`)|
|`\D`|Not a digit|
|`\w`|Word character (`a-zA-Z0-9_`)|
|`\W`|Not a word character|
|`\s`|Whitespace|
|`\S`|Non-whitespace|

---

# Quantifiers

Control how many times something appears.

|Regex|Meaning|
|---|---|
|`*`|0 or more|
|`+`|1 or more|
|`?`|0 or 1|
|`{3}`|Exactly 3|
|`{2,5}`|Between 2 and 5|
|`{3,}`|3 or more|
|`{,5}`*|Up to 5 (not supported everywhere)|

Examples

```regex
a*
```

```
"", "a", "aa", "aaa"
```

```regex
\d{4}
```

Matches

```
2026
1984
0001
```

---

# Greedy vs Lazy

By default, quantifiers are **greedy**.

```regex
<.*>
```

Matches

```
<div>Hello</div>
```

as one match.

Lazy quantifiers stop as soon as possible.

```regex
<.*?>
```

Produces

```
<div>
</div>
```

---

# Anchors

Anchors match positions instead of characters.

|Regex|Meaning|
|---|---|
|`^`|Beginning of line/string|
|`$`|End of line/string|
|`\A`|Beginning of string|
|`\Z`|End of string|
|`\b`|Word boundary|
|`\B`|Not a word boundary|

Example

```regex
^\d+$
```

Matches

```
12345
```

But not

```
abc123
```

---

# Alternation

Equivalent to OR.

```regex
cat|dog
```

Matches either

```
cat
```

or

```
dog
```

---

# Groups

## Capturing Group

```regex
(\d+)
```

Stores the match.

Example

```
2026
```

Group 1

```
2026
```

---

## Non-Capturing Group

```regex
(?:cat|dog)
```

Useful when grouping without creating a capture.

---

## Named Groups

Syntax depends on the regex engine.

Python

```regex
(?P<year>\d+)
```

JavaScript

```regex
(?<year>\d+)
```

---

# Backreferences

Reuse a previously captured group.

```regex
(\w+)\s+\1
```

Matches

```
hello hello
```

Does not match

```
hello world
```

---

# Lookarounds

Lookarounds test context without consuming characters.

## Positive Lookahead

```regex
\d+(?=€)
```

Matches

```
50
```

inside

```
50€
```

---

## Negative Lookahead

```regex
\d+(?!€)
```

Matches numbers **not** followed by `€`.

---

## Positive Lookbehind

```regex
(?<=\$)\d+
```

Matches

```
100
```

inside

```
$100
```

---

## Negative Lookbehind

```regex
(?<!\$)\d+
```

Matches numbers **not** preceded by `$`.

---

# Escaping Special Characters

Characters with special meaning must be escaped.

```
.
+
*
?
[
]
(
)
{
}
\
^
$
|
```

Example

```regex
\.
```

Matches

```
.
```

---

# Flags

Flags modify regex behavior.

|Flag|Meaning|
|---|---|
|`i`|Ignore case|
|`g`|Global search|
|`m`|Multiline|
|`s`|Dot matches newline|
|`u`|Unicode|
|`x`|Ignore whitespace/comments (engine dependent)|

Example

```regex
/hello/gi
```

---

# Common Patterns

## Integer

```regex
^-?\d+$
```

---

## Decimal Number

```regex
^-?\d+(\.\d+)?$
```

---

## Email

```regex
^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$
```

---

## URL (Simple)

```regex
https?://\S+
```

---

## Hex Color

```regex
^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$
```

---

## IPv4

```regex
^(\d{1,3}\.){3}\d{1,3}$
```

---

## Date (YYYY-MM-DD)

```regex
^\d{4}-\d{2}-\d{2}$
```

---

## Time (HH:MM)

```regex
^\d{2}:\d{2}$
```

---

## Whitespace

```regex
\s+
```

---

## Remove Multiple Spaces

Search

```regex
\s+
```

Replace

```
(space)
```

---

## Extract Words

```regex
\w+
```

---

## HTML Tags

```regex
<[^>]+>
```

---

# Regex Engine Differences

Not all regex engines support the same features.

|Feature|JS|Python|PCRE|Rust|
|---|:-:|:-:|:-:|:-:|
|Lookahead|✓|✓|✓|✓|
|Lookbehind|✓ (modern)|✓|✓|✗|
|Named Groups|✓|✓|✓|✓|
|Backreferences|✓|✓|✓|✗|
|Atomic Groups|✗|✗|✓|✗|

Always check your language's regex engine documentation before using advanced features.

---

# Most Useful Tokens

```text
.          Any character

\d         Digit

\w         Word

\s         Whitespace

^          Start

$          End

[]         Character class

[^]        Negated class

()         Capturing group

(?:)       Non-capturing group

|          OR

*          0+

+          1+

?          Optional

{n}        Exactly n

{m,n}      Range

\b         Word boundary

\1         Backreference

(?=)       Lookahead

(?! )      Negative lookahead

(?<=)      Lookbehind

(?<!)      Negative lookbehind
```

---

# Example

Extract the filename and extension:

Input

```
archive.tar.gz
```

Regex

```regex
^(.+)\.([^.]+)$
```

Result

|Group|Value|
|---|---|
|1|`archive.tar`|
|2|`gz`|

This illustrates how groups can capture different parts of a string for later use.