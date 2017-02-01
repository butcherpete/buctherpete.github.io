---
title: Vim HTML
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_html.html
folder: vim 
---

## HTML Cleanup

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

## Emmet

To expand shortcuts: `CTRL+y,`

### HTML Page
`html5:_`

## Matchit

To do, install machit

The `%` command jumps between matching parentheses. Matchit expands this behavior to include jumps between paired `< >`, HTML tags, or regex expressions.

## Vim-Ragtag

https://github.com/tpope/vim-ragtag

> A set of mappings for HTML, XML, PHP, ASP, eRuby, JSP, and more (formerly allml)

> This plugin started out as a set of personal mappings, but there was enough enjoyment among those I shared it with for me to clean it up and release it.
