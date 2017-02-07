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

## .ackrc

To view and edit the .ackrc:

~~~~~
$ vim ~/.ackrc
~~~~~

[Sample ackrc file](https://gist.github.com/bracke/6183737)

~~~~~
# Always sort the files
#--sort−files
 
# Always color, even if piping to a another program
--color
 
# Ignore case
--ignore-case
 
# Use "less −r" as my pager
# --pager

# Do not send output through a pager.
--nopager

# Print a break between results from different files.
--break

# Print a filename heading above each file's results.
--heading

# less -r
 
--ignore-dir=.idea/
--ignore-dir=node_modules/
--ignore-dir=.sass-cache/
--ignore-dir=.tmp/

--ignore-dir=.gist-cache
--ignore-dir=.pygments-cache
--ignore-dir=.sass-cache
--ignore-dir=.themes
--ignore-dir=_deploy
--ignore-dir=public
--ignore-dir=bower_components/
--ignore-dir=dist
 
#make sure ack knows how to search common filetypes used in rails projects
--type-add=css=scss
--type-add=ruby=.haml,.rselm,.feature,.ru,.lock
--type-set=coffeescript=.coffee
--type-set=coffee=.coffee
 
#make sure ack knows how to search common filetypes used in node.js projects
--type-set=coffee=.coffee
--type-set=jade=.jade
--type-set=feature=.feature
--type-set=json=.json

--type-add=css=.sass,.scss
--type-set=haml=.haml
--type-add=css=less
--type-set=markdown=.md,.mkd,.markdown
~~~~~

## Returning File Names Only
[Stackoverflow](https://serverfault.com/questions/57321/how-do-i-show-filenames-only-after-a-keyword-grep-search)
You can use xargs in combination with --null with grep or --print0 with ack. I find that ack speed is faster.

~~~~~
ack  -lr --print0 searchterm * | xargs -I {} -0 echo {}
~~~~~
