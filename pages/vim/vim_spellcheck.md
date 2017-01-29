---
title: Vim Spellchecking 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: mydoc_sidebar
permalink: vim_spellcheck.html
folder: vim 
---

http://vimcasts.org/episodes/spell-checking/

Spell check.

```
:set spell
```
Set spelling language to American English.

```
:set spelllang=en_us
```

Jump backward.

```
[s
```
Jump forward.

```
]s
```

Suggest correct spelling.

```
z=
```

To select a suggestion, enter the line number and press the Return key.

To take the first suggestion  without viewing the list, enter `1z=`.  To reverse the correction,  press the `u` key.

Add highlighted word spell file.

```
zg
```
Spell file location: `~/.vim/spell/en.utf-8.add`

To remove a highlighted word from spell file.

```
zug
```

