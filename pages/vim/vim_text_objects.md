---
title: Vim Text Objects 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: mydoc_sidebar
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
`cit`  | delete tag contents & insert mode
`dit`  | delete tag contents
`vit`  | select tag contents & visual mode
`yit`  | this

## Text Objects Selection

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

