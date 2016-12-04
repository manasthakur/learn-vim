## Learn Vim - Module 2: BTW -- Buffers, Tabs, Windows

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module1.md)  |  [Next module](module3.md)

Module 1 is sufficient to get us started with vim.
This module starts expanding our vim-knowledge to help us work with _multiple files_.
This requires understanding the concepts of buffers, tabs, and windows.

### Buffers
A _buffer_ is a container that holds a file in vim.
Thus, opening a file is equivalent to loading it in a new buffer.

By default, vim requires us to save the current buffer before moving on to another one;
we can enhance the same to keep multiple unsaved buffers open at a time, using the following configuration in the vimrc:
```
set hidden    // allow multiple files to opened in different buffers, 'hidden' in the background
```

We can create a new buffer (with a new file) using the command:
```
:e file-name    // open a new file for editing
```
This hides the current buffer and reveals a new buffer with the specified file-name.

To _list_ all the currently open buffers, along with their _buffer-ids_ and the contained files, type the following:
```
:ls    // list buffers
```
Looking at these numbers (buffer-ids), we can _switch_ to different buffers as follows:
```
:b<buffer-id>    // :b2 will switch to the buffer with id '2'
```
In addition, the following shorthands can be used to switch to the next and the previous buffers (in the order specified in `:ls`):
```
:bnext  or  :bn    // switch to the next buffer
:bprevious  or :bp    // switch to the previous buffer
```

### Windows
_Windows_ are useful to view multiple files side-by-side, in a _split_:
```
:vsplit <file>  or  :vs <file>    // open file in a vertical split
:split <file> or :sp <file>    // open file in a horizontal split 
```

##### Extra dose:
If we don't supply the file-name to any of the above split commands, the current file itself is opened in the new split.
This allows us to view (and edit) different portions of the same file side-by-side!!
Awesome, right?
In fact, this feature (along with many others) was unique to Vim, and is now being implemented in many other text-editors and IDEs as well.

The following commands help in handling windows in normal mode (`<C-k>` means you have to press `Ctrl+k`):

* `<C-w>c` (or `:q`) -- close current window
* `<C-w>w` -- toggle among windows
* `<C-w>r` -- rotate the window-pattern
* `<C-w><arrow-key>` -- switch among windows

### Tabs
A _tab_ is a collection of windows.
Note that the concept of tabs is different from many other tools as in Vim, multiple tabs can be used to view the same file.
The common usage of tabs is to use one tab per project-specific layout.

A tab can be _created_ using:
```
:tabnew <file>    // Open file in a new tab
```
Similarly, the following commands can be used to _switch_ among tabs:
```
:tabnext    // next tab
:tabprevious    // previous tab
```
Vim makes it easy to _list_ all the open tabs by providing a *tabline* at the top, whenever more than one tab exists.
The current tab is highlighted using a different color.

A tab can be closed using `:q`.

##### Extra dose:
Similar to the tabline, Vim also provides a *statusline* at the bottom, which can be used to list various useful information, such as the current line-number, file-type, etc.
By default, the statusline is shown only when there are more than one buffers open.
To make the statusline _always visible_, add the following in your vimrc:
```
set laststatus=2    // always show the statusline
```

#### Endnote:
In this module, we learned about some powerful ways to work with multiple files in vim.
Believe me, many vim users do not understand the difference between buffers, tabs, and windows, and hence either get confused or don't use BTW at all.
In the next module, we will learn about some amazing features unique to Vim (read _Normal mode_) that make it the most popular text-editor in the world.

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module1.md)  |  [Next module](module3.md)

[Star this repository](https://github.com/manasthakur/learn-vim/) on GitHub if you like the tutorial.
[Follow me](https://twitter.com/manasthakur17) on twitter for updates.

