# Regular expressions

Regular expressions (also know as regex) offer a powerful way to
process text in ways that regular searches cannot. Since code is nothing
but text, understanding how to use regular expressions to solve problems
both large and small can dramatically increase your productivity as a
programmer.

A regex pattern describes the text that you are looking for. For
instance, a pattern can describe words that begin with "C" and end in
"l". A pattern like this would match "Call", "Cornwall", and "Criminal"
as well as hundreds of other words.

What makes pattern searching counterintuitive at first is how you
describe the pattern. Consider the example above, where we want to
search for text that begins with the letter "C" and ends with the letter
"l" with any number of letters in between. What exactly do you put
between them that means "any number of letters"? That is what regular
expressions are all about.

## Usage

The following sections use the `grep` command to demonstrate how regular
expressions work. By default, `grep` prints any line from its input
stream that matches one or more regex patterns. The `-o` flag instructs
`grep` to print only the matching part of the lines.

Depending on your distribution, `grep` recognizes three different
versions of regular expression syntax: basic (BRE), extended (ERE), and
Perl-compatible (PCRE). The examples below use the extended syntax,
which is activated with the `-E` flag.

Alternatively, you can use a [regex debugger][regex101] to help you
build and test patterns interactively. All text editors worthy of the
name also allow you to search files using regular expressions.

[regex101]: https://regex101.com

## Writing search patterns

Regular expressions are composed of two types of characters. Special
characters that have different meanings in regular expressions are
called *metacharacters*, while the rest are called *literal*, or normal
text characters.

Most characters in a regex pattern match themselves. For instance, if
you are looking for the letter "t", `grep` stops and reports a match when
it encounters a "t" in the text:

```sh
$ echo tomato | grep -Eo t
t
t
```

The same thing happens with multiple literal characters:

```sh
$ echo tomato | grep -Eo mat
mat
```

This idea is so obvious that it seems not worth mentioning, but the
important thing to remember is that these characters *are* search
patterns. Very simple patterns, to be sure, but patterns nonetheless.

### Positional assertions

In addition to the simple character matching discussed above, there are
various special characters that have different meanings when used in a
regex pattern than in a normal search.

Probably the easiest metacharacters to understand are `^` (caret) and
`$` (dollar), which respectively represent the start and end of the line
of text as it is being checked. As we've seen, the regular expression
`cat` finds "cat" anywhere on the line, but `ˆcat` matches only if the
"cat" is at the beginning of the line. The `ˆ` is used to effectively
*anchor* the match of the rest of the regular expression to the start
of the line. Similarly, `cat$` finds "cat" only at the end of the line,
such as a line ending with "scat".

A common problem is that a regular expression that matches the word you
want can often also match where the "word" is embedded within a larger
word. For instance, the word `education` contains `cat`. In these cases,
we can use the metasequence `\b`, which represents a word boundary:

```sh
$ echo "education cat catapult" | grep -Eo "\bcat\b"
cat
```

Positional assertions are special in that they match a *position* in the
line rather than any actual text characters themselves.

### Character classes

Let's say you want to search for "grey", but also want to find it if it
were spelled "gray". The regular expression construct `[...]`, usually
called a character class, lets you list the characters you want to allow
at that point in the match. While `e` matches just an "e", and `a`
matches just an "a", the regular expression `[ea]` matches either.

Within a character class, the character-class metacharacter `-` (dash)
indicates a range of characters. `H[1-6]` is identical to `H[123456]`;
it matches "H1", "H2", "H3", etc.

If you use `[ˆ...]` instead of `[...]`, the class matches any character
that isn't listed. For example, `[ˆ1-6]` matches a character that's not
1 through 6. The leading `ˆ` in the class negates the list, so rather
than listing the characters you want to include in the class, you list
the characters you don't want to be included.

The metacharacter `.` (usually called dot or point) is a shorthand for a
character class that matches any character. It can be convenient when
you want to have an "any character here" placeholder in your expression.
For example, if you want to search for a date such as "03/19/76",
"03-19-76", or even "03.19.76", you could go to the trouble to construct
a regular expression that uses character classes to explicitly allow
"/", "-", or "." between each number, such as `03[-./]19[-./]76`.
However, you might also try simply using `03.19.76`.

### Metasequences

Regex patterns can include several other sequences for matching
different types or categories of characters.

`\s` matches any whitespace character (space, tab, carriage return, line
feed, form feed), while `\S` matches any non-whitespace character (any
character not included by `\s`).

`\w` matches any word character (a-z, A-Z, 0-9, _, and some 8-bit
characters), while `\W` matches any non-word character (all characters
not included by \w, including line breaks).

`\w` matches any digit (0–9), while `\W` matches any non-digit character
(including line breaks).

### Alternation

A very convenient metacharacter is `|`, which means "or". It allows you
to combine multiple expressions into a single expression that matches
any of the individual ones. For example, `Bob` and `Robert` are separate
expressions, but `Bob|Robert` is one expression that matches either.
When combined this way, the subexpressions are called *alternatives*.

Looking back to our `gr[ea]y` example, it is interesting to realize that
it can be written as `grey|gray`, and even `gr(a|e)y`. The latter case
uses parentheses to constrain the alternation. (For the record,
parentheses are metacharacters too.) Note that something like `gr[a|e]y`
is not what we want. Within a class, `|` is just a normal character.

### Quantifiers

Let's look at matching "color" or "colour". Since they are the same
except that one has a "u" and the other doesn't, we can use `colou?r` to
match either. The metacharacter `?` (question mark) means optional. It
is placed after the character that is allowed to appear at that point in
the expression, but whose existence isn't actually required to still be
considered a successful match.

Similar to the question mark are `+` (plus) and `*` (asterisk). The
metacharacter `+` means "one or more of the immediately-preceding item",
and `*` means "any number, including none, of the item".

### Escaping

One important thing we haven't discussed yet is how to actually match a
character that a regular expression would normally interpret as a
metacharacter. For example, if I searched for "ega.att.com" using
`ega.att.com`, it could end up matching something like "megawatt".
(Remember, `.` is a metacharacter that matches any character, including
a space.)

The metasequence to match an actual period is a period preceded by a
backslash: `ega\.att\.com`. The sequence `\.` is described as an
*escaped* period, and you can do this with all the normal
metacharacters, except in a character class.

## Resources

- [Jeffrey E.F. Friedl. Mastering Regular Expressions.](https://www.oreilly.com/library/view/mastering-regular-expressions/0596528124/)
- [GNU. Regular Expressions](https://www.gnu.org/software/grep/manual/html_node/Regular-Expressions.html)