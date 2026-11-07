**Opening and finding files**

|Keys|Action|
|---|---|
|`Space Space` or `Space f f`|Fuzzy find files in the project|
|`Space f r`|Recent files|
|`Space /`|Live grep (search text across the project)|
|`Space e`|Toggle the file tree (explorer)|
|`Space f b` or `Space ,`|Switch between open buffers|
|`:e path/to/file`|Open a file by path (Tab completes)|

**File tree (once it’s open)**

|Keys|Action|
|---|---|
|`j` / `k`|Move down / up|
|`Enter`|Open file or expand folder|
|`a`|Create a new file (end with `/` for a folder)|
|`d` / `r` / `c` / `m`|Delete / rename / copy / move|
|`?`|Show all tree keybinds|
|`q`|Close the tree|

**Buffers (open files)**

|Keys|Action|
|---|---|
|`Shift h` / `Shift l`|Previous / next buffer|
|`Ctrl ^` (or `Ctrl 6`)|Jump back to the last file|
|`Space b d`|Close the current buffer|
|`Space b o`|Close all other buffers|

**Splits and windows**

|Keys|Action|
|---|---|
|`Space -` / `Space \|`|Split horizontally / vertically|
|`Ctrl h/j/k/l`|Move between splits|
|`Space w d`|Close the current split|
|`Ctrl w =`|Equalize split sizes|

**Moving inside a file**

|Keys|Action|
|---|---|
|`gg` / `G`|Top / bottom of the file|
|`{number}G`|Go to a line number|
|`w` / `b` / `e`|Next word / previous word / end of word|
|`0` / `^` / `$`|Line start / first character / line end|
|`{` / `}`|Previous / next blank line (paragraph)|
|`%`|Jump to the matching bracket|
|`Ctrl d` / `Ctrl u`|Half page down / up|
|`/text` then `n` / `N`|Search, next / previous match|
|`f{char}` / `;`|Jump to a character on the line, repeat|
|`s{2 chars}`|Flash jump: type two letters, press the label shown|

**Code navigation (the ones you’ll use while debugging)**

| Keys                | Action                                          |
| ------------------- | ----------------------------------------------- |
| `g d`               | Go to definition                                |
| `g r`               | Show references                                 |
| `K`                 | Hover docs for the symbol                       |
| `Ctrl o` / `Ctrl i` | Jump back / forward through your jump history   |
| `Space s s`         | Search symbols (functions, classes) in the file |
| `] d` / `[ d`       | Next / previous diagnostic (error)              |
**Fastest way to build the habit:** learn `Space Space`, `Space /`, `Shift h/l`, `g d`, and `Ctrl o` first. Those five cover most daily navigation. Press `Space` and wait a second, and LazyVim shows a popup (which-key) listing every available follow-up key, so you can discover the rest without memorizing.