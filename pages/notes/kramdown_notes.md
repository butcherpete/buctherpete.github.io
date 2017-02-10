---
title: Kramdown Notes
tags: [vim, markdown, jekyll]
keywords: vim, jekyll
last_updated: February 1, 2017
summary: The kramdown syntax is based on the Markdown syntax and has been enhanced with features that are found in other Markdown implementations like Maruku, PHP Markdown Extra and Pandoc. 
sidebar: notes_sidebar
permalink: kramdown_notes.html
folder: vim 
---

## Kramdown
[kramdown Syntax](https://kramdown.gettalong.org/syntax.html)

[Updating your Markdown processor to kramdown](https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/)

> If you are not already using kramdown, Jekyll 3.0.0's default Markdown processor, then you must update your Markdown processor in your `_config.yml` file.
> GitHub Pages only supports kramdown as a Markdown processor.
> GitHub-flavored Markdown is supported by kramdown by default, so you can use Markdown with GitHub Pages the same way you use Markdown on GitHub.

[Updating from redcarpet and Pygments to Kramdown and Rouge on Github Pages](http://idratherbewriting.com/2016/02/21/bug-with-kramdown-and-rouge-with-github-pages/)

An example of the Jekyll `_config.yml` file:

~~~
markdown: kramdown
kramdown:
 input: GFM
 auto_ids: true
 hard_wrap: false
 syntax_highlighter: rouge
# filter used to process markdown. note that kramdown differs from github-flavored markdown in some subtle ways
~~~

* The `remove_block_html_tags` and  `remove_span_html_tags` kramdown options are not supported in Jekyll due to the fact that they are not included within the kramdown HTML converter.
* The `coderay_*` kramdown options are deprecated. 

###  Jekyll Markdown Processor Defaults

> Jekyll runs with the following configuration options by default. Alternative settings for these options can be explicitly specified in the configuration file or on the command-line.

~~~
rdiscount:
  extensions: []

redcarpet:
  extensions: []

kramdown:
  auto_ids:       true
  footnote_nr:    1
  entity_output:  as_char
  toc_levels:     1..6
  smart_quotes:   lsquo,rsquo,ldquo,rdquo
  input:          gfm
  hard_wrap:      false
  footnote_nr:    1
~~~

[kramdown options](https://kramdown.gettalong.org/rdoc/kramdown/options.html)

[jekyll markdown config options](https://jekyllrb.com/docs/configuration/#markdown-options)

[Kramdown Markdown Options (Defaults?) for Github Flavored Markdown (GFM) - Backticks](https://github.com/jekyll/jekyll/issues/4202)


