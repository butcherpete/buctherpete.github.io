---
title: Vim Buffers 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: mydoc_sidebar
permalink: vim_buffers.html
folder: vim 
---

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

