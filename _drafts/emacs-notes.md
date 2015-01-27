Emacs Manual Notes
==================

# C1. The Organization of the Screen #

## Point ##

1. If a buffer is displayed in multiple windows, each of those windows has its own value of point.

2. C-x = to show information of current *point*, and show the character after the *point* in hex.

# C2. Characters, Keys and Commands #

## Kinds of User Input ##

1. You can also type Meta characters using two-character sequences starting with ESC. eg., M-a equals to ESC a

## Keys ##

1. Prefix key; Complete key.

2. Typing the help character (C-h or F1) after a prefix key displays a list of the commands starting with that prefix. But ESC C-h is equivalent to C-M-h, so use ESC F1 instead.

## Keys and Commands ##

1. Emacs does not assign meanings to keys directly, instead, Emacs assigns meanings to named *commands*, and then gives keys their meanings by binding them to commands.

2. The name of a command is usually make of a few English words separated by dashes.

3. Internally, each command is a special type of Lisp function.

4. The bindings between keys and commands are recorded in tables called *keymaps*.

# Keyboard Macros #

1. Keyboard macros differ from ordinary Emacs commands in that they are written in the Emacs *command language* rather than in Lisp.

2. Press F3 to start defining a keyboard macro, press F4 to end the definition and save the macro.

3. C-u F3 to re-execute last macro, then append keys to its definition; C-u C-u F3 to append keys to the last macro without re-executing it.

4. (apply-macro-to-region-lines) to run th elast keyboard macro on *each line* that begins in the region.

5. Apply F4 with a numeric prefix 'n' to invoke the macro 'n' times; an argument of '0' repeats the macro indefinitely until some error occur or C-g typed.

6. Alternative key bindings: *C-x (* and *C-x )*, *C-x e* to execute it, and repeat it by *e*.

## Keyboard Macro Counter ##

1. Each keyboard macro has an associated counter which allowd you to insert a number into the buffer that depends on the number of times the macro has been called.

2. C-x C-k C-i (kmacro-insert-counter); C-x C-k C-c (kmacro-set-counter); C-x C-k C-a (kmacro-add-counter); C-x C-k C-f (kmacro-set-format);

## Executing Macros with Variations ##

1. C-x q in macro definition => When *this point* is reached during macro execution, ask for confirmation.

## Naming and Saving Keyboard Macros ##

1. C-x C-k n => naming the most recently defined keyboard macro

2. C-x C-k b => binding the most recently defined keyboard macro to a key sequence

3. *M-x insert-kbd-macro* => insert in the buffer a keyboard macro's definition, as Lisp code.

4. Generally, we use C-x C-k 0 through C-x C-k 9 and C-x C-k A through C-x C-k Z as key sequences for macro bindings. Then you only need to type in C-x C-k b 4 to bind C-x C-k 4.

## Editing a Keyboard Macro ##

1. C-x C-k C-e => Edit the last defined keyboard macro

2. C-x C-k e name RET => Edit a previously defined keyboard macro name

3. *C-x C-k l* => Edit the last 300 keystrokes as a keyboard macro

## Stepwise Editing a Keyboard Macro ##

1. *C-x C-k SPC* => (kmacro-step-edit-macro)

# Basic Editing Commands #

## Inserting Text ##

1. To insert a non-graphic character, or a character that your keyboard does not support, first quote it by typing C-q

- C-q followed by any non-graphic character, eg., C-q DEL inserts a literal 'DEL' character

- C-q followed by a sequence of octal digits, eg., C-q 1 0 1 B inserts 'AB'. To use decimal or hexadecimal instead of octal, set the variable read-quoted-char-radix to 10 or 16.

2. Alternatively, you can use the command C-x 8 RET (insert-char)

## Changing the Location of Point ##

1. M-g M-g or M-g g => Read a number n and move point to the beginning of line number n (goto-line).

2. M-g TAB => Read a number n and move to column n in the current line.

## Undoing Changes ##

1. *C-/* or *C-x u* or *C-_*, but in by config *C-x u* is bound to (undo-tree-visualize) instead of (undo-tree-undo)

## Find Out What a Key Sequence Does ##

1. *C-h k* (describe-key)

## Blank Lines ##

1. C-o => Insert a blank line after the cursor (open-line).

2. *C-x C-o* => Delete all but one of many consecutive blank lines (delete-blank-lines).

## Continuation Lines ##

1. Most commands that act on lines act on logical lines, not screen lines. Except for C-n and C-p.

2. You can make Emacs insert a newline automatically when a line gets too long, by using Auto Fill mode.

## Cursor Position Information ##

1. M-x what-line => Display the line number of point

2. M-x line-number-mode and M-x column-number-mode => Toggle atomatic display of the current line number or column number.

3. *M-=* => Display the number of lines, words, and characters that are present *in the region* (count-words-region).

4. *M-x count-words* => Display the number of lines, words, and characters that are present *in the buffer*. If the region is active, display the numbers for the region instead.

5. *C-x =* => (what-cursor-position)

6. M-x hl-line-mode => Enable or disable highlighting of the current line.

7. *M-x size-indication-mode* => Toggle automatic display of the size of the buffer.

## Numeric Arguments ##

1. Some commands interpret the argument as a repetition count, eg., C-u 3 C-f

2. M-digit command => Repeat command digit times.

3. If you enter more than one digit, you need to hold down the META key for the second and subsequent digits.

4. C-u digit command => equivalent to M-digit command

5. C-u alone has the special meaning of "four times"; C-u C-u multiplies it by sixteen.

## Repeating a Command ##

1. *C-x z (repeat)* => This command repeats the previous Emacs command; the second and subsequent repeatings can be invoked by simplly input 'z'

# Searching and Replacement #

## Basics of Incremental Search ##

1. C-s (isearch-forward)

2. C-r (isearch-backward)

3. When you are satisfied with the place you have reached, type RET, this stops searching, leaving the cursor where the search brought it.

4. When you exit the invremental search, *it adds the original value of point to the mark ring*, without activating the mark; you can thus use C-u C-SPC to return to where you were before beginning the search.

5. After exiting a search, you can search for the same string again by typing just C-s C-s

6. To *reuse earlier search strings*, use the search ring. The commands M-p and M-n move through the ring to pick a search string to reuse.

7. *M-e* to edit the current search string in the minibuffer.

8. If the search string was mistyped, you can type *C-g* to remove from the search string the chracters that could not be found.

9. *lax space matching* => each space, or sequence of spaces, matches *any sequence of one or more spaces* in the text.

## Regular Expression Search ##

1. *C-M-s* => Begin incremental regexp search (isearch-forward-regexp).

2. *C-M-r* => Begin reverse incremental regexp search (isearch-backward-regexp).

## Query Replace ##

1. *M-%* => Replace some occurences of string with newstring.

2. *C-M-%* => Replace some matches for regexp with newstring.

3. The charaters you can type when you are shown a match for the string or regexp:

SPC => to replace the occurence with newstring.

DEL => to skip to the next occurence without replacing this one.
,   => to replace this occurrence and display the result and then you are asked for another input character to say what to do next. C-r to alter the replaced text; C-x u to undo the replacement. Since this exits the query-replace, so you must use *C-x ESC ESC RET* to do further replacement.

RET => to exit without doing any more replacements.

.   => to replace this occurrence and then exit without searching for more occurrences.

!   => to replace all remaining occurrences without asking again.

# The Minibuffer #

## Minibuffer History ##

M-p => Move to previous item in the minibuffer history

M-n => Move to next item in the minibuffer history

M-r regexp RET => (previous-matching-history-element)

M-s regexp RET => (next-matching-history-element)

## Repeating Minibuffer Commands ##

C-x ESC ESC => Re-execute a recent minibuffer command

M-x list-command-history => Display the entire command history

# Running Commands by Name #

M-x command RET => Run a command by name (execute-extended-command)

# Help #

C-h e => Display \*Messages\* buffer

C-h w command RET => Show which keys run the command named _command_ (where-is)

C-h F command RET => (Info-goto-emacs-command-node)

C-h C-h => (help-for-help)

C-h b => Display all active key bindings

C-h C-f => Display the Emacs FAQ, using Info

C-h f function RET => (describe-function)

C-h c key => (discribe-key-briefly)

C-h d topics RET => Display the commands and variables whose documentation matches topics (apropos-documentation)

C-h r => Display the Emacs manual in Info (info-emacs-manual)

C-h C-t => Display the Emacs to-do list
