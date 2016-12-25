## Learn Vim - Module 5: Plug n Play

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module4.md)  |  [Next module](module6.md)

Vim is very flexible.
It can be extended with plugins.
And thanks to the community, there are literally thousands of freely-available,
open-source plugins for Vim that can be used as it is.

It is advisable not to pollute your Vim setup with unnecessary plugins; even
though tempting, such a practice can take away what Vim is most famous for
-- its performance.
Further, you need to remember that a set of plugins that you have installed on
your machine might not be available on a different machine that you need to log
in to.

All that said, the aim of this module is to initialize you into using Vim
plugins and introduce you to a handful of the useful ones,
so that you at least know what all you can expect from a plugin in Vim.

But how do you install a plugin?
Better use a _plugin manager_.

### Plugin Managers
Almost every plugin that is available now-a-days is available as a GitHub
repository.
The job of a plugin manager is to elegantly let you download and install new
plugins, update them when the plugin-writers create new features or remove bugs,
and graciously remove them.

There are many popular plugin managers; for example,
[Pathogen](https://github.com/tpope/vim-pathogen),
[Vundle](https://github.com/VundleVim/Vundle.vim),
[Vim-plug](https://github.com/junegunn/vim-plug),
and so on.
The installation instructions are very clearly written on the respective webpages.
Most of them require you to add some initialization lines, and then list the
plugins that you want to use, in your vimrc.

I recommend using [Vim-plug](https://github.com/junegunn/vim-plug), which
downloads and updates plugins in parallel, thus speeding up the whole process.
If you are using Vim-plug, you need to specify each plugin that you wish to be
loaded in the following format:
```vim
Plug 'github-repo'
```
For example, to use a plugin available at
[http://vimawesome.com/?q=cat%3Alanguage](https://github.com/manasthakur/vim-sessionist), you need to add the following
line (after setting up vim-plug):
```vim
Plug 'manasthakur/vim-sessionist'
```

Next, you need to install the plugin using the command `:PlugInstall`.
As simple as that!
To update a plugin, just run `:PlugUpdate <plugin-name>` (or `:PlugUpdate`
to update all the plugins).
You can delete a plugin by removing its entry from the vimrc, and then running
`:PlugClean`.

### Getting plugins
Apart from googling for a particular functionality that could be provided by
some plugin, there are two great ways to know about existing Vim plugins:

* Find out popular plugins at [vimawesome.som](http://vimawesome.com/).
* Follow popular plugin writers on GitHub, such as
  [tpope](https://github.com/tpope/), [junegunn](https://github.com/junegunn/),
  and [shougo](https://github.com/shougo/).

Vimawesome is a great resource that sorts plugins submitted to the website based
on categories and popularity.
Tim Pope writes awesome plugins that blend into Vim so smoothly, that people often
wonder whether they are part of the default Vim itself.
Junegunn writes super-performing plugins with a sleek interface.
Shougo writes heavyweight but feature-rich plugins.

Before choosing a plugin, also see whether it is being recently updated.
If not, chances are that it won't add any new features; in that case, better try
another recent alternative.

### Some useful plugins
Here, I will categorically list out some plugins that I find useful.
Please read the plugin's webpage and its documentation (usually accessible using
`:help <plugin-name>`) to know all the features and usage instructions.
Note that some of the plugins have dependencies due to which they might not work
on some versions of Vim directly.

#### Fuzzy finding
Fuzzy finders let you type a part of the file (or path) names, tags
(recall ctags), etc., and open up a selectable list of available options.
These are very handy when you are working on big projects, and
don't remember the full path of a file that you wish to open (using `:e`).
Some popular fuzzy-finding plugins are:

* [CtrlP](https://github.com/ctrlpvim/ctrlp.vim): written purely in vimscript (a
  language to script vim); lets you fuzzy-find files, buffers, tags, mru files,
  etc.
* [fzf.vim](https://github.com/junegunn/fzf.vim): a blazingly fast vim-wrapper
  over a command-line tool called [FZF](https://github.com/junegunn/fzf),
  that lets you find files, buffers, tags, commands, help-files, etc.
* [Command-T](https://github.com/wincent/command-t): a slightly faster
  alternative to CtrlP, that uses code written in multiple languages to improve
  performance.

#### Managing sessions
Vim supports sessions, which means that you can create project-specific
workspaces that can later be loaded as it is.
There are a handful of plugins that make managing sessions easily (instead
of manually running `:mksession` and `:source` commands to create and load a
session, respectively):

* [vim-sessionist](https://github.com/manasthakur/vim-sessionist): written by
  your beloved tutor; it's a very lightweight wrapper that provides commands to
  save a session, open an existing session, restore previous session (in case
  you closed Vim by mistake), etc.
* [vim-session](https://github.com/xolox/vim-session): a slightly heavyweight
  option that gives you more customizability while managing sessions.

#### Code editing
Plugins such as the following enhance your coding experience by providing either
new features, or simplifying the existing ones:

* [vim-commentary](https://github.com/tpope/vim-commentary): lets you comment
  (and uncomment) multiple lines in a very few keystrokes.
* [vim-surround](https://github.com/tpope/vim-surround): lets you change
  surrounding environments (e.g., `'manas'` to `"manas"`).
* [UltiSnips](https://github.com/SirVer/ultisnips): adds snippet-functionality
  to Vim; e.g., a snippet for a _for loop_ might instantly create an editable
  loop body, in a very few keystrokes.

#### Completion
As learnt in the last module, Vim lets you complete keywords, file-paths, tags,
dictionary items, and so on.
There are a bunch of plugins that simplify completion by either displaying
the completion-menu as-you-type, or merging different completion-keystrokes
into one.
Some notable ones are:

* [SuperTab](https://github.com/ervandew/supertab): the classic plugin that lets
  you complete everything using a `<TAB`>.
* [YouCompleteMe](https://github.com/Valloric/YouCompleteMe): apart from default
  completions, also provides language-based completion (like IDEs); needs
  linking with external tools.
* [VimCompletesMe](https://github.com/ajh17/VimCompletesMe): a very lightweight
  alternative to SuperTab.
* [vim-mucomplete](https://github.com/lifepillar/vim-mucomplete): offers
  automatic chained completion (fall-back to another mode if one fails).

#### Integration
Many plugins let you integrate with external commands/tools that you need to
use regularly while editing code.
These plugins allow you to adapt a workflow in which you rarely leave Vim.
A few interesting ones are:

* [vim-fugitive](https://github.com/tpope/vim-fugitive): provides wrappers to
  run Git commands on your project from within Vim.
* [vim-dispatch](https://github.com/tpope/vim-dispatch): allows compilation and
  build processes to be performed in the background; displays errors in a
  quickfix window.
* [Syntastic](https://github.com/vim-syntastic/syntastic): keeps compiling code
  in the background and displays errors using markers within Vim itself; needs
  linking with external tools.

#### Interface
* [Tagbar](https://github.com/majutsushi/tagbar): displays a list of navigable
  tags (variables and functions) in the current file on the right side of your
  editor window.
* [NerdTree](https://github.com/scrooloose/nerdtree): opens a navigable window
  for viewing and moving around your project.
* [Airline](https://github.com/vim-airline/vim-airline)/[Lightline](https://github.com/itchyny/lightline.vim):
  extend the functionality of your statusline and tabline, beautifully!

Apart from these, there are a lot many language-specific plugins out there.
For example, [vimtex](https://github.com/lervag/vimtex) lets you compile,
complete, fold, and preview LaTeX code.
Check out [vimawesome.com](http://vimawesome.com/?q=cat%3Alanguage) to find out which ones you
might need.

The functionality of many of the plugins discussed above can be replaced by
creating custom mappings over the built-in features of Vim.
On the other hand, many of the plugins provide a neat documentation to customize
the plugins themselves as per your needs.
At an advanced stage, you can even write your own plugins (in languages ranging
from Vimscript, C, Python, Ruby, etc.), and publish them for others on GitHub.

Which plugins do I use?
Well, the list keeps on changing based on my requirements and experience (over
the last year, the number has varied between 0 and 25!).
However, at the time of writing this (December 25th, 2016), I cannot live
without [CtrlP](https://github.com/ctrlpvim/ctrlp.vim),
[vim-fugitive](https://github.com/tpope/vim-fugitive),
[vim-commentary](https://github.com/tpope/vim-commentary), and
[vim-sessionist](https://github.com/manasthakur/vim-sessionist).

#### Endnote:
In this module, we learnt how plugins extend the functionalities of Vim.
We went through a short list of plugin-managers, plugin-websites, and a bunch of
useful plugins themselves.
I suggest don't pollute your vimrc with plugins without knowing (a) whether you
need them; and (b) whether something simpler (and hence lighter) can provide you what you need.
Before moving on to the last module of this tutorial, thank the concept of
open-source again!

[Home](https://github.com/manasthakur/learn-vim/)  |  [Previous module](module4.md)  |  [Next module](module6.md)

[Star this repository](https://github.com/manasthakur/learn-vim/) on GitHub if you like the tutorial.

