---
title: Vim Search 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_search.html
folder: vim 
---

## Ack

[mileszs/ack.vim](https://github.com/mileszs/ack.vim)

[Ack Documentation](http://beyondgrep.com/documentation/)

### Ack Syntax

To search recursively in `{directories}`, which defaults to the current directory for the `{pattern}`.

```
:Ack[!] [options] {pattern} [{directories}]
```

Command  |  Action
-------  |  ------
`[!]`    |  If the `[!]` flag is provided, the first occurence is not immediately returned..
`[options]`    |  .
`{patterns}`    |  .
`[{directories}]`    |  Default is the current directory.

Files containing the search term are listed in the quickfix window, along with the line number of the occurrence, once for each occurrence. `<Enter>` on a line in this window will open the file, and place the cursor on the matching line.

### Ack Options

Command  |  Action
-------  |  ------
`-i`       |    Ignore case distinctions in PATTERN.
`-w`       |    Force PATTERN to match only whole words.
`-n`       |    No descending into subdirectories.
`-f`       |    Only print the files selected, without searching. The PATTERN must not be specified..
`-g`       |    Same as -`f`, but only select files matching PATTERN.
`--type=X`  | Include only X files, where X is a recognized filetype.
`--type=noX`  | Exclude X files. See `ack --help-types` for supported filetypes.

### Other Acks

Just like where you use `:grep`, `:grepadd`, `:lgrep`, and `:lgrepadd`, you can use `:Ack`, `:AckAdd`, `:LAck`, and `:LAckAdd` respectively.
 
Command  |  Action
-------  |  ------
`:AckAdd` |  Just like `:Ack`, but instead of making a new list, the matches are appended to the current `quickfix` list.
`:AckFromSearch [{directory}]` | Just like `:Ack` but the pattern is from previous search.
`:LAck` | Just like `:Ack` but instead of the `quickfix` list, matches are placed in the current `location-list`.
`:LAckAdd` | Just like `:AckAdd` but instead of the `quickfix` list, matches are added to the current `location-list`
`:AckFile` | Search recursively in {directory} (which defaults to the current directory) for filenames matching the `{pattern}`.  Behaves just like the `:grep` command, but will open the `Quickfix` window for you.
`:AckWindow[!] [options] {pattern}` | Search all buffers visible in the screen (current tab page only) files for the `{pattern}`.
`:LAckWindow [options] {pattern}` | Just like `:AckWindow` but instead of the `quickfix` list, matches are placed in the current location-list.


### Ack Keyboard Shortcuts

The quickfix results window is augmented with these convenience mappings:

Command  |  Action
---     |  ------
`?`  |    A quick summary of these keys, repeat to close.
`o`  |    To open (same as Enter).
`O`  | To open and close the quickfix window.
`go` | To preview file, open but maintain focus on ack.vim results.
`t`  |    To open in new tab.
`T`  |   To open in new tab without moving to it.
`h`  |   To open in horizontal split.
`H`  |   To open in horizontal split, keeping focus on the results.
`v`  |   To open in vertical split.
`gv` |   To open in vertical split, keeping focus on the results.
`q`  |   To close the quickfix window.

### Gotchas

Some characters have special meaning, and need to be escaped in your search pattern. For instance, `#`. You need to escape it with `:Ack '\\\#define foo'` to search for `'#define foo'`.

### Do Not Jump First Result Automatically

To not jump to the first result, use the bang (`!`) flag: `:Ack!`. 

If you want this behavior most of the time, you might like an abbreviation or mapping in your personal config, something like these:

```
cnoreabbrev Ack Ack!
nnoremap <Leader>a :Ack!<Space>
```

Most of the `:[L]Ack*` commands support this. Note that this behavior follows the convention of Vim's built-in `:grep` and `:make` commands.

## Vimgrep

<http://vimcasts.org/episodes/search-multiple-files-with-vimgrep/>

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


You can give multiple commands after :global using `|` as a separator. If you want to use `|` in an argument, precede it with `\`. Another example from Zintz tutorial:

```
:g/^Error:/ copy $ | s /Error/copy of the error/
```

Will copy all Error line to the end of the file and then make a substitution in the copied line. Without giving the line address :s will operate on the current line, which is the newly copied line.

Here the order is reversed: first modify the string then copy to the end:

```
:g/^Error:/ s /Error/copy of the error/ | copy $
```

