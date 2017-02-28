---
title: fasd 
tags: [bash, vim]
keywords:  
last_updated: February 21, 2017
summary: Fasd (pronounced similar to "fast") is a command-line productivity booster. Fasd offers quick access to files and directories for POSIX shells. It is inspired by tools like autojump, z and v. Fasd keeps track of files and directories you have accessed, so that you can quickly reference them in the command line.
sidebar: notes_sidebar
permalink: bash_fasd.html
folder: notes 
---

[civv/fasd](https://github.com/clvv/fasd)

"The name fasd comes from the default suggested aliases f(files), a(files/directories), s(show/search/select), d(directories)."

## Setup

To install `fasd`, use homebrew:

~~~
$ brew fasd
~~~

To enable `fasd` in a shell, initialize it with the command: 

~~~
$ eval "$(fasd --init auto)"
~~~

To enable autocompletion in bash, call `_fasd_bash_hook_cmd_complete`:

~~~
_fasd_bash_hook_cmd_complete v m j o
~~~

## Commands

~~~
fasd [options] [query ...]
[f|a|s|d|z] [options] [query ...]
  options:
    -s         list paths with scores
    -l         list paths without scores
    -i         interactive mode
    -e <cmd>   set command to execute on the result file
    -b <name>  only use <name> backend
    -B <name>  add additional backend <name>
    -a         match files and directories
    -d         match directories only
    -f         match files only
    -r         match by rank only
    -t         match by recent access only
    -R         reverse listing order
    -h         show a brief help message
    -[0-9]     select the nth entry

fasd [-A|-D] [paths ...]
    -A    add paths
    -D    delete paths
~~~

## Aliases

~~~
alias a='fasd -a'        # any
alias s='fasd -si'       # show / search / select
alias d='fasd -d'        # directory
alias f='fasd -f'        # file
alias sd='fasd -sid'     # interactive directory selection
alias sf='fasd -sif'     # interactive file selection
alias z='fasd_cd -d'     # cd, same functionality as j in autojump
alias zz='fasd_cd -d -i' # cd with interactive selection
~~~

## Tweaks

Some shell variables that you can set before sourcing fasd. You can set them in $HOME/.fasdrc

~~~
$_FASD_DATA
Path to the fasd data file, default "$HOME/.fasd".

$_FASD_BLACKLIST
List of blacklisted strings. Commands matching them will not be processed.
Default is "--help".

$_FASD_SHIFT
List of all commands that needs to be shifted, defaults to "sudo busybox".

$_FASD_IGNORE
List of all commands that will be ignored, defaults to "fasd ls echo".

$_FASD_TRACK_PWD
Fasd defaults to track your "$PWD". Set this to 0 to disable this behavior.

$_FASD_AWK
Which awk to use. Fasd can detect and use a compatible awk.

$_FASD_SINK
File to log all STDERR to, defaults to "/dev/null".

$_FASD_MAX
Max total score / weight, defaults to 2000.

$_FASD_SHELL
Which shell to execute. Some shells will run faster than others. fasd
runs faster with dash and ksh variants.

$_FASD_BACKENDS
Default backends.

$_FASD_RO
If set to any non-empty string, fasd will not add or delete entries from
database. You can set and export this variable from command line.

$_FASD_FUZZY
Level of "fuzziness" when doing fuzzy matching. More precisely, the number of
characters that can be skipped to generate a match. Set to empty or 0 to
disable fuzzy matching. Default value is 2.

$_FASD_VIMINFO
Path to .viminfo file for viminfo backend, defaults to "$HOME/.viminfo"

$_FASD_RECENTLY_USED_XBEL
Path to XDG recently-used.xbel file for recently-used backend, defaults to
"$HOME/.local/share/recently-used.xbel"
~~~
