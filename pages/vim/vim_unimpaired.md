---
title: Vim Unimpaired 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_unimpaired.html
folder: vim 
---

```
:help unimpaired
```

The following maps all correspond to normal mode commands.  If a count is
given, it becomes an argument to the command.  A mnemonic for the "a" commands is "args" and for the "q" commands is "quickfix".

Key | Action
--- | ------
`[a`     |`:previous`|
`]a`     |`:next`|
`[A`     |`:first`|
`]A`     |`:last`|
`[b`     |`:bprevious`|
`]b`     |`:bnext`|
`[B`     |`:bfirst`|
`]B`     |`:blast`|
`[l`     |`:lprevious`|
`]l`     |`:lnext`|
`[L`     |`:lfirst`|
`]L`     |`:llast`|
`[<C-L>` |`:lpfile`|
`]<C-L>` |`:lnfile`|
`[q`     |`:cprevious`|
`]q`     |`:cnext`|
`[Q`     |`:cfirst`|
`]Q`     |`:clast`|
`[<C-Q>` |`:cpfile`| (Note that <C-Q> only works in a terminal if you disable flow control.)
`]<C-Q>` |`:cnfile`| 
`[t`     |`:tprevious`|
`]t`     |`:tnext`|
`[T`     |`:tfirst`|
`]T`     |`:tlast`|


