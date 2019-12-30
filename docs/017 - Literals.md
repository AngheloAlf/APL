# Literals

The following will be described with regex.

## Decimal literals

Base 10

`[0-9]+`

## Hexadecimal literals

Base 16

`0x[0-9a-fA-F]+`

## Octal literals

Base 8

`0o[0-7]+`

## Binary literals

Base 2

`0b[0-1]+`

## Floats literals

`[0-9]+\.[0-9]+`

`[0-9]+e[+|-][0-9]+`

`[0-9]+[0-9]+\.e[+|-][0-9]+`

## Imaginary literals

Basically a decimal or float literal with a `i` suffix.

`[0-9]+i`

`[0-9]+\.[0-9]+i`

`[0-9]+e[+|-][0-9]+i`

`[0-9]+[0-9]+\.e[+|-][0-9]+i`

## Complex literals

(Decimal or float literal) +|- (Imaginary literal)

## Character literals

Fits in a `char`.

`'([^\\'\n])'`

Or a escape sequence sorrounded by `'`

## Unicode character literals

- For 2byte representable codepoint.
  - `u16'.+'`
  - Fits in `int16`
  - e.g. `u16'貓'`, but not `u16'🍌'`

- For 4byte representable codepoint.
  - `u32'.+'`
  - Fits in `int32`
  - e.g. `u32'貓'` or `u32'🍌'`

Escape sequences also work. For example you may use `u32'\xf0\x9f\x8d\x8c'` or `u32'\360\237'`

## String literals

All strings literals all Unicode compatible and UTF-8 encoded.

Default
- `"[^"]"`

Raw literal
- `r"[^"]"`
- Escapes sequences are not escaped.
  - For example, `"\n"` is a string which contains only one character (the new line character). Meanwhile, `r"\n"` is a string which contains 2 characters, the `\` (backslash) and `n`.
- UTF-8 encoded.

## Bool literals

`true|false`


## Escape sequences

| Escape sequence | Description | Representation | Notes |
| --- | --- | --- | --- |
| `\'` | single quote | byte 0x27 in ASCII encoding |  |
| `\"` | double quote | byte 0x22 in ASCII encoding |  |
| `\\` | backslash | byte 0x5c in ASCII encoding |  |
| `\a` | audible bell | byte 0x07 in ASCII encoding |  |
| `\b` | backspace | byte 0x08 in ASCII encoding |  |
| `\f` | form feed - new page | byte 0x0c in ASCII encoding |  |
| `\n` | line feed - new line | byte 0x0a in ASCII encoding |  |
| `\r` | carriage return | byte 0x0d in ASCII encoding |  |
| `\t` | horizontal tab | byte 0x09 in ASCII encoding |  |
| `\v` | vertical tab | byte 0x0b in ASCII encoding |  |
| `\nnn` | arbitrary octal value | byte `nnn` | Numbers bigger than 255 (or `\nnn` > `\377`) will produce a compile time error |
| `\xnn` | arbitrary hexadecimal value | byte `nn` |  |
| `\unnnn` | universal character name | code point `U+nnnn` | Can only be used in 2bytes representable literals or bigger, and strings literals |
| `\Unnnnnnnn` | universal character name | code point `U+nnnnnnnn` | Can only be used in 4bytes representable literals or bigger, and strings literals |

Notes:
- For Unicode escape sequences: If a universal character name does not correspond to a code point in ISO/IEC 10646 (the range `0x0`-`0x10FFFF`, inclusive), or it is between the range of surrogate code points  `U+D800` - `U+DFFF`, inclusive), a compile-time error will be emitted.
