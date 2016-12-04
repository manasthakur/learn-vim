##Learn Vim - Module 1: (Not just an) Intro

[Vim](http://www.vim.org/) is a command-line text editor, created by [Bram Moolenar](http://www.moolenaar.net/).
It stands for _Vi-IMproved_; _Vi_ was an older ubiquitous editor, which was enhanced to create Vim.

To open Vim, just type `vim` at the command-prompt.
Note that on most modern systems, `vi` is symlinked to `vim`.
However, just in case the symlink does not exist, I recommend typing the whole word `vim`.

To open a file in the beginning, type `vim file-name` at the command-prompt.
To open a file inside vim, type
```
:e file-name	// 'e' stands for 'edit'
```

Vim is a _modal_ text-editor.
That is, it has different modes to perform different tasks.
The major ones (for now) are:

* Normal (N) -- edit text
* Insert (I) -- type text
* Command (C) -- execute commands

The following diagram shows how to switch from one mode to the other:

![](../images/vim-modes.jpg =80x)

