---
title: Git Diff 
tags: [git, vim]
keywords: git, vim
last_updated: February 6, 2017
summary: Git Diff notes 
sidebar: notes_sidebar
permalink: git_diff.html
folder: notes 
---

## A Diff Menagerie

Blow out your candles Laura.

[Git Diff Overview](https://stackoverflow.com/questions/1587846/how-do-i-show-the-changes-which-have-been-staged)

![git--diff-diagram](/images/git-diff-simple.png){:class="img-responsive"}

### Git Diff

Shows the changes between the working directory and the index. This shows what has been changed, but is not staged for a commit.

~~~~~
$ git diff
~~~~~


### Git Diff Cached/Staged

The commands `git diff --staged` and `git diff --cached` do the same thing: compare staged changes with committed changes.

Shows changes between the index and HEAD, the last commit this branch. This command shows everything that has been  added (`git add`) to the index and staged for a commit.

~~~~~
$ git diff --cached

# Running in Vim
:Git! diff --staged 
~~~~~

Fugitive does not support a command that directly corresponds to `git diff --cached`. [Fugitive Git Diff --Staged](https://stackoverflow.com/questions/15407652/how-can-i-run-git-diff-staged-with-fugitive)

### Git Diff Head 

Shows all the changes between the working directory and HEAD (which includes changes in the index). This shows all the changes since the last commit, whether or not they have been staged for commit or not.

~~~~~
$ git diff HEAD
~~~~~


