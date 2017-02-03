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


## Markdown Preview

I installed grip using homebrew. Grip provides the Github flavored markdown formatting.

```
$ grip filename.md
```

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


