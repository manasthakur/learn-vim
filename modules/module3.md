## Learn Vim - Module 3: Being Normal

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module2.md)  |  [Next module](module4.md)

This is the module that introduces what makes Vim the most unique and amazing text-editor -- the _normal_ mode.

The Vim philosophy dictates that most of the _editing_ should be done in normal mode, not in insert mode (hence the name _normal_).
Vim makes this possible by introducing its own unique, flexible language.
Many of the letters in the Vim alphabet have several _contextual_ meanings.
Let us begin with some of them:

* `a`: around, append; `A`: append at the end of line
* `b`: beginning of word
* `c`: change (delete and switch to insert mode); `C`: change till the end of line
* `d`: delete; `D`: delete till the end of line
* `e`: end of current word
* `f`: find in current line
* `h`: alias to left arrow
* `i`: inside, switch to insert mode; `I`: insert at the beginning of line
* `j`: alias to down arrow
* `k`: alias to up arrow
* `l`: alias to right arrow
* `n`: next search item; `N`: `n` in reverse order
* `o`: open a new line below current line; `O`: open a new line above current line
* `p`: paste after the cursor position; `P`: paste before the cursor position
* `t`: till
* `u`: undo (`<C-r>` is for redo)
* `v`: visual mode; `V`: visual-line mode; `<C-v>`: visual-block mode
* `w`: next word
* `x`: cut
* `y`: yank (copy)

Some of the commands have a _two-letter_ combination.
For example:
* `dd` deletes the current line
* `cc` changes the current line
* `yy` copies the current line

Note: The above list is far from being comprehensive; we will keep learning Vim alphabets and their usage till the time we keep learning Vim.
Similar to learning any new language (programming or otherwise), learning Vim keystrokes and their usage takes time.
However, once mastered, it enables blazingly-fast editing, which cannot be achieved using any other editor.

Most of the normal-mode commands can be prefixed with a number `n` to perform them `n` times.
For example, `3dd` will perform the `dd` command 3 times; thus, deleting 3 lines at a shot!

We will now learn some common usage patterns of the Vim alphabet using example scenarios.
I strongly recommend you open your Vim and keep testing the same, in parallel.

| Requirement	                                | Command	        |
| --------------------------------------------- | ----------------- |
| Move 2 lines up	                            | `2k`	            |
| Move 10 lines down	                        | `10j`	            |
| Cut current letter	                        | `x`	            |
| Cut 5 letters	                                | `5x`	            |
| Jump to next word	                            | `w`	            |
| Delete till next word	                        | `dw`	            |
| Delete 2 words	                            | `2dw`	            |
| Delete current line	                        | `dd`	            |
| Delete 6 lines	                            | `6dd`	            |
| Copy current line	                            | `yy`	            |
| Copy 5 lines	                                | `5yy`	            |
| Change word	                        	    | `cw`	            |
| Delete till next _k_	                        | `dtk`	            |
| Delete including next _k_	                    | `dfk`	            |
| Change till next _"_	        	            | `ct"`	            |
| Delete the word inside which the cursor is	| `diw`	            |
| Delete inside parentheses	    	            | `di(` or `di)`	|
| Change inside quotation marks                 | `ci"`	            |
| Change around quotation marks	                | `ca"`	            |
| Delete till _;_	                            | `dt;`	            |
| Copy current word	                            | `yw`	            |
| Copy 4 lines	                                | `4yy`	            |
| Paste copied line below	                    | `p`	            |
| Paste copied line 5 times	                    | `5p`	            |

As there can be an infinitely large number of sentences formed with English alphabet, so can be using the Vim alphabet.
Keep practicing by asking you the question "Can I do this in Vim?", and then trying the combination that comes to your mind and observing the effect(s).
This will be a truly rewarding experience.

### Visual-mode
Vim offers a _visual_ mode to visually select regions of text, before applying a normal-mode command.
For example,

* `vw` followed by `y` selects till next word and copies selection.
* `vt"` followed by `d` selects till next _"_ and deletes the selection.

There is also a convenience `visual-line` mode that lets you select line-by-line.
For example,

* `V` (capital `V`) followed by `y` selects the current line and copies it.
* `V` followed by `2j` followed by `d` selects the current and the next two lines, and deletes them.

Further, there is a _visual-block_ mode (triggered using `<C-v>`) that lets select text vertically.
This is very helpful for deleting say a column in a table.
Just select the column visually and press `d`.
We will see how the visual-block mode can be used to _comment_ (and _uncomment_) your code in the next module.

##### Extra dose:
Vim provides an easy way to toggle the case of typed text.
We can use `~` (tilde) to toggle the case of a single character, or select some text (using visual-mode) and use `~` to toggle the case of the selection..

### Navigating faster with relative numbers
To use numerical values for, say, moving `k` lines down, we usually need to mentally count the number of lines.
However, in Vim 7.4+, there is a very useful option _relativenumber_, which can be set to explicitly see the line numbers relative to the current line.
To always use it, set the following in the vimrc file:
```vim
set relativenumber
```
To temporarily disable relative numbers in the current file, type:
```vim
:set norelativenumber
```

##### Extra dose:
* You can scroll down and up in Vim with `<C-f>` and `<C-b>`, respectively.
* You can jump to the beginning and end of a line with `0` (zero) and the `$` (dollar) keys, respectively.
Do you think now that `D` (in the alphabet listing above) is actually a shortcut for `d$`?

### Search-and-replace (in the current buffer)
Vim provides an easy way to search content in the current buffer (well, searching across buffers is also easy; we will learn it in the next module).
Type the following in normal mode:
```
/searchterm<CR>	    " search forwards
?searchterm<CR>	    " search backwards
*	                " search current word forwards
#	                " search current word backwards
```
After searching something, jump to the next and previous occurrences of the search-term using `n` and `N`, respectively.

Vim also provides a sophisticated mechanism to **replace** occurrences of a word in the current buffer:
```
:%s/oldword/newword/c	" replace one-by-one
:%s/oldword/newword/g	" replace all occurrences at once
```

To perform replacement within a block of text:

* First select the text using visual mode.
* `:s/oldword/newword/c` or `:s/oldword/newword/g`

Note that _oldword_ and _newword_ can even be regular expressions, thus opening a plethora of opportunities to ease searching and replacing.

The following option **highlights** all the occurrences of the searched word:
```vim
set hlsearch	" highlight searches
```
The search highlights can be cleared using `:nohlsearch` or `:noh`.

There is one more interesting option related to searching in Vim:
```vim
set incsearch	" highlight matches as you type
```
This option can be used to see which word(s) related to our search-term actually exist in the buffer.

### Pasting text from outside
We can paste text copied from outside Vim using the corresponding terminal emulator's keys for pasting:
`Command-V` for macOS, and `Ctrl-Shift-V` for Linux.
However, this may sometime randomly indent the pasted text (because of syntax-based indentation for the current file-type).
To avoid this, Vim provides a special _paste_ mode that can be enabled in such scenarios:
```vim
:set paste	    " enable paste-mode
:set nopaste	" disable paste-mode
```
I recommend you avoid setting paste-mode in your vimrc and use it only when you need (as paste-mode disables several indentation features).
We will learn how to _map_ keys to perform such small tasks in the next module.

### Simple is Powerful: The dot command
The most powerful (yet simple) command in Vim is the _repeat_ (or dot) command.
It can either be used to repeat the previous normal-mode command, or to repeat whatever you did in insert mode till you press the `<Esc>` key.
For example,

* `5dd` --> `.` will delete 10 lines.
* `/searchword` --> `cw` --> enter new word --> `<Esc>` --> `n` --> `.` will change first word, and its next occurrence.

Notice how much the dot command simplifies the repetition.
And we keep performing repetitive tasks all the time, isn't it?

#### Endnote:
In this module, we learned a plethora of tricks to make us adapt to the _Vim way_ of editing text.
Even though the learning curve is a bit steep, the joy that it will give you will be overwhelming.
In the next module, we will tighten our belts and learn how the coder-you-envy writes code at the speed of thought using Vim.
Till then, keep practicing.

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module2.md)  |  [Next module](module4.md)

[Star this repository](https://github.com/manasthakur/learn-vim/) on GitHub if you like the tutorial.
[Follow me](https://twitter.com/manasthakur17) on twitter for updates.

