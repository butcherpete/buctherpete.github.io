---
title: Vim Miscellany 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_misc.html
folder: vim 
---

## Useful Commands

[Stackoverflow: Simple Vim commands you wish you'd known earlier](https://stackoverflow.com/questions/1276403/simple-vim-commands-you-wish-youd-known-earlier)

## Markdown Preview

I installed grip using homebrew. Grip provides the Github flavored markdown formatting.

```
$ grip filename.md
```

## Fenced Code Blocks


`Esc` + *n* + `i` + `~` + `Esc`

For example `5i~Esc`.

~~~~~ swift
Code Sample
~~~~~

## Pandoc

[Vimcast 64:Using external filter commands to reformat HTML](http://vimcasts.org/episodes/using-external-filter-commands-to-reformat-html/)

Use the bang Ex command to filter the contents of the current buffer through a pandoc pipeline:

~~~
:%!pandoc --from=html --to=markdown | pandoc --from=markdown --to=html
~~~

## URLs

Command | Action
---     | ------
`gx` |  Opens URL under cursor.

 
## Emojis

<http://www.webpagefx.com/tools/emoji-cheat-sheet/>


