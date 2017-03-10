---
title: Browsersync 
tags: [gulp, tooling, npm, javascript, sass]
keywords: gulp, tooling, npm, javascript, sass 
last_updated: February 18, 2017
summary: BrowserSync makes your tweaking and testing faster by synchronising file changes and interactions across multiple devices.
sidebar: notes_sidebar
permalink: js_browsersync.html
folder: notes 
---

## Resources

- [browser-sync](https://www.npmjs.com/package/browser-sync)
- [Browsersync Docs](https://browsersync.io/docs)
- [Browsersync + Gulp.js](https://browsersync.io/docs/gulp)

## Installing

Install Gulp and Browsersync as development dependencies:

~~~javascript
$ npm install browser-sync gulp --save-dev
~~~

Use `gulp` and `browser-sync` in the `gulpfile.js`.

## Gulp Watch Processes

"You also booted up a local development server with Browsersync, which allows you to see those iterative changes. File watchers again notify your server to inject changes into the visual representation in your browser."

Watch processes listen to file changes and trigger one or more tasks. A socket connection between the client and server enables you to inject resources (styles and scripts).

The server task can be used as a standalone component that can be integrated into the build execution chain.

~~~javascript
/* Require Browsersync */
var bSync   = require('browser-sync');
...

/* Create new task with a done callback */
gulp.task('server', function(done) {
  /* Start server with function call */
  bSync({
    server: {
      /* config object defines the base directories of your server */
      baseDir: ['dist', 'app']
    }
  });
  /* Once the server is opened, call the callback */
  done();
});
~~~

> Browsersync starts a new process, and without the callback, Gulp would be stuck there, unable to call the functions afterward. The done callback function makes sure you return to the next step in your previous execution chain, which you adapt in the next listing.

~~~javascript
gulp.task('default',
  gulp.series('clean',
    gulp.parallel('styles', 'scripts'), 
    /* Call the server task */
    'server',
    /* Add watcher function */
    function watcher(done) {
      /* Call watcher with gulp.watch function */
      gulp.watch(
      /* Pass array of globs pointing to JS files as first parameter */
        ['app/scripts/**/*.js', '!app/scripts/vendor/**/*.js'],
        gulp.parallel('scripts')
      );
      /* Pass a glob pointing to LESS files */
      gulp.watch(
        'app/styles/**/*.less', 
        gulp.parallel('styles')
      );
      /* Pass a glob pointing to created files in dist folder */
      gulp.watch(
        'dist/**/*',
        /* Add reload function as second parameter */
        bSync.reload
      );
      /* Finish the watcher function */ 
      done();
    }
  ) 
);
~~~

## Browsersync: Gulp & SASS

[BrowserSync/recipes](https://github.com/Browsersync/recipes/tree/master/recipes/gulp.sass)

~~~javascript
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var sass        = require('gulp-sass');
var reload      = browserSync.reload;

var src = {
    scss: 'app/scss/*.scss',
    css:  'app/css',
    html: 'app/*.html'
};

// Static Server + watching scss/html files
gulp.task('serve', ['sass'], function() {

    browserSync.init({
        server: "./app"
    });

    gulp.watch(src.scss, ['sass']);
    gulp.watch(src.html).on('change', reload);
});

// Compile sass into CSS
gulp.task('sass', function() {
    return gulp.src(src.scss)
        .pipe(sass())
        .pipe(gulp.dest(src.css))
        .pipe(reload({stream: true}));
});

gulp.task('default', ['serve']);
~~~

## SASS & CSS Injecting

[Browsersync + Gulp.js](https://browsersync.io/docs/gulp)

> "Streams are supported in Browsersync, so you can call reload at specific points during your tasks and all browsers will be informed of the changes. Because Browsersync only cares about your CSS when it's finished compiling - make sure you call `.stream()` after `gulp.dest`"

~~~ javascript
var gulp        = require('gulp');
var browserSync = require('browser-sync').create();
var sass        = require('gulp-sass');

/* Static Server + watching scss/html files */
gulp.task('serve', ['sass'], function() {

    browserSync.init({
        server: "./app"
    });

    gulp.watch("app/scss/*.scss", ['sass']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
});

/* Compile sass into CSS & auto-inject into browsers */
gulp.task('sass', function() {
    return gulp.src("app/scss/*.scss")
        .pipe(sass())
        .pipe(gulp.dest("app/css"))
        .pipe(browserSync.stream());
});

gulp.task('default', ['serve']);
~~~

## Ruby SASS & Source Maps

> If you use gulp-ruby-sass with the sourcemap: true option, additional .map files will be generated. These files end up being sent down stream and when browserSync.reload() receives them, it will attempt a full page reload (as it will not find any .map files in the DOM).

> To fix this problem, use browserSync.stream({match: '**/*.css'}) as seen in the following example.

[Browsersync + Gulp.js](https://browsersync.io/docs/gulp)


~~~ javascript
var gulp        = require("gulp");
var sass        = require("gulp-ruby-sass");
var browserSync = require("browser-sync").create();

// Static Server + watching scss/html files
gulp.task('serve', ['sass'], function() {

    browserSync.init({
        server: "./app"
    });

    gulp.watch("app/scss/*.scss", ['sass']);
    gulp.watch("app/*.html").on('change', browserSync.reload);
});

/**
 * Compile with gulp-ruby-sass + source maps
 */
gulp.task('sass', function () {

    return sass('app/scss', {sourcemap: true})
        .on('error', function (err) {
            console.error('Error!', err.message);
        })
        .pipe(sourcemaps.write('./', {
            includeContent: false,
            sourceRoot: '/app/scss'
        }))
        .pipe(browserSync.stream({match: '**/*.css'}));
});
~~~
