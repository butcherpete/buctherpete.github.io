---
title: ACK Notes 
tags: [bash]
keywords:  
last_updated: February 6, 2017
summary: Notes on ACK
sidebar: notes_sidebar
permalink: ack_notes.html
folder: notes 
---
## Returning File Names Only
[Stackoverflow](https://serverfault.com/questions/57321/how-do-i-show-filenames-only-after-a-keyword-grep-search)
You can use xargs in combination with --null with grep or --print0 with ack. I find that ack speed is faster.

~~~~~
ack  -lr --print0 searchterm * | xargs -I {} -0 echo {}
~~~~~
