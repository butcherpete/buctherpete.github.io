---
title: Vim Buffers 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_buffers.html
folder: vim 
---


## Navigating the Buffer List 

[Vimcast: Working with Buffers](http://vimcasts.org/episodes/working-with-buffers/)

These commands show and navigate through the buffer list: 

Command  | Action
----     |  ------
`:ls` |  Show the buffer list
`:bn` | Open the next buffer in the current window (cycles from the end of the list to the beginning).
`:bp` |  Open the previous buffer in the current window (cycles from the start of the list to the end).
`:b2` |  Open buffers in the current window by specifying the buffer number.
`CTRL-^` |   Switch to the alternate file.


Explaining the buffer list:

Symbol  |  Meaning
----     |  ------
`a`  | Identifes the active buffer.
`h` | Identifies a hidden buffer.
`%` | Identfies the buffer displayed in the current window.
`#` | Identifies the alternate buffer, which can be accessed by pressing `CTRL-^`.


## Opening Multiple Files into Buffers

To open the contents of a directory into the buffer:

```
:args /path_to_dir/*
```

To open multiple files into the buffer list:

```
:args a.txt b.txt c.txt 
```

To open open files into the buffer list using globs:

Glob | Matching Files
--- | ---
`:args *.*` | `index.html` <br/> `app.js`
`:args *.txt` | `a.txt` <br/> `b.txt`
`:args **.js` | `app.js` <br/> `lib/framework.js` <br/> `app/controllers/mailer.js`
`:args **/*.*` | `index.html` </br> `app.js` <br/> `lib/framework.js` <br/> `lib/theme.css` <br/>  `app/controllers/mailer.js`

From _Practical Vim_.

## Closing Buffers

Command  | Action
----     |  ------
`:bd` | Close the current buffer.
`:bw2` | Close buffers by specifying he buffer number, i.e. `:bw2`
`:1,3bw` | Close a range of buffers.


## Buffers in Airline

Tab line in airline automatically displays all buffers if only one tab open. Added the following to my `.vimrc` file:

```
let g:airline#extensions#tabline#enabled = 1
```

## Argdo Command

[Vimcast: Using :argdo to change multiple files](http://vimcasts.org/episodes/using-argdo-to-change-multiple-files/)

### Substitutions in Multiple Buffers 

To make substitutions to buffers in the arglist:

```
:argdo %s/mydoc_sidebar/notes_sidebar/ge
```
The `e` flag suppresses errors that may occur if a buffer in the arglist does not contain a match for the specified pattern.

### Reverting Changes

To revert changes:

```
:argdo edit!
```

### Saving Changes

To save changes to files in arglist:

```
:argdo update
```
