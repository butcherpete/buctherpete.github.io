---
title: Bash Data 
tags: [bash]
keywords:  
last_updated: February 6, 2017
summary: A list of essential command line skills for onboarding operations team members.
sidebar: notes_sidebar
permalink: bash_data.html
folder: notes 
---

## File Viewing

### head / tail 

### less 

## Text Manipulation

### cut / paste 

### sort

### tee 

## Screen Output

### clear

### pbcopy

```
$ cat mydoc | pbcopy
```

### pbpaste

### script

> The script utility makes a typescript of everything printed on your terminal.  It is useful for students who need a hardcopy record of an interactive session as proof of an assignment, as the typescript file can be printed out later with lpr(1).

```
$ script -akq -t <time> [command]
```

Flag        | Description
-------     | -----------
-a          | Append to file or typescript.
-k          | Logs keys as well as output.
-q          | Quiet mode; omit start & stop.
-t          | Time interval. Default 30 seconds.

## File Comparison 

### diff 

### md5 

### shasum
