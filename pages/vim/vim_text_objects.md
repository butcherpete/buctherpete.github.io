---
title: Vim Text Objects 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_text_objects.html
folder: vim 
---

## HTML Tags

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
`cit`  | Delete tag contents & insert mode.
`dit`  | Delete tag contents.
`vit`  | Select tag contents & visual mode.
`yit`  | Yank tag contents. 

## Text Objects Selection

Text Object  | Selection
---          | ------
`a)` / `i)`  | All / inside paretheses.
`a}` / `i}`  | All / inside braces.
`a]` / `i]`  | All / inside brackets.
`a>` / `i>`  | All / inside angle brackets.
`a'` / `i'`  | All / inside single quote.
`a"` / `i"`  | All / inside double quote.
`` a` `` / ``i` `` | All / inside backticks.
`at` / `it`  | All / inside tags.
`a_` / `i_`  | All / inside underscores. (vim-textobj-underscore)

## Custom Text Objects
[vim-textobj-user](https://github.com/kana/vim-textobj-user)

vim-textobj-user is a library plugin for Vim to define your own text objects without handling many edge cases and complex stuffs.

A list of predefined text objects implemented using `vim-textobj-user`.

[Text Object Plugins](https://github.com/kana/vim-textobj-user/wiki)

Plugins Installed:

* [vim-textobj-underscore](https://github.com/lucapette/vim-textobj-underscore): Works in Visual mode; In Default mode, works if cursor is over and underscore or blank space.

## targets-vim
I removed this plugin. It worked in Visual mode, but not in Default mode. Also it appeared to overwrite some default Vim behaviors and I was concerned that it might conflict with surround-vim.

[targets.vim](https://github.com/wellle/targets.vim)


