# Regular Expressions
#topic
#concept
**Related:**
-  [[Textbook Regular Expressions]]
-  [[Ruby#Regular Expressions in Ruby]]

---

Special language for efficient string comparisons
- letter at the end of the slashes indicates something. i is case-insensitive 

==Regular expression (RE):== a language for specifying text search strings. An algebraic notation for characterizing a set of strings. 
==Pattern:== what you search for
==Corpus:== what you search in

- Case-sensitive
- By default, uses greedy matching: matches as much of a sequence as possible

## Characters

| Character                 | Function                                                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `/`                       | Indicates RE                                                                                                           |
| `[ ]` Disjunction         | Disjunction of characters to match. **Ex: ✏** `/[wW]oodchuck/` specifies **either** woodchuck or Woodchuck.                  |
| `[a-z]`                   | Specifies a range within a well-defined sequence, inclusive                                                            |
| `[^x]`                    | When caret is the first character after the bracket, specifies anything other than the next RE                         |
| `?`                       | Either zero or one instances of the preceding character/RE            |
| `*`                       | Zero or more occurrences of the previous character/RE. **Ex: ✏** `/[ab]*/` specifies zero or more (a or bs) |
| `+`                       | Specifies one or more occurrences of the previous character or RE                                                      |
| `.`                       | Wildcard that matches any single character (except a carriage return?)                                                 |
| `^` Start of line anchor  | Specifies the proceeding RE must come at the beginning of the line                                                     |
| `\$` End of line anchor   | Specifies the preceding RE must come at the end of the line                                                            |
| `\b` Word boundary anchor | Must come at a boundary of a word. Can be at the end or front. Words are generally specified by spaces                 |
| `\B` Non-word boundary    |                                                                                                                        |
| `/` Escape character      | Use to cancel out special chars                                                                                        |
| \| Disjunction operator  | Either one RE or another. **Ex: ✏** `/gupp(y|ies)` matches guppy and guppies                                                 |
| `*?` Kleene star          | Matches as little text as possible                                                                                     |
| `+?` Kleene plus          | Matches as little text as possible                                                                                     |
| `{1}`                     | Matches a specific number of occurrences of the preceding RE                                                           |
| `{n, m}`                  | Matches a number of occurrences between n and m                                                                         |
| `{n,}`                    | Matches at least n occurrences                                                                                                                        |

### Character Sets

| Character Alias | Set                         |
| --------------- | --------------------------- |
| `\d`            | any digit                   |
| `\D`            | any non-digit               |
| `\w`            | any alphanumeric/underscore |
| `\W`            | a non-alphanumeric          |
| `\s`            | whitespace                  |
| `\S`            | non-whitespace                            |

### Operator precedence hierarchy
1. `()` Parentheses
2. `* + ? {}` Counters
3. `the ^my end$` Sequences and anchors
4. `|` Disjunction

Ex: `/the*/` matches theeee but not thethe because counters takes precedence over sequences

## Substitution
Allows a string characterized by a RE to be replaced by another string

`s/RE/replacement`


## Capture groups
A way to store and represent the values that matches the pattern. Every time a capture group (parentheses surround the pattern) is used, the resulting match is stored in a numbered register that can be accessed by a backslash and the number. If you want to use parentheses for grouping but not capture it to a register, start the parentheses with `?:` like `/(?: whatever)/`

**Ex: ✏**  Find an integer and put angle brackets around it
`s/([0-9]+/<\1>/`

The `\1` refers to the first matching substring 

**Ex: ✏** See if something occurs two times in a string
`/the (.*)er they were, the \1er they will be/`
*Checks if what is found at the first place is what appears where they `\1` is*

## Lookahead assertions
Uses `(?` syntax
**Ex: ✏**  To match, at the beginning of a line, ,any single word that doesn't start with volcano
`/^(?!Volcano)[A-Za-z]+/`