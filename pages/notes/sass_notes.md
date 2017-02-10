---
title: Sass Notes 
tags: [sass, tooling]
keywords: sass, css 
last_updated: February 6, 2017
summary: Sass is an extension of CSS that adds power and elegance to the basic language. It allows you to use variables, nested rules, mixins, inline imports, and more, all with a fully CSS-compatible syntax. Sass helps keep large stylesheets well-organized, and get small stylesheets up and running quickly, particularly with the help of the Compass style library. 
sidebar: notes_sidebar
permalink: sass_notes.html
folder: notes 
---

## Resources
[Sass Reference](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)

## Sass & Jekyll

[How to use Sass with Jekyll (Bootstrap and Font Awesome example)](https://dalanzg.github.io/tips-tutorials/jekyll/2016/03/25/how-to-use-sass-with-jekyll/)

Jekyll project directory structure:

`````
jekyll-project/
├── _includes/
├── _layouts/
├── _posts/
├── _sass/
│   └── bootstrap/
│   │   └── bootstrap-sass-3.3.6/
│   |       └── assets
│   |           └── stylesheets/*
│   └── font-awesome/
│       └── font-awesome-4.5.0/
|            └── scss/*
├── css/
│   └── main.scss
├── fonts
│   └── bootstrap/
│   │   └── bootstrap-sass-3.3.6/
│   |       └── fonts 
│   |           └── bootstrap/*
│   └── font-awesome/
│       └── fonts/*
├── js
│   └── jquery/
|   |   └── jquery.min.js
│   └── bootstrap/
│        └── bootstrap-sass-3.3.6/
│            └── assets 
│                └── javascripts/
│                    └── bootstrap.min.js 
├── _config.yml
└── index.html
`````

### Setting Stylesheets and JavaScripts

To include the main stylesheet in the Jekyll head.

`````
<link rel="stylesheet" href="/css/main.css">
`````

To include the JQuery and Bootstrap JS files:

`````
<!-- jQuery -->
<script src="/tips-tutorials/js/jquery/jquery.min.js"></script>

<!-- Bootstrap Core JavaScript -->
<script src="/tips-tutorials/js/bootstrap/bootstrap.min.js"></script>
`````

### Imports in SCSS

To import bootstrap and font awesome in the `css/main.scss`: 

`````
---
# Only the main Sass file needs front matter (the dashes are enough)
---
@charset "utf-8";

// Variables to modify font folders
$icon-font-path:      "../fonts/bootstrap";
$fa-font-path:        "../fonts/font-awesome";

// Import partials from `sass_dir` (defaults to `_sass`)
@import "bootstrap-sass/bootstrap";
@import "font-awesome/font-awesome";

`````

### Minification

To ensure minification, add the following to the `_config.yml`:

`````
sass:
  style: compressed
`````



## Compass 

