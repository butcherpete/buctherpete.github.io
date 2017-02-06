---
title: Vim Git 
tags: [vim, git]
keywords: vim 
last_updated: February 1, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_git.html
folder: vim 
---

## Resources
[Drew Neil on Vim and Workflow](https://www.youtube.com/watch?v=GUptUQGrJLE)

## Vim as Diff Tool


### Configuration
[Viewing all `git diffs` with vimdiff](https://stackoverflow.com/questions/3713765/viewing-all-git-diffs-with-vimdiff)

~~~~~
git config --global diff.tool vimdiff
git config --global difftool.prompt false
git config --global alias.d difftool
~~~~~

Typing `git d` yields the expected behavior, typing `:wq` in vim cycles to the next file in the changeset.

## Comparing Two Files
[How do I use vim as a diff tool?](https://vi.stackexchange.com/questions/625/how-do-i-use-vim-as-a-diff-tool)

To open two files in Vim using vimdiff:

~~~~~
# Use -d flag
$ vim -d <file1> <file2>

# Use vimdiff wrapper app
$ vimdiff <file1> <file2>
~~~~~

To run vimdiff within Vim to compare two files in a new tab:

~~~~~
:tabe file1
:vert diffsplit file2
~~~~~

To compare two files in the current tab:

~~~~~
:e file1
:vert diffsplit file2
~~~~~


## Fugitive

[vim-fugitive](https://github.com/tpope/vim-fugitive)

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
[Must Have Git Aliases: Advanced Examples](http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/)

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

## Gitgutter
[Git Gutter Plugin](https://github.com/jisaacks/GitGutter)

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


