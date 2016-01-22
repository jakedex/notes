# Vim Notes

## Commands
* `.` repeats the last character
* `b` goes back a word
* `E`, and `W` jump to end of WORDS (group of letters separated by blank characters)
* `*` (resp. `#`) go to the next (resp. previous) occurence of the word under the cursor
* `y2/WORD` yank up to the occurrence of "WORD"
* `^` go to the first character on the line
* `f<character>` go to the next occurance of the `<character>` on the line, `,` finds the next
* `t<character>` go just before the `<character>`
* `F` and `T` work like their lowercase counterparts, but backward
* `dt<character>` delete everything until the <character>
* `D` deletes and copies to end of line (i.e. `d$`)
* *zone selection*: `<action>a<object>` inclusive, `<action>i<object>` exclusive
	* rectangular blocks: `<ctrl+v>`, `<shift+I>`, insert intended characters and `esc`
* `<ctrl+a>` increment number
* *Macros*: `qa` start recording to register `a`, `q` stop recording, `@a` replay the macro in register `a`, `@@` replay the last executed macro
* `J` join lines
* `<` and `>` indent lines, `=` auto-indent
* `V` visual line
* `:split` and `:vsplit`, `<ctrl+w+_>` maximize split, `<ctrl+w++>` grow split (`-`)

### Moving within the screen
* `H`: move to the top of the screen
* `M`: move to the middle of the screen
* `L`: move to the bottom of the screen
* `ctrl+E`: scroll up one line
* `ctrl+Y`: scroll down one line
* `ctrl+U`: move up half a page
* `ctrl+D`: move down half a page
* `ctrl+F`: move down a page
* `ctrl+B`: move up a page

### Basic change/insert options
* `I` insert at the beginning of the line
* `s` substitute from where you are to the next command
* `S` substitute the entire line

**Vim Primer - Advanced**
