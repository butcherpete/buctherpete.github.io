---
title: Browsersync 
tags: [gulp, tooling, npm, javascript, sass]
keywords: gulp, tooling, npm, javascript, sass 
last_updated: February 18, 2017
summary: 
sidebar: notes_sidebar
permalink: gulp_browsersync.html
folder: notes 
---

[Browsersync Docs](https://browsersync.io/docs)

## Gulp Integration

## Browsersync & SASS

[Browsersync + Gulp.js](https://browsersync.io/docs/gulp)

"Streams are supported in Browsersync, so you can call reload at specific points during your tasks and all browsers will be informed of the changes. Because Browsersync only cares about your CSS when it's finished compiling - make sure you call `.stream()` after `gulp.dest`"

~~~ javascript
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var sass        = require('gulp-sass');

// Static Server + watching scss/html files
gulp.task('serve', ['sass'], function() {

    browserSync.init({
        server: "./app"
    });

    gulp.watch("app/scss/*.scss", ['sass']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
});

// Compile sass into CSS & auto-inject into browsers
gulp.task('sass', function() {
    return gulp.src("app/scss/*.scss")
        .pipe(sass())
        .pipe(gulp.dest("app/css"))
        .pipe(browserSync.stream());
});

gulp.task('default', ['serve']);
~~~
