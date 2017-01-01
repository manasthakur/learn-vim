## Learn Vim - Module 6: That's not all, Folks!

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module5.md)

A very Happy New Year (2017) to all the readers!
This is the concluding module of this tutorial.
The aim here is to touch upon some advanced concepts, and introduce you to some
good practices.
At the end, I will list some resources for further learning and troubleshooting.

### Registers
Vim consists of a lot many registers for temporary storage (remember your
microprocessor classes?).
Registers are used to store something that you yank (copy),
to store jump-locations,
to store your search-terms,
and so on.
All the alphabets, numbers and some more special characters are registers in
Vim. See `:help registers` for an exhaustive list.

We will cover two uses of registers: _marks_ and _macros_.

#### Marks
You can _mark_ a location in Vim so that you can jump back to it.
The syntax to mark a location is `m<register>`, and to get back to that mark is
`'<register>`.

Let's say you are at line 10 in a file foo, and then suddenly recall that you
have to edit something in a file bar.
You can mark your location in register `k` as follows (in normal mode):
```
mk	" Mark the current location in register k
```

That's it. You won't _see_ anything happen.
Now when you want to go back to the marked location (from the same or any other
buffer), press:
```
'k	" Jump to the location marked in the register k
```
See the magic!

#### Macros 
Macros are one of the best time-savers of Vim.
You can _record_ any key-sequence into a register by typing the sequence once
between `q<register>` and `q`, and then _play_ the sequence using `@<register`.

Let's consider an example scenario.
Say you have a big file consisting of several lines that look like this:
```
A sample line of sample text.
Another sample line of sample text.
Yet another sample line of sample text.
...
```

Say, you want to change the first occurrence of 'sample' in each line to
'simple'.
Reckon that you cannot replace all occurrences using `%s`, as there are some
occurrences that you don't want to replace.
For the first line, you can achieve the same using `0fscwsimple<Esc>:w<CR>`.
Then you realize that you can actually use the same key-sequence for other lines
as well.
Scope for macros!
Do the following:
1. Start recording the macro in register `k`:
```
qk
```
2. Type the key-sequence for the first line:
```
0fscwsimple<Esc>:w<CR>
```
3. End the recording:
```
q
```
4. Go to next line:
```
j
```
5. Play the macro:
```
@k
```
Enjoy!

##### Extra dose:
You can play the previously-recorded macro (in whichever register) using `@@`. 

### Autocommands 
Autocommands allow us to specify command(s) that we wish Vim to perform
_automatically_ when an _event_ happens.
For example, say you want spell-check to be enabled by default when you open a
markdown file.
You can put the following autocommand into your vimrc:
```vim
augroup VIMRC
	autocmd!
	autocmd FileType markdown setlocal spell 
END
```
Notice that we have written the autocommand in a group (using `augroup VIMRC ...  END`).
This and the first line (`autocmd!`) are used to flush the autocommands for a
particular group when you reload your vimrc.
Otherwise, you will end up having multiple copies of the same autocommand.

The autocommand tells Vim to enable spell-check locally for the current buffer
when a markdown file is loaded.
See `:help autocommand-events` for an exhaustive list of events that your
version of Vim supports. 

### Colorschemes 
Bored of the default look of your favorite editor?
Vim can be made to look entirely different by using colorschemes.
To change the default colorscheme to something else, use the following command:
```vim
colorscheme <TAB>
```
This gives you a list of colorschemes (keep pressing tab);
you can press Enter and make the one you like permanent by adding the following
line to your vimrc:
```vim
colorscheme theme-name
```

Vim provides another option called `background` (possible values: `light` or
`dark`) that is used to choose colors that look good on a dark or a light
background. You can set it as follows:
```vim
set background=dark		" other option: light
```

[Solarized](https://github.com/altercation/vim-colors-solarized) is an extremely
popular low-contrast colorscheme that is available in dark as well as light
variations, and is easy on your eyes.

There is also a [colorscheme pack to rule them
all](https://github.com/flazz/vim-colorschemes) that packages a large number of
colorschemes in a single plugin.

Your beloved author also maintains two customized colorscheme plugins based on
his tastes:
[vim-solarized](https://github.com/manasthakur/vim-solarized)
and
[vim-seoul](https://github.com/manasthakur/vim-seoul). 

### Vim directory hierarchy 
Have you ever wondered where how does Vim load your plugins?

Vim recognizes a special directory called `.vim` (hidden) in your home
directory (`~`).
You can put your `.vim` files inside a predefined hierarchy inside the .vim
directory in order to get them loaded automatically.

The .vim directory may include the following sub-directories (apart from some others):
* __plugin__: Any file inside this directory is loaded every time you open Vim.
* __autoload__: Files that are loaded on-demand (containing say function
  definitions).
* __ftplugin__: FileType specific files. Thus a file `markdown.vim` inside
  `ftplugin` should consist of settings required only for a markdown file (an
  alternative for the FileType autocommands that we learnt above).
* __colors__: Colorscheme files.
* __syntax__: Files for specifying syntax-based highlights and/or indentation.
* __doc__: Documentation files.
* after: Files that should be loaded after plugins.

Thus, an easy way to install a plugin is to simply copy the files that exist in
corresponding plugin folders to the respective folders inside your .vim
directory.
Vim takes care of the rest. 

### Vim8
Vim8 is the major upgrade to Vim in last 10 years, released on [September 9th,
2016](https://groups.google.com/forum/#!topic/vim_announce/EKTuhjF3ET0).
Vim8 has given boost to various features that were being explored using several
plugins over the last few years.
A few of the most interesting ones are:

* __Async support__: Lets commands (e.g., compilation) run in the background.
* __Packages__: Provides [pathogen](https://github.com/tpope/vim-pathogen) like
  in-build plugin-management functionality (see `:help packages`in Vim8).
* __defaults.vim__: A useful vimrc that is enabled by _default_.

We can hope to see many more plugins taking advantage of the above features
to provide an even enhanced and faster Vim in future.

### Neovim
[Neovim](https://neovim.io/) is a fork of Vim that has gained huge popularity
recently.
It is community-drive, more feature-rich, and claims to have a cleaner
code-base.

Many plugins have been created specifically for Neovim, and many others have
been advertising themselves to be catering to both - Vim and Neovim.

Neovim is not installed by default on many OSes yet.
Further, the releases are sometimes buggy.
However, it will be interesting to see the course it takes.

### Resources for the enthusiast
* First and foremost: `:help` -- the excellent Vim documentation.
* Awesome screencasts demonstrating various Vim features: [vimcasts](http://vimcasts.org)
* A very detailed guide on Vim:
  [vim-galore](https://github.com/mhinz/vim-galore)
* An excellent guideline on sculpting your vimrc:
  [idiomatic-vimrc](https://github.com/mhinz/vim-galore)
* For doubts and queries: [vistackexchange](http://vi.stackexchange.com)
* For interesting announcements and discussions: [vim
  subreddit](https://www.reddit.com/r/vim/)

#### Endnote
That's all from my side, folks!
This is the end to the six-part tutorial on Vim.
I truly enjoyed writing it.
I have been getting many mails that praise the tutorial, appreciate my sticking
to the announced schedule, and suggest improvements.
I am thankful to all of them and to my readers.
Stay in touch and ... __Keep Vimming__.

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module5.md)

[Star this repository](https://github.com/manasthakur/learn-vim/) on GitHub if you like the tutorial.

