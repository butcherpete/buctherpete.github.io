---
title: Vim Restructured Text 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_rest.html
folder: vim 
---

## Marking Up Headers

A naïve approach (no plugins or scripting) would be `Esc`+ `Y` + `p` + `V` + `r` + `=`

1. `Y` + `p` duplicates the current line and puts the cursor on the lower line.
2. `V` selects the second line in Visual Line mode.
3. `r` + `=` replaces all characters on the line with the `=` character.

You can `:noremap` that keystroke sequence to your taste.

For example

```
" Add Heading: Control-H
nnoremap <C-h> YpVr
```
Leaving off the last character so you can type in whichever you want for the title.
