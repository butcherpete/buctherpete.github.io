---
title: Jekyll Resources 
tags: [jekyll]
keywords: jekyll 
last_updated: January 30, 2017
summary: A list of useful Jekyll resources.
sidebar: notes_sidebar
permalink: jekyll_resources.html
toc: false
folder: notes 
---

## Jekyll 

* [Jekyll Documentation](https://jekyllrb.com/docs/home/)
* [Jekyll on Stackoverflow](https://stackoverflow.com/questions/tagged/jekyll)
* [I'd Rather Be Writing](http://idratherbewriting.com/category-jekyll/)
* [How to create data-driven navigation in Jekyll](http://www.tournemille.com/blog/How-to-create-data-driven-navigation-in-Jekyll)
* [Jekyll F.A.Q.s](https://github.com/planetjekyll/quickrefs/blob/master/FAQ.md)

## Jekyll Themes 
* [documentation-theme-jekyll](https://github.com/tomjohnson1492/documentation-theme-jekyll)

## Github Pages 

* [Github Pages Help](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)

## Static Site Generators

* [StaticGen](https://www.staticgen.com/)

## Jekyll Sites

- [eb](https://eduardoboucas.com/)
- [Including and Managing Images in Jekyll](https://eduardoboucas.com/blog/2014/12/07/including-and-managing-images-in-jekyll.html)
- [Web Development Notes](http://dev-notes.eu/jekyll/)

## Jekyll File Structure

This is the default tree structure:

~~~~~
`root`/
│── `.gitignore`
│── `.sass-cache`
│── `config-yml`
│── `_posts`/
│── `about.md`
│── `Gemfile`
│── `Gemfile.lock`
└── `index.md`
~~~~~

Gem-based theme system. The default theme is `minima`. To view the `minima` files, run the follow command:

~~~~~
$ bundle show minima
/usr/local/lib/ruby/gems/2.4.0/gems/minima-2.1.0

$ open  /usr/local/lib/ruby/gems/2.4.0/gems/minima-2.1.0
~~~~~

Copy the files to the directory. The local files will overwrite the remote files.

~~~~~
`root`/
│── `.gitignore`
│── `.sass-cache`
│── `config-yml`
│── `_posts`/
│── `_layouts`/
│── `_sass`/
│── `_site`/
│── `assets`/
│── `index.md`
│── `LICENSE.md`
│── `README.md`
│── `about.md`
│── `Gemfile`
└── `Gemfile.lock`

~~~~~



