---
title: Visual Blocks 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "Visual mode is a flexible and easy way to select a piece of text for an
operator.  It is the only way to select a block of text."
sidebar: notes_sidebar
permalink: vim_visual_blocks.html
folder: vim 
---

[vimcasts 22: Selecting columns with visual block mode](http://vimcasts.org/episodes/selecting-columns-with-visual-block-mode/)

## Entering and Exiting Visual Modes

Command	| Action
-------- | --------
`v` | Enter Visual mode per character.
`V` | Enter Visual mode per line.
`CTRL-V` | Enter Visual mode per block.
`gv` | Enter Visual mode with the same area as the previous area and the same mode. 
`<Esc>` | Exit Visual Block Mode with insertion.
`CTRL-C`| Exit Visual Block Mode without insertion.

## Changing the Visual Area

Command	| Action
-------- | --------
`o`	| Toggle cursor to opposite corner.
`O`	| Toggle cursor to end of same line.
`$`	| Highlight to end of longest line.

## Operating on Visual Blocks 

Command	| Action
-------- | --------
`c` |	Change selection (delete and switch to insert mode).
`I`	| Insert in front of cursor.
`A`	| Append after cursor.
`r`	| Replace every character in selection.
`d`	| Delete selection.


## Selecting Columns in Visual Block Mode

To insert on multiple lines:

1. Move the cursor to the first letter of the first line.
2. Enter visual block mode (CTRL+v).
3. Press `j` to select to end of list.
4. Press `I`.
5. Type the prefix. For example, `*<space>`
6. Press the `<Esc>` key.

