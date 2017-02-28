---
title: generator-jekyllized 
tags: [jekyll, npm, yeoman]
keywords: jekyll, notes 
last_updated: February 18, 2017
summary: generator-jekyllized is a very opinionated Yeoman generator built with Jekyll and gulp. You will be able to quickly scaffold your site and start developing. As you are working on your site your assets will automatically be updated and injected into your browser as well as your posts. When you are done developing and want to publish it you are two commands away from having everything optimized and published.
sidebar: notes_sidebar
permalink: jekyll_generator.html
folder: notes 
---

## File Structure

~~~
root/
    ├── _config.build.yml
    ├── _config.yml
    ├── .editconfig
    ├── .git/
    ├── .gitattributes
    ├── .gitignore
    ├── .tmp
    ├── Gemfile
    ├── Gemfile.lock
    ├── gulpfile.js
    ├── package.json
    ├── README.md
    ├── dist/
    │       ├── 404/ 
    │       ├── about/ 
    │       ├── assets/ 
    │       ├── crossdomain.xml 
    │       ├── feed.xml 
    │       ├── humans.txt 
    │       ├── index.html 
    │       ├── jekyll/ 
    │       ├── robots.txt 
    │       └── sitemap.xml 
    ├── gulp/
    │       └── tasks/ 
    │                ├── assets.js 
    │                ├── build.js 
    │                ├── clean.js 
    │                ├── copy.js 
    │                ├── fonts.js 
    │                ├── html.js 
    │                ├── images.js 
    │                ├── inject.js 
    │                └── uploading.js 
    ├── node_modules/                 
    └── src/
           ├── _drafts/          
           ├── _includes/ 
           │            ├── footer.html 
           │            ├── head.html 
           │            ├── header.html 
           │            ├── icon-github.html 
           │            ├── icon-github.svg 
           │            ├── icon-twitter.html 
           │            └── icon-twitter.svg 
           ├── _layouts/ 
           │            ├── default.html 
           │            ├── page.html 
           │            └── post.html 
           ├── _posts/ 
           ├── 404.html                 
           ├── about.md         
           ├── assets/ 
           │         ├── favicon.ico 
           │         ├── images/ 
           │         ├── javascript/ 
           │         └── scss/ 
           ├── crossdomain.xml 
           ├── humans.txt 
           ├── robots.txt 
           └── index.htm  
~~~

## Gemfile

~~~
source "http://rubygems.org"

gem 'jekyll'
gem 'redcarpet'

# jekyll plugins
gem 'jekyll-feed'
gem 'jekyll-gist'
gem 'jekyll-paginate'
gem 'jekyll-sitemap'
gem 'jekyll-seo-tag'
gem 'jekyll-redirect-from'
gem 'jekyll-compose', group: [:jekyll_plugins]
~~~
