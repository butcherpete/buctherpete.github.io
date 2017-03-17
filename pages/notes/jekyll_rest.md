---
title: jekyll-rst 
tags: [jekyll, rest, python]
keywords:  
last_updated: February 6, 2017
summary: This plugin adds ReStructuredText support to Jekyll and Octopress. It renders ReST in posts and pages, and provides a custom directive to support Octopress-compatible syntax highlighting.
sidebar: notes_sidebar
permalink: jekyll_rest.html
folder: notes 
---

## Installation

Install Docutils and Pygments.

1. Use virtualenv_burrito:

    ~~~
    $ curl -sL https://raw.githubusercontent.com/brainsik/virtualenv-burrito/master/virtualenv-burrito.sh | $SHELL
    $ source /Users/tes/.venvburrito/startup.sh
    $ mkvirtualenv jekyll-rst
    $ pip install docutils pygments
    ~~~

2. Install RbST.

3. If you use bundler with Octopress, add gem 'RbST' to your Gemfile in the development group, then run bundle install. Otherwise, gem install RbST.

4. Install the plugin.

    ~~~
    $ cd <jekyll-project-path>
    $ git submodule add https://github.com/xdissent/jekyll-rst.git _plugins/jekyll-rst
    ~~~
