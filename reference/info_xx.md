# xx

The [xx file format](https://github.com/netspooky/xx) is a format I designed to make working with hex data easier.

It's a simple file format with just a few rules.

## Hex
The main data type is hex. Many popular hex representations are supported in xx.

```
41414141               -- This is the string "AAAA" in hex
42 42 42 42            -- This is the string "BBBB" in hex
0x43, 0x43, 0x43, 0x43 -- This is the string "CCCC" in hex
44h, 44h, 44h, 44h     -- This is the string "DDDD" in hex
$45, $45, $45, $45     -- This is the string "EEEE" in hex
0x46464646             -- This is the string "FFFF" in hex
FF:FF:FF:FF:FF:FF      -- This is a multicast mac address=
```

## Strings
Another data type is strings. These should be enclosed in quotation marks "like this".

```
"This is a string, a newline is the 0a after this" 0a -- A string with a new line.
```

## Binary
The final data type is binary numbers.

These are prefixed with "0y" and have 8 bits after. Multiple binary numbers can occur in a row, if you include a space between them.

```
0y10101010 0y01010101 -- This is 0xAA55
0y10101010 55         -- This is also 0xAA55
```

## Separators

Each element on a line of text should be separated with spaces.

```
4142"CD"0y010001010y01000110    -- Not valid
4142 "CD" 0y01000101 0y01000110 -- Becomes "ABCDEF"
```

## Comments

Comments are a key feature of xx. Many different comment styles are supported. Here is a list of them:

```
-- Lua Style
/* C multi-
line Style */
// C++ Style
# Python Style
; Nasm Style
% MATLAB, PDF 
| Pipes
┌─┬┐╔═╦╗╓╥  Any box drawing 
╖╒╤╕│║├┼┤╠  character can also
╬╣╟╫╢╞╪╡└┴  be used as a comment.
┘╚╩╝╙╨╜╘╧╛  Perfect for diagrams!
▀▁▂▃▄▅▆▇█▉▊▋▌▍▎▏ Any block element 
▐░▒▓▔▕▖▗▘▙▚▛▜▝▞▟ can also be used
```
For more info on box drawing characters, check here: https://en.wikipedia.org/wiki/Box-drawing_character

Comments essentially end the line of parsable hex data, so 

```
41414141 // Nothing after the two slashes is parsed
└──────┘ You can use box drawing characters to annotate hex data
```

## ANSI Escapes

ANSI escapes are another type of comment. This is the hex value "\x1b". This is used for ANSI colors and escapes to mark up comments and allow for more colorful diagrams.

I tend to use [8 bit ANSI codes](https://en.wikipedia.org/wiki/ANSI_escape_code#8-bit) because they don't rely on terminal settings, but it will require a 256 color terminal. Some terminals don't support this, such as your tty when you are on a non-graphical \*nix based system such as a Raspberry Pi. You can use the standard [3 or 4 bit ANSI colors](https://en.wikipedia.org/wiki/ANSI_escape_code#3-bit_and_4-bit) for that.

You can copy raw ansi escapes in Sublime Text and other editors. If you need one, this one liner will print the word "hey" in pink.

```
printf "\x1b[38;5;219mhey\n\x1b[0m"
#       │  ││        ││   ││  │└─┴── [0m resets to the default value
#       │  ││        ││   │└──┴───── \x1b is the escape code again
#       │  ││        │└───┴───────── This is "hey" with a new line
#       │  │└────────┴────────────── [38;5; tells the terminal it's using 256 color mode, and 219 is the color pink. "m" ends the escape
#       └──┴──────────────────────── \x1b is the escape code that tells the terminal a special sequence will come after.
```

## xx File Examples

The flyer for this workshop:

![image](https://user-images.githubusercontent.com/26436276/201207165-b4c5305b-16f9-4515-9e34-a45992346f18.png)

Release notes for xx v0.5

![image](https://user-images.githubusercontent.com/26436276/201207230-3a31f545-0db0-4418-925a-5d0b34ff4c24.png)

A skull

![image](https://user-images.githubusercontent.com/26436276/201207340-eefaf461-8361-4f40-be0d-0fc6c8217f4d.png)

An ELF binary

![image](https://user-images.githubusercontent.com/26436276/201207467-cefdb998-d1c2-42db-8540-992e18fc52a3.png)


