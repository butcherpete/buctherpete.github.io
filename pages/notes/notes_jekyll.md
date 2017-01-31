---
title: Jekyll Notes 
tags: [jekyll, ruby]
keywords: jekyll, notes 
last_updated: January 30, 2017
summary: Jekyll is a blog-aware, static site generator in Ruby.
sidebar: notes_sidebar
permalink: notes_jekyll.html
toc: false
folder: notes 
---

## Serving Pages

To serve pages locally:

```
$ jekyll serve
```
A development server runs at <http://localhost:4000/>

By default, the site is automatically regenerated based on local changes. To disable automatic updates, run using the  `--no-watch` option. 

```
$ jekyll serve --no-watch
```

To run the server in background mode, use the `--detatch` option:

```
$ jekyll serve --detach
```
{% include important.html content="Remember to kill the server. Run `kill -9 1234`,  where _1234_ is the process ID." %}


## Building Sites
To generate the current folder into `./_site`:

```
$ bundle exec jekyll build 
```
By default the _SOURCE_ is the current folder and the _DESTINATION_ is `./_site`.

To specify the source and destination folders:

```
$ bundle exec jekyll build --source SOURCE --destination DESTINATION
```

### Debugging Build Errors 
To view details of the build:

```
$ bundle update
$ bundle exec jekyll build --trace --verbose
```

### Watching for Changes
To watch the current folder for changes and regenerate into `./_site`:

```
$ bundle exec jekyll build --watch
``` 
{% include callout.html content="**Changes to `_config.yml` are not included during automatic regeneration** <br/><br/>  The `_config.yml` master configuration file contains global configurations and variable definitions that are read once at execution time. Changes made to `_config.yml` during automatic regeneration are not loaded until the next execution." type="primary" %} 

A complete list of `jekyll build` options:

Option | Operation 
----     |  ------
`--config` _CONFIGFILE[,CONFIGFILE2,...]_ |   Custom configuration file.
`-d,` `--destination` _DESTINATION_ |  The current folder will be generated into DESTINATION.
`-s,` `--source` _SOURCE_ |  Custom source directory.
`--future`    |    Publishes posts with a future date.
`--limit_posts` _MAXPOSTS_  |  Limits the number of posts to parse and publish.
`-w`, `--[no-]watch` |   Watch for changes and rebuild.
`-b`, `--baseurl` _URL_  |  Serve the website from the given base URL.
`--force_polling`  |  Force watch to use polling.
`--lsi`        |   Use LSI for improved related posts.
`-D`, `--drafts` |       Render posts in the `_drafts` folder.
`--unpublished`  | Render posts that were marked as unpublished.
`-q`, `--quiet`    |    Silence output.
`-V`, `--verbose`  |    Print verbose output.
`-I`, `--incremental` | Enable incremental rebuild.
`-s`, `--source` _[DIR]_ | Source directory (defaults to `./`).
`-d`, `--destination` _[DIR]_ |  Destination directory (defaults to `./_site`).
`--safe`     |    Safe mode (defaults to false).
`-p`, `--plugins` _PLUGINSDIR1[,PLUGINSDIR2[,...]]_ |  Plugins directory (defaults to `./_plugins`).
`--layouts` _DIR_  | Layouts directory (defaults to `./_layouts`).
`--profile`     |  Generate a Liquid rendering profile.
.-h,. `--help`   |       Show this message.
`-v`,	 `--version`  |    Print the name and version.
`-t`, `--trace`     |   Show the full backtrace when an error occurs.


## Command Line Options

### Usage

`jekyll <subcommand> [options]`

### Options

Option | Operation 
----     |  ------
`-s,` `--source` _[DIR]_ |  Source directory (defaults to `./`).
`-d,` `--destination` _[DIR]_ |  Destination directory (defaults to `./_site`).
`--safe`      |    Safe mode (defaults to false).
`-p,` `--plugins` _PLUGINSDIR1[,PLUGINSDIR2[,...]]_  | Plugins directory (defaults to `./_plugins`).
`--layouts` _DIR_  |  Layouts directory (defaults to `./_layouts`).
`--profile`   |    Generate a Liquid rendering profile.
`-h,` `--help`   |       Show this message.
`-v,` `--version` |      Print the name and version.
`-t,` `--trace`    |     Show the full backtrace when an error occurs.

### Subcommands

Subcommand | Operation 
----     |  ------
`docs` | 
`import` |
`build`, `b` |              Build your site.
`clean` |                 Clean the site (removes site output and metadata file) without building.
`doctor`, `hyde` |          Search site and print specific deprecation warnings
`help` |                  Show the help message, optionally for a given subcommand.
`new` |                   Creates a new Jekyll site scaffold in PATH.
`new-theme` |             Creates a new Jekyll theme scaffold.
`serve`, `server`, `s` |      Serve your site locally.

