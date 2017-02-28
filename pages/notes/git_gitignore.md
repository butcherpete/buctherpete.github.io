---
title: gitignore & gitattributes
tags: [git]
keywords: git, customization 
last_updated: February 19, 2017
summary: A few notes about the .gitignore and .gitattributes files.
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

## .gitattribute Files

### Identifying Binary Files

### Diffing Word (.docx) Files

A way of tracking between Word files in Git using `docx2txt` command line utility, `.gitattributes` file, and Git configurations.

Once enabled, Git processes diffs of files ending in `.docx`using the user-defined "word" filter (the docx2txt program). The docx2txt program generates text files from Word docs whenever Git performs a diff on those files. 

Changes in formatting are not identified, but you can track changes to the text.  

1. Add to .gitattributes file:

   ```
   *.docx diff=word
   ```

2. Install docx2txt.

   ```
   $ brew install docx2txt
   ```

3. Create a Bash script called docx2txt that converts Word documents into a format that Git can read.

   ```
   #!/bin/bash
   docx2txt.pl $1 -
   ```

4. Make the script executable and place it in your PATH

   ```
   $ chmod a+x
   ```

5. Configure Git to use the script.

   ```
   $ git config diff.word.textconv docx2txt
   ```


