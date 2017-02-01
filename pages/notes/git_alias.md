---
title: Git Aliases 
tags: [git, vim]
keywords: git, customization 
last_updated: February 1, 2017
summary: A few notes about Git aliases 
sidebar: notes_sidebar
permalink: git_alias.html
folder: notes 
---

## Resources

[Must Have Git Aliases: Advanced Examples](http://durdn.com/blog/2012/11/22/must-have-git-aliases-advanced-examples/)

## Setting Git Aliases

To set a git alias:

```
$ git config --global alias.co checkout

$ git config --global alias.last 'log -1 HEAD'
```

Or edit the `.gitconfig` file.

```
ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate
```

To define the `alias` alias:

```
$ git config --global alias.alias "config --get-regexp ^alias\."
```

## Viewing Git Aliases

To view my aliases:

```
$ git alias
```
Or open the `.gitconfig`.

```
$ vim ~/.gitconfig
```

## My Git Aliases


Alias | Expansion 
--- | ------
`alias` | `config --get-regexp ^alias\`
`gst` | `status`
`co` | `checkout`
`br` | `branch`
`ci` | `commit`
`last` | `log -1 HEAD`
`logtree` | `log --graph --oneline --decorate --all`
`ls` | `log --pretty=format:%C(yellow)%h%Cred%d\ %Creset%s%Cblue\ [%cn] --decorate`
`ll` | `log --pretty=format:%C(yellow)%h%Cred%d\ %Creset%s%Cblue\ [%cn] --decorate --numstat`
`lds` | `log --pretty=format:%C(yellow)%h\ %ad%Cred%d\ %Creset%s%Cblue\ [%cn] --decorate --date=short`

## Vim Git Aliases

Alias | Expansion 
--- | ------
`:git gst` | git status
`:git co` | git checkout
`:git br` | git branch
`:git ci` | git commit
`:git unstage` | git reset HEAD --
`:git ls` | list commits w/ branch tag annotations
`:git ll` | list commits w/ changed files
`:git lds` | list commits w/ dates
`:git logtree` | list commits w/ graph
