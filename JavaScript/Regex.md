# Regex

| pattern      | description               |
| ------------ | ------------------------- |
| ¸?\*+{#}     | quantifiers               |
| [...]        | charachter ranges         |
| \s           | shorthand character codes |
| (..&#124;..) | grouping and alternation  |
| ^...$        | anchors                   |
| i            | modifiers                 |

## pitfalls

- backspace, literally backspace
- [A-z] it will also catch parentheses because it follows the "unicode" table A,B,C...Z,[,],{...a,b...z
  - the parentheses are in between, so they will also be taken
- [0-9] != [9-0]

## repetation quantifiers

- ? -> zero or one times
- \* -> zero or more times(unlimited)
- \+ -> one or more times(unlimited)

## order of alternations

- PCRE
  - left-most, first match
- POSIX
  - left-most longest match
  - with multiple choices left one is that we most desire but it shouldn't block others
