---
title: Syntastic 
tags: [vim]
keywords: vim 
last_updated: February 7, 2017
summary:  Syntastic is a syntax checking plugin for Vim created by Martin Grenfell. It runs files through external syntax checkers and displays any resulting errors to the user. This can be done on demand, or automatically as files are saved. If syntax errors are detected, the user is notified and is happy because they didn't have to compile their code or execute their script to find them.
sidebar: notes_sidebar
permalink: vim_syntastic.html
folder: vim 
---

## Syntastic

[vim-syntastic/syntastic](https://github.com/vim-syntastic/syntastic)

[Syntastic Documentation](https://github.com/vim-syntastic/syntastic/blob/master/doc/syntastic-checkers.txt)

### Recommended Settings

> Syntastic has numerous options that can be configured, and the defaults are not particularly well suitable for new users. It is recommended that you start by adding the following lines to your vimrc file, and return to them after reading the manual. (cf. `:help syntastic` in Vim)

`````
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
`````

### Viewing Available Checkers 

~~~~~
:SyntasticInfo
~~~~~

### Adding Checkers to File Types

In the `.vimrc`, add a line that specifies the file type and one or more checkers:

~~~~~
# Syntax
let g:syntastic_<filetype>_checkers = ['<checker-name>']

# To add one checker
let g:syntastic_python_checkers = ['pylint']

# To add multiple checkers:
let g:syntastic_php_checkers = ['php', 'phpcs', 'phpmd']
~~~~~

### Toggling Between Modes

Syntastic has two modes: active mode and passive mode. Active mode checks on writing to the buffer. Passive mode requires manual intervention.

To toggle between Synastic modes:

~~~~~
:SyntasticToggleMode
~~~~~



### Running Checkers Manually

~~~~~
:SyntasticCheck phpcs phpmd
~~~~~

## Tidy

[Tidy Documentation](http://www.html-tidy.org/documentation/)

### Configuration Files

[Syntastic HTML:tidy](https://github.com/vim-syntastic/syntastic/wiki/HTML:---tidy)

If tidy produces the error that you want to ignore, add an exception to your `vimrc`:

`````
let g:syntastic_html_tidy_ignore_errors = [ '<input> proprietary attribute "role"' ]
let g:syntastic_html_tidy_ignore_errors = [ '<img> lacks "alt" attribute' ]
`````
The relevant error message is in single quotes.

> I have added the `<img> lacks "alt" attribute` error because the `<alt>` is not required in HTML5. We use `figcation`s instead.

## Proselint

[amperser/proselint](https://github.com/amperser/proselint)

### Disabling Checks

You can disable any of the checks by modifying `~/.proselintrc`:

~~~~~
{
  "checks": {
    "typography.diacritical_marks": false,
  	"typography.symbols": false,
  	"leonard.exclamation": false

  }
}
~~~~~

The following checkers are disabled:

-  	"typography.symbols": Insists on recommending smart quotes. Not in HTML, you don't. 
-  	"leonard.exclamation": Insists on flagging bang/exclamation marks. Not in Swift documentation. 

