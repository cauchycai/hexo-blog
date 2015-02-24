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

# The Mark and the Region #

When multiple windows show the same buffer, they can have *different values of point*, and thus different regions, but they all share *one common mark position*.

## Setting the Mark ##

C-SPC or C-@ => Set the mark at point, and activate it. (set-mark-command)

C-u C-SPC => jump to mark, and pop a new position for local mark ring

C-x C-x => (exchange-point-and-mark), this command is useful when you are satisfied with the position of point but *want to move the other end of the region*.

C-y set the mark at the other end of the inserted text, without activating it.

C-x C-p => (mark-page)

C-x h => (mark-whole-buffer)

## Operating on the Region ##

*C-x TAB* or C-M-\ => Indent region

C-w => Kill the region

M-w => Copy the region to the kill ring

C-x C-l or C-x C-r => Convert case (upcase-region) or (downcase-region)

C-u C-/ => Undo changes within a region

M-% => Replac text within a region

M-x fill-region => ??

## The Mark Ring ##

C-SPC C-SPC => Set the mark, pushing it onto the mark ring, without activating it.

C-u C-SPC => Move point to where the mark was, and restore the mark from the ring of former marks.

*Repeating C-u C-SPC cycles through the positions currently in the ring.*

*If you want to move back to the same place over and over, use a register instead.*

## The Global Mark Ring ##

C-x C-SPC => (pop-global-mark)

## Disabling Transient Mark Mode ##

transient-mark-mode can be toggled by M-x transient-mark-mode

# Killing and Moving Text #

## Deletion ##

Commands that erase text but do not save it in the kill ring are known as *delete* commands; their names usually contain the word 'delete'.

eg:
C-d (delete-char)
(delete-trailing-whitespace)

C-x C-o => (delete-blank-lines)

M-^ => Join two lines by deleting the intervening newline (delete-indentation)

(delete-duplicate-lines) , with C-u C-u, it only searches for adjacent identical lines.

## Killing ##

C-S-backspace => (kill-whole-line)

C-x DEL => Kill back to beginning of sentence (backward-kill-sentence)

M-k => Kill to the end of the sentence (kill-sentence)

M-w => (kill-ring-save)

If you change the variable kill-do-not-save-duplicates to a non-nil value, identical subsequent kill yield a single kill-ring entry, without duplication.

## Yanking ##

M-y => (yank-pop)

C-y => (yank)

C-u C-y => C-y + C-u C-SPC

M-y move the *"last yank" pointer* around the ring

C-M-w => (append-next-kill)

## Accumulating Text ##

M-x append-to-buffer

M-x prepend-to-buffer

M-x copy-to-buffer

M-x insert-buffer

M-x append-to-file

## Rectangles ##

Rectangle commands are useful with text in multicolumn formats

C-x r k => (kill-rectangle)

C-x r M-w => (copy-rectangle-as-kill)

C-x r d => (delete-rectangle)

C-x r y => (yank-rectangle)

C-x r o => (open-rectangle)

*C-x r N* => (rectabgle-number-lines)

C-x r c => (clear-rectangle)

C-x r t string RET => (string-rectangle)

C-x SPC => (rectangle-mark-mode)

# Registers #

Each register has a name that consists of a single character.

To view what register r contains:

M-x view-regitster RET r

Bookmarks record files and positions in them, so you can return to those positions when you look at the file again.

A register can store a *position*, a piece of *text*, a *rectangle*, a *number*, a *window configuration*, or a *file name*

## Saving Positions in Registers ##

*C-x r SPC* (r) => Record the position of point and the current buffer in register r (point-to-register)

*C-x r j* (r) => (jump-to-register)

## Saving Text in Registers ##

*C-x r s* (r) => Copy region into register r (copy-to-register)

*C-x r i* (r) => Insert text from register r (insert-register)

M-x append-to-register RET (r)

M-x prepend-to-register RET (r)

*C-x r +* (r) => (increment-register), which behaves differently for number and text

## Saving Retangles in Registers ##

C-x r r (r) => (copy-rectanble-to-register)

C-x r i (r) => (insert-register), if it contains a rectanble

## Saving Window Configurations in Registers ##

C-x r w (r) => (window-configuration-to-register), for the selected frame

C-x r f (r) => (frameset-to-register), for all frames

C-x r j (r) => to restore a window/frame configuration, the command is the same as restore a cursor position

## Keeping Numbers in Registers ##

This can be useful in keyboard macros

*C-u number C-x r n* (r) => Store _number_ into register r (number-to-register)

*C-u number C-x r +* (r) => If r contains a number, increment the number in that register by _number_

C-x r i (r) => Insert the number from register _r_ into the buffer

C-x r + with no numeric argument increments the register value by 1; C-x r n with numeric argument stores zero in the register.

## Keeping File Names in Registers ##

(set-register r '(file . _name_))

C-x r j (r) => visit the file

## Keyboard Macro Registers ##

*C-x C-k x* (r) => Store the last keyboard macro in register _r_ , (kmacro-to-register)

C-x r j (r) => To execute the keyboard macro in register _r_

## Bookmarks ##

Bookmarks record positions you can jump to, while unlike registers they have *long names*, and they persist from one Emacs session to the next.

*C-x r m RET* => Set the bookmark for the visited file, at point.

*C-x r m _bookmark_ RET* => Set the bookmark named _bookmark_ at point (bookmark-set)

*C-x r b _bookmark_ RET* => Jump to the bookmark named _bookmark_ (bookmark-jump)

*C-x r l* => List all bookmarks (list-bookmarks)

M-x bookmark-save


# Commands for Fixing Typos #

## Undo ##

*C-/* => (undo) or its aliases, C-_ or C-x u

When there is an active region, any use of undo performs _selective undo_

## Transposing Text ##

*C-t* => (transpose-chars)

M-t => (transpose-words)

C-M-t => (transpose-sexps)

C-x C-t => (transpose-lines)

## Case Conversion ##

*M-- M-l* => Convert last word to lower case.

*M-- M-u* => Convert last word to all upper case.

*M-- M-c* => Convert last word to lower case with *capital initial*