# The vi Text Editor

## Opening and Closing Files

### Opening a File
```
$ vi file.txt
```

### Modus Operandi

There is *command mode* and *insert mode*.

Press the ESC key to force vi to enter command mode.

### Saving and Quitting a File

Without ex commands:

`ZZ` Quit and save edits

With ex commands:

`:w` to save your file but not quit

`:q` to quite if you haven't made any edits

`:wq` to both save your edits and quit (equivalent to `ZZ`)

## Quitting Without Saving Edits

`:e!` wipe out all edits you have made in a session and return to the original file

`:q!` wipe out your edits and quit

# Simple Editing

## vi Commands

`i` begin insert mode

ESC stop inserting text, move the cursor back one space and return to command mode

## Moving the Cursor

# Single Movements

`h` left, one space

`j` down, one line

`k` up, one line

`l` right, one space

### Numeric Arguments

`4l` == `llll`

### Movement Within a Line

`0`Move to beginning of line.

`$` Move to end of line.

### Movement by Text Blocks

`w` move cursor forward one word at a time (counting symbols and punctuation as words)

`W` move by word, not counting symbols and punctuation

`b` move cursor backward one word at a time (counting symbols and punctuation as words)

`B` move backward by word, not counting symbols and punctuation

numeric arguments also apply here

## Simple Edits

General form of vi commands:

(command)(number)(text object) (e.g. `d2w`)

(number)(command)(text object) (e.g. `2dw`)

### Appending Text

`a` insert text *after* the cursor rather than before

### Changing Text

`c` replace text

Combine `c` with a movement command to tell it how much text to change:

`cw` to the end of a word (also works on a portion of a word)

`c2b` back two words

`c$` to the end of line

`c0` to the beginning of line

`cc` replace the entire current line

`C` == `c$` replaces characters from the current position to the end of the line.

`r` replace a single character (pressing ESC is not necessary)

`s` replace a single character (or with a preceding count, replace multiple characters)

`S` change the whole line (deletes entire line, no matter where cursor is.  With preceding count, replace that many lines)

`R` replace text by simply entering overstrike mode: the characters you type replace what's on the screen until you type ESC.

### Changing Case

`~` change case of a letter

### Deleting Text

`dw` delete a word beginning where the cursor is positioned (space following word is deleted)

`de` delete, but retain space between words

`dE` delete to the end of a word, including punctuation

`dd` delete entire line that cursor is on

`D` == `d$` delete line from where the cursor is and stay in command mode?

`x` delete the character the cursor is on

`u` undo most recent command

`U` restore the line to its pristine state, the way it was before *any* changes were applied to it

### Moving Text

vi saves the last nine deletions in nine numbered buffers.  To restore for example the third deletion: `"3p`

`p` put the text that is in the buffer *after* the cursor position.

`P` put the text that is in the buffer *before* the cursor position.

### Copying Text

`y` copy the selected text into a special buffer

`yy` == `Y` yank an entire line

### Repeating or Undoing Your Last Command

`.` repeat the last editing command

`u` undo the last command

`U` undo all edits on a single line, *as long as the cursor remains on that line*

## More Ways to Insert Text

`A` Append text to end of current line.

`I` Insert text at beginning of line.

`o` Open blank line below cursor for text.

`O` Open blank line above cursor for text.

`s` Delete character at cursor and substitute text.

`S` Delete line and substitute text.

`R` Overstrike existing characters with new characters.

All of these commands place you in insert mode.

### Numeric Arguments for Insert Commands

`50i* ESC` inserts 50 asterisks

`25a*- ESC` appends 50 characters (25 pairs of asterisk and hyphen)

`ea` is useful for appending new text to the end of a word

## Joining Two Lines with J

`J` join two lines

## Review of Basic vi Commands


# Useful options

`:set wm=10` set a wrapmargin at 10 characters

`:set nu` to display line numbersxx
