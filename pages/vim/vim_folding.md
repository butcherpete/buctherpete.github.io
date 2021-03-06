---
title: Vim Folding 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_folding.html
folder: vim 
---

<http://vimcasts.org/episodes/how-to-fold/>

<https://github.com/nelstrom/vim-markdown-folding>


## Essentials

Command  |  Action
---     |  ------
`zi`  | Switch folding on or off
`za`  | Toggle current fold open/closed
`zc`  | Close current fold
`zR`  | Open all folds
`zM`  | Close all folds
`zv`  | Expand folds to reveal cursor
`:FoldToggle` | Toggles between flat and nested folding in vim-markdown-folding.

## Navigation 

To navigate an unfolded document:

Command  |  Action
---     |  ------
`zj`  | Move down to toop of the next fold.
`zk`  | Move up the bottom of the previous fold.
 
## More Commands 

Command  |  Action
---     |  ------
`zo`  | Open the current fold.
`zO`  | Recursively Open the current fold.
`zc`  | Close the current fold.
`zC`  | Recursively close the current fold.
`za`  | Toggle the current fold.
`zA`  | Recursively toggle the current fold.
`zm`  | Reduce the fold-level by one.
`zM`  | Close all folds.
`zr`  | Increase the fold-level by one.
`zR`  | Open all folds.
