## Learn Vim - Module 4: Coderz

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module3.md)  |  [Next module](module5.md)

Get ready for a big module!
Here you will learn a lot of things to speed up (and enhance) your coding techniques in Vim.
Note that the content will be easy to digest if you slowly adapt the features mentioned in this module in your workflow, without trying to remember everything at once.
Also, this is the module from where I will start referring you to the awesome Vim documentation, for learning the topics introduced here in detail.

### Navigating code using ctags and cscope

[Exuberant ctags](http://ctags.sourceforge.net/) and [cscope](http://cscope.sourceforge.net/) are external programs that allow jumping across code-blocks, just like IDEs, in Vim.
For installation, please refer to their respective websites.

To use **ctags**, first build tags for your project in the project's root directory using the command:
```
ctags -R	" Build tags recursively
```
The above command creates a `tags` file in your directory, containing a list of tags that ctags can parse very fast.
Note that you need to repeat the command regularly to update the tags after you make changes in your project.

Now, say you are at a function call `foo()` in a cpp file.
To jump to the definition of `foo`, just press `Ctrl=]`.
Whoa! This even jumps across files!
To get back to where you were, press `Ctrl-t`.
If there are multiple functions with the name `foo`, you will get a list to select from.

##### Extra dose:
Note that ctags maintains a stack of your jump-locations.
Thus, you can keep jumping from one function-call to another using `Ctrl-]`, and pop back repeatedly using `Ctrl-t`.

**Cscope** is an even advanced tool that not only supersedes what ctags does, but also lets you jump to the call-sites of a method.
Post installation, similar to ctags, you first need to build a database for cscope.
For example, to build a cscope-database for all the cpp files in your directory, use:
```
find . -name '*.cpp' > cscope.files
cscope -Rb	" Build cscope-database recursively (in a file `cscope.out`)
```

Now let's say you want to get all the call-sites of the method `foo`.
Stay over the function header and type `Ctrl-\ c` to get the list of all the callers of `foo`.
Refer to the [cscope website](http://cscope.sourceforge.net/) to learn about many other features of cscope.

### Indenting code

Forget about code indentation worries in Vim!
Vim supports indentation for programs written in almost every language (and others keep getting added).
The following two options are useful in this regard:
```vim
filetype indent on	" enable file-type based indentation
set autoindent	    " indent next line based on the previous one (e.g., whether it's a `{`)
```
But you had not enabled these in the beginning.
Or someone gave you a very badly-indented file.
No problem!
You can _indent existing code_ using the `=` command.
Just select the text you wish to indent, and press `=`.
See the magic!

You can indent code in the normal mode as well.
Say you want to indent the next 6 lines.
Just press `6==` and see the magic again!

You can also increase or decrease the indentation levels of a line using `>>` and `<<`, respectively, in normal mode.
Similar to the `=` command, you can select text in visual mode and press `>` or `<` as well.

##### Extra dose:
* You can indent a whole file using the shortcut `gg=G` in normal mode.
Try figuring out what do the individual commands mean.
* You can set the number of characters used for indentation by `>>` and `<<` (say, to 4) as follows:
```vim
set shiftwidth=4
```

### Matching parentheses (and more)
Vim can show you the matching parentheses, braces, and brackets when the cursor is on one of them.
Add the following in your vimrc:
```vim
set showmatch
```
Now, if your cursor is on say, the opening bracket, press `%` to jump to the corresponding closing bracket.

There is another secret built-in plugin (called _matchit_) that also allows you to jump to the corresponding keywords (for example, `endif` for `if`), using the `%` operator.
Add the following line to your vimrc file to enable this plugin by default:
```vim
runtime! macros/matchit.vim
```
Once you start coding, you will find this very handy, specially when a code-block doesn't fit into your screen.

### Running shell commands from Vim
It's routine to keep editing your code, compile it, edit it again, and so on.
And it's very inefficient to close Vim and run the commands, open Vim and edit again, and so on.

One simple alternative is to simply put Vim to the background using `Ctrl-Z`, use the shell, and then come back using `fg`.
However, you can even avoid that by running shell commands while being inside Vim.
There are two ways to do this:

1. Type `:shell` to get to a temporary shell-prompt.
Type `Ctrl-D` to come back to Vim.

2. Run shell commands using the `!` operator in command-line mode.
For example, `:!javac %` will compile the file loaded in the current buffer.

When you have _Makefiles_, you can build your project even more efficiently using the builtin _make_ command of Vim.
Just run `:make` and see your project built!

There are even better ways to compile your code using plugins.
We will learn more about them in later modules.

### Search-and-replace across files

In module 3, we had learnt that we can search in the current buffer using the `/` and `?` commands, and replace text in the current buffer using the `%s/oldword/newword/g` command.

To search across multiple files, we can use **grep** (yes, the one you use in a terminal) along with all its options, in the command-line mode of Vim.
For example, to recursively search for the word `sophisticated` in the current directory, use:
```
:grep -R 'sophisticated' .	" search the word 'sophisticated' recursively (-R) in the current directory (.)
```
The advantage of using grep within Vim is that it loads all the search-results in the **quickfix window**.
To understand this, once you have searched for a word using `grep`, type `:copen` in the command-line mode.
This creates a new split in your Vim with all the search occurrences.
You can either use the arrow keys with `<CR>` to jump to any results (use `<C-w>w` to switch windows),
or use the following commands to jump to the next and the previous search-result, respectively:
```
:cnext	    " jump to the next entry in the quickfix window
:cprevious	" jump to the previous entry in the quickfix window
```
Cool, right!
But this is not all.
You can _apply_ a command to all the entries in the quickfix window using `:cdo`.
This means you can replace all the occurrences of the searched word as follows:
```
:grep -R 'oldword' .                    " search 'oldword' recursively
:cdo %s/oldword/newword/c	            " replace occurrences one-by-one
OR
:cdo %s/oldword/newword/g | update	    " replace all occurrences and save
```
Note that in the last command, as we have replaced all the occurrences in one shot, we have used the bar operator (`|`) to also update (i.e., save) all the files.
In the former case, you need to save the buffers explicitly --  either one-by-one, or using `:wall`.

Combine the above commands with regular expressions, and see Vim do wonders with searching and replacement.

### Diffing files

Similar to the `diff` command in your terminal, Vim provides a `vimdiff` program to compare and merge two files.

To see the differences between `file1` and `file2`, type the following at your command prompt:
```
vimdiff file1 file2
```
This will open Vim with the two files open side-by-side, in a vertical split.
The changes will be highlighted using different colors.
If you have used `diff` before, you will find `vimdiff` a boon.

Vim provides the following shortcuts to navigate among the changes, and push or pull changes from one file to another:

* `]c`: Jump to next change.
* `[c`: Jump to previous change.
* `:diffput` or `dp`: push the current change to the other split.
* `:diffget` or `do`: pull the corresponding change from the other split.

You can also diff multiple files using vimdiff.
Use `:help vimdiff` to learn the details.

### Typing less and getting more

Now we are moving on to some sophisticated, not-known-to-basic-users, features of Vim.
Let's start with insert-mode completions.

#### Completion

Vim provides superb completion support.
You can avoid typing literally anything you have typed before, and also complete things that you have not even typed yet!
In insert-mode, just type a few characters and press the following to complete items (you will get a navigable list if multiple choices are available):

* `Ctrl-p`: Search what you have already typed, in reverse order (backwards from the current location).
* `Ctrl-n`: Search what you have already typed, forwards from the current location.
* `Ctrl-x Ctrl-f`: Complete file paths
* `Ctrl-x Ctrl-]`: Complete tags
* `Ctrl-x Ctrl-l`: Complete whole lines
* `Ctrl-x Ctrl-k`: Complete from Vim's built-in dictionary
* `Ctrl-x Ctrl-o`: Omni-completion

The last entry (omni-completion) needs special mention.
Omni-completion lets you complete keywords based on special characters.
For example, in c/cpp programs, omni-completion will let you complete after typing `.` or `->` operators.
To see a list of languages for which Vim provides omni-completion, use `:help omni<TAB>`.

These are not the only completion-types available.
Use `:help ins-completion` to get the comprehensive list.
In the next module, we will learn about some plugins that simplify as well as extend the completion types available, even further.

#### Abbreviations
Vim allows you to create abbreviations as shortcuts to enter text.
Say you want to expand `syso` in Java to `System.out.println`.
Create an abbreviation as follows:
```
:iabbrev syso System.out.println
```
You would find that once you type `syso` and then anything else, it gets expanded to `System.out.println`.
The `i` in the above command says that the abbreviation works only in insert mode.

Another common use-case of abbreviations is to correct spellings.
Say you find that you repeatedly type `teh` instead of `the`.
Now you know how to correct yourself automatically:
```
:iabbrev teh the
```

#### Mappings
Mappings are one of the most useful features of Vim.
You can map almost any sequence of keys to a shorter one.

Say, you want to map `Ctrl-l` to clear highlights (created say because of some search).
You know from the previous module that the command to clear highlights is `:nohlsearch`.
The mapping goes as follows:
```vim
nmap <C-l> :nohlsearch<CR>	    " clear search-highlights using `<C-l>`
```
Let's break down the mapping:

- The first `n` means that the mapping should work only in normal mode.
If the mapping should work in all the modes, drop the `n`.
Similarly, `imap` is for the insert mode.
- The first string till a space (`C` in `<C-l>` stands for the `Ctrl` key) is the map that we are creating.
- The second string is the command that we wish to map the first string to.
Here we have mapped `<C-l>` to first go to the command-line mode, type `nohlsearch`, and then press enter (`<CR>`).

It is advisable to always use `noremap` instead of `map` to avoid recursive mappings (map within a map).
Thus, the above command becomes:
```vim
nnoremap <C-l> :nohlsearch<CR>	    " clear search-highlights using `<C-l>`
```

Following is a small list of the keystrokes used to represent the special-keys on our keyboards:
* `C` stands for `Ctrl`
* `M` stands for `Alt/Option`
* `CR` stands for `Enter`

Mappings are mostly created by appending them to a **leader** key (in order to avoid conflicts with the existing commands).
The default leader is the `\` (backslash) key.
Thus, the following map would clear the search highlights using `\l`:
```vim
nnoremap <leader>l :nohlsearch<CR>	    " clear search-highlights using `\l`
```
I am not covering how to change the leader key in this tutorial.

You can add multiple commands in a map using the `<bar>` (or `|`) operator.
Thus, to save your code and then build it using `\m`, you can have the following mapping:
```vim
nnoremap <leader>m :w<CR> <bar> :make<CR>
```

Mappings are very useful.
With time, you will keep finding keystrokes or commands that you often use in sequence.
Those will be good times to add shortcuts using maps in your vimrc.

### Folding text

We will wrap up this module by getting a glimpse of the many ways code (or any text) can be folded for better visibility and movement in large files, in Vim.

In programs, folding is useful to wrap, say functions, so that you can easily glance over and move among the functions in your file.
In text, latex, or markdown files, folding is useful to wrap, say sections or figures, and look over the way your file is organized.

There are many ways to fold text.
First, we need to enable folding, and then select one of the following modes:

* manual: Create folds manually, as and when needed (default).
* marker: Create folds using fold-markers (`{{{` and `}}}`).
* indent: Create folds based on indentation levels.
* syntax: Create folds based on syntax-highlighting items.
* expr: Create folds based on custom expressions.

We will learn about manual folding and markers-based folding in this tutorial.

As _manual_ mode is the default, just enable folding as follows:
```vim
set foldenable	    " Enable folding
```
To fold a block of text, select it (using visual-mode), and then press `zf`.
This creates a fold over the selected region.

The following is a subset of commands to work with folds (in normal mode):

* `zo`: Open a fold
* `zO`: Open all folds under the cursor recursively
* `zc`: Close a fold
* `zC`: Close all folds under the cursor recursively
* `za`: Toggle a fold
* `zA`: Toggle all folds under the cursor recursively

The disadvantage of manual folds is that they get lost once you close a file.
Let's learn about one of the folding methods that creates persistent folds -- _marker_.
Enable it as follows:
```vim

set foldmethod=marker	    " Enable marker-based folding
```
Now you can _define_ a fold by enclosing the intended region of text between `{{{` and `}}}` (in comments around the text-block).

You can create _nested_ marker-based folds by defining a level next to the fold-markers; e.g., `{{{1` and `}}}1`, `{{{2` and `}}}2`, and so on.
Remember to close the folds properly with the correct level-numbers.

Folding is a very broad subject.
Learn more about the other fold-methods using `:help folding`.

#### Endnote:
In this module, we learnt a lot of options and facilities provided by Vim for coders.
The aim was to introduce you to the kind of things that can be done; mastering all of them will take months of practise.
I suggest you keep coming back to this module whenever you need a specific feature, instead of trying to remember everything and complicating your workflow.
In the next module, we will see how some of the existing functionalities can be extended using the plugins created by the Vim community.

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module3.md)  |  [Next module](module5.md)

[Star this repository](https://github.com/manasthakur/learn-vim/) on GitHub if you like the tutorial.

