---
title: gitignore 
tags: [git]
keywords: git, customization 
last_updated: February 1, 2017
summary: A few notes about gitignore 
sidebar: notes_sidebar
permalink: git_gitignore.html
folder: notes 
---

[Ignoring Files](https://help.github.com/articles/ignoring-files/)

## Local .gitignore Files

### Adding Local .gitignore Files

To create a local `.gitignore` file:

1. In Terminal, go to the repository.
2. Enter `vim .gitignore` to create a `.gitignore` file.


### Patterns

The rules for the patterns you can put in the `.gitignore` file are as follows:

*  Blank lines or lines starting with # are ignored.
* Standard glob patterns work.
* You can start patterns with a forward slash (/) to avoid recursivity.
* You can end patterns with a forward slash (/) to specify a directory.
* You can negate a pattern by starting it with an exclamation point (!).

## Untracking Files

### Untracking Committed Files

> If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal:

```
$ git rm --cached FILENAME
```

### Untracking Modified Files

[Stackoverflow](https://stackoverflow.com/questions/10755655/git-ignore-tracked-files)

To untrack modified files:

```
$ git update-index --assume-unchanged file
```

To undo and start tracking files:

```
$ git update-index --no-assume-unchanged [<file> ...]
```

## Global .gitignore Files

### Adding Global .gitignore Files

To create a global `.gitignore` file:

```
$ git config --global core.excludesfile ~/.gitignore_global
```

### Guidelines for Global .gitignore Files

[octocat/.gitignore](https://gist.github.com/octocat/9257657)

```
# Compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log
*.sql
*.sqlite

# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```
