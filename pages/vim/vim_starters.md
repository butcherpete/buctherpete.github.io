---
title: Vim Starters 
tags: [vim]
keywords: vim 
last_updated: January 29, 2017
summary: "A crib of Vim tips and tricks."
sidebar: notes_sidebar
permalink: vim_starters.html
folder: vim 
---

To get information:

```
:version
```

## Brew

Installed with Homebrew.

* Version: 8.0.52
* Location: `/usr/local/bin/vim` ### Vimrc To edit: 

```
$ vim ~/.vimrc
```

To reload (source) changes to the `.vimrc` from within the .vimrc file:

```
:so %
```

The character `%` stands for the current file name (see `:h current-file`).

Otherwise:

```
:so $MYVIMRC
```

## Vundle

To install in Vim, launch vim and run:

```
:PluginInstall
```

To install from command line:

```
$ vim +PluginInstall +qall
```
To read docs:

```
:h vundle
```

