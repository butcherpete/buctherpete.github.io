---
title: Vim Starters 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: mydoc_sidebar
permalink: vim_starters.html
folder: vim 
---

## Starters

To get information:

```
:version
```

### Brew

Installed with Homebrew.

* Version: 8.0.52
* Location: `/usr/local/bin/vim` ### Vimrc To edit: 

```
$ vim ~/.vimrc
```

To reload (source) changes to the `.vimrc` from within the .vimrc file:

```
:so %
```

The character `%` stands for the current file name (see `:h current-file`).

Otherwise:

```
:so $MYVIMRC
```

### Vundle

To install in Vim, launch vim and run:

```
:PluginInstall
```

To install from command line:

```
$ vim +PluginInstall +qall
```
To read docs:

```
:h vundle
```

## <a id="moving">Moving Around</a>
### Up-Down Motions

Key | Action
--- | ------
_#_ `gk` | Count display lines upward. Differs from `k` when lines wrap, and when used with an operator.
_#_ `gj` | Count display lines upward. Differs from `j` when lines wrap, and when used with an operator.
_#_ `G` | Count display lines upward.
`G` | Go to bottom of file.
`gg` | Go to top of file.

### Line Motions

Key | Action
--- | ------
`$`  | End of line
`$p`  | Paste to end of line
`0`  | Start of line
`A`  | End of line & Input mode
`C`  | Delete to the end line & Input mode

### Word Motions

Key | Action
--- | ------
`b` / `B`  | Backward one word/WORD
`w` / `W`  | Forward one word/WORD
`e`  | End of current/next word
`E`  | End of current/next WORD
`ge`  | End of previous word
`gE`  | End of previous WORD

WORDs are bigger than words.
* A WORD consists of a sequence of non-blank characters is separated by white space. Both _we're_ and _e.g._ are WORDs.
* A word consists of a sequence of letters, digits, and underscores.

### Character Searches

Key | Action
--- | ------
`f{char}`  | Forward to the next {char}. 
`F{char}`  | Backward to the previous {char}.
`t{char}`  | Forward to the character before next {char}.
`T{char}`  | Backward to the characgter before the next {char}.
`;`  | Repeat the last character-search command (forward). 
`,`  | Reverse the last character-search command (backward). 

## <a id="unimpaired">Unimpaired</a>

```
:help unimpaired
```

The following maps all correspond to normal mode commands.  If a count is
given, it becomes an argument to the command.  A mnemonic for the "a" commands is "args" and for the "q" commands is "quickfix".

Key | Action
--- | ------
`[a`     |`:previous`|
`]a`     |`:next`|
`[A`     |`:first`|
`]A`     |`:last`|
`[b`     |`:bprevious`|
`]b`     |`:bnext`|
`[B`     |`:bfirst`|
`]B`     |`:blast`|
`[l`     |`:lprevious`|
`]l`     |`:lnext`|
`[L`     |`:lfirst`|
`]L`     |`:llast`|
`[<C-L>` |`:lpfile`|
`]<C-L>` |`:lnfile`|
`[q`     |`:cprevious`|
`]q`     |`:cnext`|
`[Q`     |`:cfirst`|
`]Q`     |`:clast`|
`[<C-Q>` |`:cpfile`| (Note that <C-Q> only works in a terminal if you disable
`]<C-Q>` |`:cnfile`| flow control: stty -ixon)
`[t`     |`:tprevious`|
`]t`     |`:tnext`|
`[T`     |`:tfirst`|
`]T`     |`:tlast`|


## <a id="edit">Editing/Substituting</a>

### Change

A change is a "chord" that deletes and switches to INSERT mode.

Key | Action
--- | ------
`cl` | Delete letter & INSERT mode.
`ch` | Delete back one letter & INSERT mode.
`cw` / `cW` | Delete word/WORD & INSERT mode.
`cb` / `cB` | Delete previous word/WORD & INSERT mode.
`c$` / `C` | Delete to end of line & INSERT mode.
`dt.` | Delete to end of line and period.
`c^` | Delete to beginning of line & INSERT mode.

###  Substituting Cases

Key | Action
--- | ------
`g~<motion>` | Swap case.
`gu<motion>` | Make lowercase.
`gU<motion>` | Make uppercase.
`3~` | Toggle case of next three characters.
`gUiw` | Make entire word uppercase. (If `i` is excluded, from current position to end of the word only.)
`gUiW` | Make entire WORD uppercase.
`gU3w` | Make next three words uppercase.
`gU0` | Make uppercase to beginning of line.
`gU$` | Make uppercase to end of line.

## <a id="html">HTML Cleanup</a>

### Live Preview of HTML

Run the following in the root folder:

```
$ python -m SimpleHTTPServer 8080
```

### Editing HTML
To delete blank lines:

```
:g/^$/d
```

To strip trailing whitespace:

```
:%s/\s\+$//e
```

To remove leading whitespace from range of lines:

```
:19,25s/^\s\+//
```

### Tidy
Pipe the buffer through Tidy to get clean HTML:

```
:%!tidy -qicbn -asxhtml
```

Command  |  Action
---     |  ------
`-indent`, `-i`  | Indent element content
`-clean`, `-c`  | Replace FONT, NOBR, and CENTER tags by CSS.
`-bare`, `-b`  | Strip out smart quotes and em dashes, etc.
`-quiet`, `-q`  | Suppress nonessential output..
`-asxml`, `-asxhtml`  | Convert HTML to well formed XML.

Use `tidy -h` to view more options.

### Pandoc

http://vimcasts.org/episodes/using-external-filter-commands-to-reformat-html/

Use the bang Ex command to filter the contents of the current buffer through a pandoc pipeline:

```
:%!pandoc --from=html --to=markdown | pandoc --from=markdown --to=html
```

## <a id="emmet">Emmet</a>

To expand shortcuts: `CTRL+y,`

### HTML Page
`html5:_`

## <a id="folding">Folding</a>

http://vimcasts.org/episodes/how-to-fold/

https://github.com/nelstrom/vim-markdown-folding


### Essentials

Command  |  Action
---     |  ------
`zi`  | Switch folding on or off
`za`  | Toggle current fold open/closed
`zc`  | Close current fold
`zR`  | Open all folds
`zM`  | Close all folds
`zv`  | Expand folds to reveal cursor
`:FoldToggle` | Toggles between flat and nested folding in vim-markdown-folding.

### Navigation 

To navigate an unfolded document:

Command  |  Action
---     |  ------
`zj`  | Move down to toop of the next fold.
`zk`  | Move up the bottom of the previous fold.
 
### More Commands 

Command  |  Action
---     |  ------
`zo`  | Open the current fold.
`zO`  | Recursively Open the current fold.
`zc`  | Close the current fold.
`zC`  | Recursively close the current fold.
`za`  | Toggle the current fold.
`zA`  | Recursively toggle the current fold.
`zm`  | Reduce the fold-level by one.
`zM`  | Close all folds.
`zr`  | Increase the fold-level by one.
`zR`  | Open all folds.

## <a id="search">Search & Replace</a>

### Substitute

Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.

```
:%s/foo/bar/g
```
Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'.

```
:s/foo/bar/g
```
Change each 'foo' to 'bar', but ask for confirmation first.
```
:%s/foo/bar/gc
```

Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation.

```
:%s/\<foo\>/bar/gc
```
Change each 'foo' (case insensitive due to the `i` flag) to 'bar'; ask for confirmation.

```
:%s/foo/bar/gci
```

`:%s/foo\c/bar/gc` is the same because `\c` makes the search case insensitive.

This may be wanted after using :set noignorecase to make searches case sensitive (the default).

Change each 'foo' (case sensitive due to the `I` flag) to 'bar'; ask for confirmation.

```
:%s/foo/bar/gcI
```
`:%s/foo\C/bar/gc` is the same because `\C` makes the search case sensitive.

This may be wanted after using `:set ignorecase` to make searches case insensitive.

## <a id="ack">Ack Search</a>

http://beyondgrep.com/documentation/

```
:Ack [options] {pattern} [{directories}]
```
Search recursively in `{directories}`, which defaults to the current directory for the `{pattern}`.

Files containing the search term will be listed in the quickfix window, along with the line number of the occurrence, once for each occurrence. `<Enter>` on a line in this window will open the file, and place the cursor on the matching line.

Just like where you use `:grep`, `:grepadd`, `:lgrep`, and `:lgrepadd`, you can use `:Ack`, `:AckAdd`, `:LAck`, and `:LAckAdd` respectively. (See `:help Ack` after installing, or `doc/ack.txt` in the repo, for more information.)

### Keyboard Shortcuts

The quickfix results window is augmented with these convenience mappings:

Command  |  Action
---     |  ------
`?`  |    A quick summary of these keys, repeat to close
`o`  |    To open (same as Enter)
`O`  | To open and close the quickfix window
`go` | To preview file, open but maintain focus on ack.vim results
`t`  |    To open in new tab
`T`  |   To open in new tab without moving to it
`h`  |   To open in horizontal split
`H`  |   To open in horizontal split, keeping focus on the results
`v`  |   To open in vertical split
`gv` |   To open in vertical split, keeping focus on the results
`q`  |   To close the quickfix window

### Gotchas

Some characters have special meaning, and need to be escaped in your search pattern. For instance, `#`. You need to escape it with `:Ack '\\\#define foo'` to search for `'#define foo'`.

### Do Not Jump First Result Automatically

Use `:Ack!`, with bang. If you want this behavior most of the time, you might like an abbreviation or mapping in your personal config, something like these:

```
cnoreabbrev Ack Ack!
nnoremap <Leader>a :Ack!<Space>
```

Most of the `:[L]Ack*` commands support this. Note that this behavior follows the convention of Vim's built-in `:grep` and `:make` commands.

## <a id="spellcheck">Spellcheck in Vim</a>
http://vimcasts.org/episodes/spell-checking/


Spell check.

```
:set spell
```
Set spelling language to American English.

```
:set spelllang=en_us
```

Jump backward.

```
[s
```
Jump forward.

```
]s
```

Suggest correct spelling.

```
z=
```

To select a suggestion, enter the line number and press the Return key.

To take the first suggestion  without viewing the list, enter `1z=`.  To reverse the correction,  press the `u` key.

Add highlighted word spell file.

```
zg
```
Spell file location: `~/.vim/spell/en.utf-8.add`

To remove a highlighted word from spell file.

```
zug
```

## <a id="copying">Copying and Pasting</a>

### System Clipboard / Quoteplus Register

> CLIPBOARD is expected to be used for cut, copy and paste operations. … Vim uses CLIPBOARD when reading and writing the “+ register. (see `:h quoteplus)

To yank text from a Vim buffer into the system clipboard, use these commands:

Command | Affect
--- | ------
`{VISUAL}"+y` | Copy the selected text into the system clipboard.
`"+y{motion}` | Copy the text specified by `{motion}` into the system clipboard.
`:[range]yank +` | Copy the text specified by `[range]` into the system clipboard.

To copy text into the Mac OS register:

```
"*y
```

To paste text from the system clipboard into a Vim buffer, use these commands:

Command | Affect
--- | ------
`"+p` | Pastes the system clipboard after the cursor in Normal mode.
`:put +` | Puts contents of system clipboard on a new line.
`<C-r>+` | Pastes from Insert or Commandline mode.

### Pasting 
To paste the contents of a register:

Command | Affect
--- | ------
`p` | Paste contents after the cursor.
`P` | Paster contents before the cursor.

### Alfred's Clipboard History
https://www.alfredapp.com/help/features/clipboard/

## <a id="blocks">Visual Blocks </a>

### To insert on multiple lines:

1. Move the cursor to the first letter of the first line.
2. Enter visual block mode (CTRL+v).
3. Press `j` to select to end of list.
4. Press `I`.
5. Type the prefix. For example, `*<space>`
6. Press the `ESC` key.

## <a id="fugitive">Vim Git / Fugitive</a>

* Vim Git Workflow: <https://www.youtube.com/watch?v=GUptUQGrJLE>


### Fugitive Commands
Use the `:Git` command to run git commands in Vim.

```
:Git checkout -b experimental
```

In Vim, the `%` symbol expands to the full path of the current file. You can use this to `add`, `checkout`, `rm`, or `mv` the current file.

Alternativley, Fugitive supplies convenince methods.

Git | Fugitive | Action
--- | ------ | ------
`:Git add %` | `:Gwrite` | Stage the current file to the index.
`:Git checkout %` | `:Gread` | Revert current file to last checked in version. |
 `:Git rm %` | `:Gremove` | Delete the current and the correspondn Vim buffer. |
`:Git mv %` |  `:Gmove` |  Rename the current file and the corresponding Vim buffer. |

> "The `:Gcommit` command opens up a commit window in a split window. One advantage to using this, rather than running git commit in the shell, is that you can use Vim’s keyword autocompletion when composing your commit message."


> "The `:Gblame` command opens a vertically split window containing annotations for each line of the file: the last commit reference, with author and timestamp. The split windows are bound, so that when you scroll one, the other window will follow."

### Git Status

The `:Gstatus` command opens a status window. The contents closely resemble the output from running git status in the shell, but fugitive makes the window interactive.

You can jump directly between files using `ctrl-n` and `ctrl-p`. (You can always use `j` and `k` to move up and down line by line.)

Command | Affect
--- | ------
`-` | Add/reset the selected file. Adding a modified file to the commit or removing it.  (Works in visual mode too.)
`<Enter>` | Open current file in the window below.
`p` | Run `git add --patch` for current file.
`C` | Invoke `:Gcommit`.
`:Gdiff` | View changes in file.

### Gdiff

Run `:Gdiff` without any arguments to view a vimdiff of the current working copy and the index copy in a vertically split window.

* Left: Index copy
* Right: Working copy

#### Wholesale Recon
The `:Gread` and `:Gwrite` commands can either add a file to the index or reset the file, depending on where they are called from. The following table and diagrams summarize the possibilities:

Command | Active Window | Affect
--- | ------  | ------
`:Gwrite` | working | Stage file.
`:Gwrite` | index | Check out file.
`:Gread` | working | Check out file.
`:Gread` | index | Stage file.

#### Piecemeal Recon

Vim’s built in `:diffget` and `:diffput` commands work a bit like `:Gread` and `:Gwrite`, except that they are more granular. Whereas `:Gread` will completely overwrite the current buffer with the contents of the other buffer, `:diffget` will only pull in a patch at a time.

Position cursor on the hunk and run:

Command | Active Window | Affect
--- | ------  | ------
`:diffput` | working | Stage hunk.
`:diffput` | index | Check out hunk.
`:diffget` | working | Check out hunk.
`:diffget` | index | Stage hunk.

Run `:diffupate` to update the split window with recent changes.

To view the patch to be committed, run the following in the Terminal:

```
$ git diff --cached
```

### Git Index
The git index is where you put changes that you want to be included in the next commit.  Use fugitive to read the index version of a file into a buffer by running:

```
:Gedit :path/to/file
```

You can open the index version of a working file using the following commands:

```
:Gedit
:Gedit :0
:Gedit :%
```

### Git Aliases

<http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/>

To set a git alias:

```
$ git config --global alias.co checkout

$ git config --global alias.last 'log -1 HEAD'
```
Or edit the `.gitconfig` file.

```
ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate
```

To define the `alias` alias:
```
$ git config --global alias.alias "config --get-regexp ^alias\."
```

To view my aliases:

```
$ git alias
```
Or open the `.gitconfig`.

```
$ vim ~/.gitconfig
```

My Vim Git aliases:

Key | Action
--- | ------
`:git gst` | git status
`:git co` | git checkout
`:git br` | git branch
`:git ci` | git commit
`:git unstage` | git reset HEAD --
`:git ls` | list commits w/ branch tag annotations
`:git ll` | list commits w/ changed files
`:git lds` | list commits w/ dates
`:git logtree` | list commits w/ graph




### Vimdiff
Use `vimdiff` to open two files.

```
$ vimdiff source1.htm source2.htm
```

Set `vimdiff` as the default tool for the default external diff tool for Git.

```
$ git config --global diff.tool vimdiff
```

> Any code that is identical is folded away so you do not need to look at identical code or scroll through huge chunks of identical code.

When you open `:Gdiff` on a conflicted file, figutive open a three split windows:

* Left: Target branch (HEAD) [ _//2_ ]
* Middle: Working copy with conflict markers
* Right: Merge branch [ _//3_ ]

In a three-way split `diffput` and `diffget` can be ambiguous, so you must specify a "buffspec". Use `:ls` to get the buffer number for each of the three windows in the split.

Two strategies:

* Place cursor in the middle working copies and run `:diffget //2` or  `do //2` to obtain the change from the specified buffer.
* Place the cursor in the change you want (left or right) and run `:diffput filename` or `dp filename` to push the change to working copy (middle).


Command | Description
--- | ------
`dp` / `:diffput` | Puts changes under the cursor into the other file making them identical (thus removing the diff).
`:diffget` | Obtains the change and replaces the content under cursor  making them identical.
`]c` | Jump to the next diff
`[c` | Jump to the previous diff
`:diffupdate` | Run periodically to update the color hightlighting.
`:only` | Closes all but the current window. You must do this to save the changes.
`:Gwrite` | Writes the unconflicted working copy (middle window) to the commit and closes the other windows.
`:Gwrite!` | Writes the selected branch target (left) or merge  (right) to the commit and closes the other windows.

## <a id="vim-gitgutter">Gitgutter</a>

Displays a git diffs in the gutter column that shows each line that was added, modified, or removed. You can also state or undo individual hunks.

### Basics

Command | Description
--- | ------
`:h gitgutter` | View help.
`:GitGutterToggle` | Toggle gitgutter. (Default is on)
`:GitGutterSignsToggle` | Toggle signs on or off. (Default is on)
`:GitGutterLineHighlightsToggle` | Toggle line highlighting on or off. (Default is off)

### Hunks 

Action  | Affect
--- | ------
`]c ` | Jump to next hunk (change).
`[c ` | Jump to previous hunk (change).
`\hs` | Stage hunk (change).
`\hu` | Undo staging of hunk (change).

Both `c` actions take a preceding count (#).

The `<Leader>` key is mapped to `\` by default. See `:help leader`.


## <a id="bookmarks">Bookmarks</a>

Shortcut |	Command |	Action
------ | ------------ | --------
`mm`  | 	`:BookmarkToggle` | Toggle bookmark at current line.
`mi` | 	`:BookmarkAnnotate` <TEXT> | Add/edit/remove annotation at current line.	
`mn` | 	`:BookmarkNext` |  Jump to next bookmark in buffer.
`mp` | 	`:BookmarkPrev`|  Jump to previous bookmark in buffer.
`ma` | 	`:BookmarkShowAll` | Show all bookmarks (toggle).
`mc` | 	`:BookmarkClear` | Clear bookmarks in current buffer only.
`mx` | 	`:BookmarkClearAll` | Clear bookmarks in all buffers.
`mkk` | 	`:BookmarkMoveUp` | Move up bookmark at current line.	
`mjj` | 	`:BookmarkMoveDown` | Move down bookmark at current line.	
 | `:BookmarkSave` <FILE_PATH> |  Save all bookmarks to a file.		
| | `:BookmarkLoad` <FILE_PATH> | Load bookmarks from a file.		

## <a id="text-objects">Text Objects</a>

### HTML Tags

To select the contents of a tag (`t`):

```
vit
```
To select the content of the outer tag:

```
v_it
```
To select tags:

Action  |  Selection
---     |  ------
`cit`  | delete tag contents & insert mode
`dit`  | delete tag contents
`vit`  | select tag contents & visual mode
`yit`  | this

### Text Objects Selection
Text Object  | Selection
---          | ------
`a)` / `i)`  | all / inside paretheses
`a}` / `i}`  | all / inside braces
`a]` / `i]`  | all / inside brackets
`a>` / `i>`  | all / inside angle brackets
`a'` / `i'`  | all / inside single quote
`a"` / `i"`  | all / inside double quote
`` a` `` / ``i` `` | all / inside backticks
`at` / `it`  | all / inside tags

## <a id="surround">Vim Surround</a>

* Delete surroundings: `ds`
* Change surroundings: `cs` | `cS`
* Add surroundings: `ys` | `yS` | `ySS`
* Visual mode: `vS` | `vgS`

https://github.com/tpope/vim-surround

### Change Surroundings
Change surroundings is `cs` .  It takes two arguments, a target like with `ds`, and a replacement.

`cS` changes surroundings, placing the surrounded text on its own line(s) like `yS`.  Details about the second argument can be found below in _surround-replacements_.  Once again, examples are in order.

Before | Action | After
--- | ------| ------
"Hello *world!" | `cs"'` | 'Hello world!'
"Hello *world!" | `cs"<q>` |  <q>Hello world!</q>
(123+4*56)/2 | `cs)]`   |       [123+456]/2
(123+4*56)/2  | `cs)[`  |        [ 123+456 ]/2
\<div>Yo!*\</div>  | `cst<p>`  |      <p>Yo!</p>

Description:

Key | Action
--- | ------
`cs"'` | Replaces surrounding `"` with `'`
`cs'<q>` | Replaces surrounding `'` with `<q>`
`cst"` | Replaces surrounding tag with `"`


### Delete Surroundings
Delete surroundings is `ds`.  The next character given determines the targetted delete.  The exact nature of the target is explained in _surround-targets_ but essentially it is the last character of a _text-object_.

This mapping deletes the difference between the "i"nner object and "a"n object.  This is easiest to understand with some examples:

Before | Action | After
--- | ------| ------
"Hello *world!"  |    `ds"`  |   Hello world!
(123+4*56)/2 |   `ds)`  |        123+456/2
\<div>Yo!*\</div>  |  `dst`   |       Yo!

### Add Surroundings
`ys` takes a valid Vim motion or text object as the first object, and wraps it using the second argument as with `cs`.  (It's a stretch, but a good mnemonic for `ys` is "you surround".)

Before | Action | After
--- | ------| ------
Hello w*orld!  |           `ysiw)`   |    Hello (world)!

As a special case, *yss* operates on the current line, ignoring leading
whitespace.

Before | Action | After
--- | ------| ------
Hello w*orld!   |      `yssB`      |      {Hello world!}

There is also `yS` and `ySS` which indent the surrounded text and place it on a line of its own.


Description:

Key | Action
--- | ------
`ysiw]` | Surrounds text object with `]`
Visual select + `S<p class="x">` | Surround text in element.

### Visual Mode Surroundings

### Targets

The  Vim Surround `ds` and `cs` commands both take a target as their first argument.  The possible targets are based closely on the _text-objects_ provided by Vim.

All targets are currently just one character.

#### Punctuation Marks
Eight punctuation marks, `(`, `)`, `{`, `}`, `[`, `]`, `<`, and `>`, represent themselves and their counterparts.

If the opening mark is used, contained whitespace is
also trimmed.  The targets `b`, `B`, `r`, and `a` are aliases for `)`, `}`, `]`, and `>` (the first two mirror Vim; the second two are completely arbitrary and subject to change).

#### Quotation Marks
Three quote marks, `'`, `"`, `` ` ``, represent themselves, in pairs.  They are only searched for on the current line.

#### Tag Alias
A `t` is a pair of HTML or XML tags.  See _tag-blocks_ for details.

Remember that you can specify a numerical argument if you want to get to a tag other than the innermost one.

The letters `w`, `W`, and `s` correspond to a _word_, a _WORD_, and a _sentence_, respectively.  These are special in that they have nothing to delete, and used with `ds` they are a no-op.  With `cs`, one could consider them a slight shortcut for `ysi` (`cswb` == `ysiwb`, more or less).

A `p` represents a _paragraph_.  This behaves similarly to w, W, and s above; however, newlines are sometimes added and/or removed.

## <a id="matchit">Matchit</a>

To do, install machit

The `%` command jumps between matching parentheses. Matchit expands this behavior to include jumps between paired `< >`, HTML tags, or regex expressions.

## <a id="ragtag">Vim-Ragtag</a>
(Formerly allml)

To do, install vim-ragtag.


## <a id="Buffers">Buffers</a>

http://vimcasts.org/episodes/working-with-buffers/

These commands show and navigate through the buffer list:

Command  | Action
----     |  ------
`:ls` |  Show the buffer list
`:bn` | Open the next buffer in the current window (cycles from the end of the list to the beginning).
`:bp` |  Open the previous buffer in the current window (cycles from the start of the list to the end).
`:b2` |  Open buffers in the current window by specifying the buffer number.
`CTRL-^` |   Switch to the alternate file.
`:bd` | Close the current buffer.
`:bw2` | Close buffers by specifying he buffer number, i.e. `:bw2`
`:1,3bw` | Close a range of buffers.

Tab line in airline automatically displays all buffers if only one tab open. Added the following to my `.vimrc` file:

```
let g:airline#extensions#tabline#enabled = 1
```

## <a id="windows">Windows</a>

### Opening Split Windows

Command  | Action
----     |  ------
`ctrl-w s` |   Split the current window horizontally, loading the same file in the new window
`ctrl-w v` |   Split the current window vertically, loading the same file in the new window
`:sp[lit]` _filename_ |  Split the current window horizontally, loading filename in the new window
:star: `:vsp[lit]` _filename_ |   Split the current window vertically, loading filename in the new window

### Closing Split Windows

Command  | Action
----     |  ------
`:q[uit]` |  Close the currently active window.
`:on[ly]` |  Close all windows except the currently active window.

### Changing Focus Between Windows

Shortcut | Command  | Action
---- | ----     |  ------
 -  | `ctrl-w w` |   Cycle between the open windows.
`ctrl-h` | `ctrl-w h` |   Focus the window to the left.
`ctrl-j` | `ctrl-w j` |   Focus the window to the down.
`ctrl-k` | `ctrl-w k` |   Focus the window to the up.
`ctrl-l` | `ctrl-w l` |   Focus the window to the right.

I included the following in my `.vimrc` file to enable the shortcuts:

```
map <C-h> <C-w>h
map <C-j> <C-w>j
map <C-k> <C-w>k
map <C-l> <C-w>l
```

### Resizing Windows

You can resize windows by clicking on the boundary between windows, and dragging it to your prefered size. The following key commands also help:

Command  | Action
----     |  ------
`ctrl-w +` |  Increase height of current window by 1 line.
`ctrl-w -` |  Decrease height of current window by 1 line.
`ctrl-w _` |   Maximise height of current window.
`ctrl-w |` |   Maximise width of current window.

### Moving Windows

Command  | Action
----     |  ------
`ctrl-w r` |  Rotate all windows.
`ctrl-w x` |   Exchange current window with its neighbor.
`ctrl-w H` |   Move current window to far left.
`ctrl-w J` |   Move current window to bottom.
`ctrl-w K` |   Move current window to top.
`ctrl-w L` |   Move current window to far right.

## <a id="explorer">File Explorer</a>

### Exploring the Filesystem

Lazy  | Command  |  Open File Explorer
---     | ---     |  ------
`:e.` | `:edit .` | At current working directory.
`:sp.` | `:split .` | In split at current working directory.
`:vs.` | `:vsplit .` | In vertical split at current working directory.
`:E` | `:Explore` | At directory of current line.
`:Se` | `:Sexplore` | In split at directory of current line.
`:Vex` | `:Vexplore` | In vertical split at directory of current line.

### Manipulating the Filesystem

Command  |  Action
---     |  ------
`%`  | Create a new file.
`d`  | Create a new directory.
`R`  | Rename the file/directory under the cursor.
`D`  | Delete the file/directory under the cursor.

### Vinegar

https://github.com/tpope/vim-vinegar

Command  |  Action
---     |  ------
`-` | Press `-` in any buffer to hop up to the directory listing and seek to the file you just came from. Keep bouncing to go up, up, up. Having rapid directory access available changes everything.
 `cg` or `cl` | Press `cg` or `cl` to `:cd` or `:lcd` to the currently edited directory.
`~` | Press `~` to go home.
`I` | Press `I` to toggle display the help at the top of the File Explorer.  All that annoying crap at the top is turned off, leaving you with nothing but a list of files. This is surprisingly disorienting, but ultimately very liberating.
`.`  |  Press `.` on a file to pre-populate it at the end of a : command line. This is great, for example, to quickly initiate a `:grep` of the file or directory under the cursor. There's also `!`, which starts the line off with a bang. Type `!chmod +x` and get `:!chmod +x path/to/file`.
`gh` | Press `gh` to toggle dot file hiding. Enabled if add `g:netrw_list_hide` = `'\(^\|\s\s\)\zs\.\S\+'` to your vimrc. vinegar will initialize with dot files hidden.

Other changes:

* The oddly C-biased default sort order is replaced with a sensible application of 'suffixes'.
* File hiding: files are not listed that match with one of the patterns in 'wildignore'.

## <a id="vimgrep">Vimgrep</a>
http://vimcasts.org/episodes/search-multiple-files-with-vimgrep/

We can use the `:vimgrep` command to populate the quickfix list with search results from the current file:

```
:vimgrep /{pattern}/ %
```

The `%` character is a special symbol that represents the filepath of the active buffer.

> Within out The `j` flag Vim jups to the first match. With `j` only the quickfix list is updated. With `[!]` all changes in the current buffer are abandoned. 

### Navigating the quickfix list
Matches returned by Vimgrep query are loaded into a quickfix list. You can navigate through the quickfix list using the following commands:

Command | Unimpaired |  Action
---     |  ------ |  ------
`:cprev[ious]` |  `[q` | Reverse through quickfix list.
`:cnext` |  `]q` |     Advance through quickfix list.
`:cfirst` | `[Q` |     Go to start of quickfix list.
`:clast` |  `]Q` |     Go to end of quickfix list.

### Some patterns

Pattern | Returns 
---     |  ------
`` /\v`[^`]*` `` | Returns strings enclosed within backticks.
`s:\s*$::` | Drops the blanks from the end of a line.
`s:\s\+$::` | Does not act on all lines

### Recursive Search

You can use `**` in the file pattern to search recursively. For example, to search for all lines containing _dostuff()_ in all `.c` files in the parent directory and all its subdirectories, use:

```
:vimgrep /dostuff()/j ../**/*.c
```

### Searching for the last pattern

To search for the last pattern the search history:
```
:vimgrep /<C-r>// %
```

On the command line, `<C-r>/` (i.e. `CTRL-R` followed by the `/`) returns the last search pattern.


### Regex patterns

Some examples of `:global` usage: 

Pattern | Returns 
---     |  ------
`:g/^$/ d` | Delete all empty lines in a file
`:g/^$/,/./-j` | Reduce multiple blank lines to a single blank
`:10,20g/^/ mo 10`| Reverse the order of the lines starting from the line 10 up to the line 20.
`:'a,'b g/^Error/ . w >> errors.txt` | Here is a modified example from Walter Zintz vi tutorial. In the text block marked by 'a and 'b find all the lines starting with Error and copy (append) them to "errors.txt" file. Note: . (current line address) in front of the w is very important, omitting it will cause :write to write the whole file to "errors.txt" for every Error line found.

You can give multiple commands after :global using "|" as a separator. If you want to use "|' in an argument, precede it with "\'. Another example from Zintz tutorial:

```
:g/^Error:/ copy $ | s /Error/copy of the error/
```

Will copy all Error line to the end of the file and then make a substitution in the copied line. Without giving the line address :s will operate on the current line, which is the newly copied line.

Here the order is reversed: first modify the string then copy to the end:

```
:g/^Error:/ s /Error/copy of the error/ | copy $
```

## <a id="airline">Vim Airline</a>

To view help:

```
:help airline
```

## <a id="various">Various</a>

### <a id="markdown">Markdown Preview</a>

I installed grip using homebrew. Grip provides the Github flavored markdown formatting.

```
$ grip filename.md
```

### URLs
Command | Action
---     | ------
`gx` |  Opens URL under cursor.

 
### <a id="emojis">Emojis</a>
http://www.webpagefx.com/tools/emoji-cheat-sheet/


## <a id="cli">Command Line</a>


Exiting the shell returns to vim.

To run  Linux commands within Vim using the bang commmand:

```
:! command
```

To start a specific shell within Vim use the band command:

```
:! bash
```

Or: 

```
:sh[ell]
```

## <a id="javascript">JavaScript & Node</a>
https://github.com/nodejs/node/wiki/Vim-Plugins

http://vimawesome.com/plugin/node

## <a id="rest">Restructured Text</a>
A naïve approach (no plugins or scripting) would be `Esc`+ `Y` + `p` + `V` + `r` + `=`

* `Y` + `p` duplicates the current line and puts the cursor on the lower line.
* `V` selects the second line in Visual Line mode.
* `r` + `=` replaces all characters on the line with the `=` character.

You can `:noremap` that keystroke sequence to your taste.

For example

```
" Add Heading: Control-H
nnoremap <C-h> YpVr
```



Leaving off the last character so you can type in whichever you want for the title.

