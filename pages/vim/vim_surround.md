---
title: Vim Surround 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: mydoc_sidebar
permalink: vim_surround.html
folder: vim 
---

## Vim Surround

* Delete surroundings: `ds`
* Change surroundings: `cs` | `cS`
* Add surroundings: `ys` | `yS` | `ySS`
* Visual mode: `vS` | `vgS`

https://github.com/tpope/vim-surround

### Change Surroundings
Change surroundings is `cs` .  It takes two arguments, a target like with `ds`, and a replacement.

`cS` changes surroundings, placing the surrounded text on its own line(s) like `yS`.  Details about the second argument can be found below in _surround-replacements_.  Once again, examples are in order.

Before | Action | After
--- | ------| ------
"Hello *world!" | `cs"'` | 'Hello world!'
"Hello *world!" | `cs"<q>` |  <q>Hello world!</q>
(123+4*56)/2 | `cs)]`   |       [123+456]/2
(123+4*56)/2  | `cs)[`  |        [ 123+456 ]/2
\<div>Yo!*\</div>  | `cst<p>`  |      <p>Yo!</p>

Description:

Key | Action
--- | ------
`cs"'` | Replaces surrounding `"` with `'`
`cs'<q>` | Replaces surrounding `'` with `<q>`
`cst"` | Replaces surrounding tag with `"`


### Delete Surroundings
Delete surroundings is `ds`.  The next character given determines the targetted delete.  The exact nature of the target is explained in _surround-targets_ but essentially it is the last character of a _text-object_.

This mapping deletes the difference between the "i"nner object and "a"n object.  This is easiest to understand with some examples:

Before | Action | After
--- | ------| ------
"Hello *world!"  |    `ds"`  |   Hello world!
(123+4*56)/2 |   `ds)`  |        123+456/2
\<div>Yo!*\</div>  |  `dst`   |       Yo!

### Add Surroundings
`ys` takes a valid Vim motion or text object as the first object, and wraps it using the second argument as with `cs`.  (It's a stretch, but a good mnemonic for `ys` is "you surround".)

Before | Action | After
--- | ------| ------
Hello w*orld!  |           `ysiw)`   |    Hello (world)!

As a special case, *yss* operates on the current line, ignoring leading
whitespace.

Before | Action | After
--- | ------| ------
Hello w*orld!   |      `yssB`      |      {Hello world!}

There is also `yS` and `ySS` which indent the surrounded text and place it on a line of its own.


Description:

Key | Action
--- | ------
`ysiw]` | Surrounds text object with `]`
Visual select + `S<p class="x">` | Surround text in element.

### Visual Mode Surroundings

### Targets

The  Vim Surround `ds` and `cs` commands both take a target as their first argument.  The possible targets are based closely on the _text-objects_ provided by Vim.

All targets are currently just one character.

#### Punctuation Marks
Eight punctuation marks, `(`, `)`, `{`, `}`, `[`, `]`, `<`, and `>`, represent themselves and their counterparts.

If the opening mark is used, contained whitespace is
also trimmed.  The targets `b`, `B`, `r`, and `a` are aliases for `)`, `}`, `]`, and `>` (the first two mirror Vim; the second two are completely arbitrary and subject to change).

#### Quotation Marks
Three quote marks, `'`, `"`, `` ` ``, represent themselves, in pairs.  They are only searched for on the current line.

#### Tag Alias
A `t` is a pair of HTML or XML tags.  See _tag-blocks_ for details.

Remember that you can specify a numerical argument if you want to get to a tag other than the innermost one.

The letters `w`, `W`, and `s` correspond to a _word_, a _WORD_, and a _sentence_, respectively.  These are special in that they have nothing to delete, and used with `ds` they are a no-op.  With `cs`, one could consider them a slight shortcut for `ysi` (`cswb` == `ysiwb`, more or less).

A `p` represents a _paragraph_.  This behaves similarly to w, W, and s above; however, newlines are sometimes added and/or removed.

