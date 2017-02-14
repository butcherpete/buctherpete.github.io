---
title: Gulp Notes 
tags: [gulp, tooling, npm, javascript, sass]
keywords: gulp, tooling, npm, javascript, sass 
last_updated: February 6, 2017
summary: Gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something. 
sidebar: notes_sidebar
permalink: gulp_notes.html
folder: notes 
---

## Resources 

[Gulp documentation](https://github.com/gulpjs/gulp/tree/master/docs)

## Components 

A Gulp installation consists of four components:

- Gulp CLI: checks globally for local Gulp is available in project and boots local Gulp. A CLI to start the build tool.
- local Gulp, a Gulp installation that 1) provides the basic Gulp API and 2) loads and runs the defined tasks.
- Gulpfile, a JS file that specifies the build instructions; identifies the tasks to run.
- Gulp plugins, wrappers for tasks, 'that know how to combine, modify, and assemble parts of your software.

## Installing Gulp

To install gulp globally (the Gulp CLI):

`````
$ node --version
$ npm --version
$ npm install -g gulp-cli
$ gulp --version
`````

To install gulp locally in the project directory:

`````
## Creates the package.json file.
$ npm init      

## Saves the Gulp version to the package.json.
$ npm install --save-dev gulp

## Ensures that Gulp 4 is installed.
$ npm install --save-dev gulpjs/gulp.git#4.0  
$ gulp --version
`````

To install gulp plugins locally in the project directory:

`````
$ npm install --save-dev <gulp-plugin>
`````

## Gulpfiles

The `gulpfile.js` specifies all of the tasks to be executed. This gulpfile is saved to the project's root directory.

`````
var gulp = require('gulp');  ## Requires local Gulp installation
gulp.task('<name>', function() { ... }); 
`````

"gulp.src and gulp.dest create readable and writeable streams, allowing you to copy files from one place in the file system to another."

- `gulp.dest`
- `gulp.parallel`: "This function takes the same parameters as gulp.series but executes those tasks in parallel. To do so, it spawns a series of processes that are executed at the same time."
- `gulp.series`: "This function call allows you to run a sequential order of Gulp tasks. It takes an infinite amount of parameters of either string (pointing to a defined Gulp task) or functions."
- `gulp.src`
- `gulp.task`
- `gulp.watch`

## Recipes

Watch processes


### Chaining Tasks

> Gulp4 is required for chaining tasks.

The `gulp.series` "function call allows you to run a sequential order of Gulp tasks. It takes an infinite amount of parameters of either string (pointing to a defined Gulp task) or functions."

```
gulp.task('scripts', 
  gulp.series('tests', function() {
    return gulp.src(['app/scripts/vendor/**/*.js', 'app/scripts/**/*.js'])
      .pipe(concat('main.min.js'))
      .pipe(gulp.dest('dist'));
    })
);
```

### Parallel Tasks

> Gulp4 is required for parallel tasks.

The `gulp.parallel` function "takes the same parameters as gulp.series but executes those tasks in parallel. To do so, it spawns a series of processes that are executed at the same time."

```
gulp.task('default',
  gulp.series('clean',
    gulp.parallel('styles', 'scripts')
  )
);
```

### Single Destination & Watch

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var coffee = require('gulp-coffee');
var uglify = require('gulp-uglify');

gulp.task('js', function(){
    return gulp.src('./js/src/*.coffee')
        .pipe(coffee())
        .pipe(uglify())
        .pipe(gulp.dest('./js/'));
});

gulp.task('watch', function(){
    gulp.watch('./js/src/*.coffee', ['js']);
});
`````

### Multiple Destinations

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require 'gulp';
var autoprefixer = require 'gulp-autoprefixer';
var minifyCss = require 'gulp-minify-css';
var rename = require 'gulp-rename';

gulp.task 'css', ->
    gulp.src './css/src/style.css'
    .pipe autoprefixer 'last 2 versions'
    .pipe gulp.dest ‘./css/‘
    .pipe minifyCss()
    .pipe rename extname: '.min.css'
    .pipe gulp.dest ‘./css/‘
`````

### Incremental Builds

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var cached = require('gulp-cached');
var uglify = require('gulp-uglify');
var remember = require('gulp-remember');
var concat = require('gulp-concat');

gulp.task('script', function(){
    return gulp.src('./js/src/*.js')
        .pipe(cached())
        .pipe(uglify())
        .pipe(remember())
        .pipe(concat('app.js'))
        .pipe(gulp.dest('./js/'));
});
`````

### Only Changes 

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var changed = require('gulp-changed');
var uglify = require('gulp-uglify');

gulp.task('js', function(){
    return gulp.src('./src/*.js')
        .pipe(changed('./dist/'))
        .pipe(uglify())
        .pipe(gulp.dest('./dist/'));
});
`````

### Async Streams 

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var merge = require('merge-stream');
var less = require('gulp-less');
var autoprefixer = require('gulp-autoprefixer');

gulp.task('css', function(){
    return merge(
        gulp.src('./css/src/first.less')
            .pipe(less())
            .pipe(gulp.dest('./css/')),
        gulp.src('./css/src/second.css')
            .pipe(autoprefixer())
            .pipe(gulp.dest('./css/'))
    );
});
`````

### Serial Join 

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var streamqueue = require('streamqueue');
var less = require('gulp-less');
var cssimport = require('gulp-cssimport');
var autoprefixer = require('gulp-autoprefixer');
var concat = require('gulp-concat');
var minifyCss = require('gulp-minify-css');

gulp.task('css', function(){
    return streamqueue({ objectMode: true },
        gulp.src('./css/src/first.less')
            .pipe(less()),
        gulp.src('./css/src/second.css')
            .pipe(cssimport())
            .pipe(autoprefixer('last 2 versions')))
        .pipe(concat('app.css'))
        .pipe(minifyCss())
        .pipe(gulp.dest('./css/'));
});
`````

### Serial Array 

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

`````
var gulp = require('gulp');
var es = require('event-stream');
var consolidate = require('gulp-consolidate');
var rename = require('gulp-rename');

data = [
    {
        name: 'apple',
        title: 'Apple Cake',
        attrs: some_data
    },
    {
        name: 'orange',
        title: 'Orange Cookie',
        attrs: some_data
    }
];

gulp.task('page', function(){
    var tasks = data.map(function(entry){
        return gulp.src('./templates/a.js')
            .pipe(consolidate({
                title: entry.title,
                attrs: entry.attrs
            }))
            .pipe(rename({
                basename: entry.name,
                extname: '.html'
            }))
            .pipe(gulp.dest('./html/'));
    });
    return es.concat.apply(null, tasks);
});
`````

### Task Dependency

`````
gulp.task('css',['font', 'less'], function(){
  // do something after font and less
});
`````

### Converting SASS to CSS

`````
var sass = require('gulp-sass');
var browserSync = require('browser-sync').create();

gulp.task('sass', function(){
  return gulp.src('app/scss/**/*.scss') //All .scss files in app/css and child dirs
    .pipe(sass()) // Converts Sass to CSS with gulp-sass 
    .pipe(gulp.dest('app/css'))
		.pipe(browserSync.reload({
		stream: true
	}));
});
`````

### Watching HTML or JS Changes 

`````
var sass = require('gulp-sass');
var browserSync = require('browser-sync').create();

gulp.task('browserSync', function() {
	browserSync.init({
		server: {
			baseDir: 'app'
		},
	});
});

gulp.task('watch', ['browserSync', 'sass'], function(){
	gulp.watch('app/scss/**/*.scss', ['sass']);
  //Reloads the browser whenever HTML or JS changes
  gulp.watch('app/*.html', browserSync.reload);
  gulp.watch('app/js/**/*.js', browserSync.reload);
	});
`````

### Useref Task 

`````
var useref = require('gulp-useref');
var uglify = require('gulp-uglify');
var gulpIf = require('gulp-if');
var cssnano = require('gulp-cssnano');

gulp.task('useref', function(){
  return gulp.src('**/*.html')
    .pipe(useref())
    .pipe(gulpIf('*.js', uglify()))
    .pipe(gulpIf('*.css', cssnano()))
    .pipe(gulp.dest('dist'));
});
`````

### Clean Task

The `del` package is a Node.js module that enables you to remove the products (files and folders) of a previous build. The module supports multiple files and globbing.

```
var del = require('del');

gulp.task('clean', function() {
  return del(['dist']);
});
```
The glob pattern ** matches all children *and the parent*.

### Reporting Task

Gulp tasks do not need to return streams. If you are using Node packages (such as `del`) instead of Gulp streams, you can close tasks  by passing a `done` callback back to the function.

`````
gulp.task('report', gulp.series(function (done) {
  console.log('We are done');
  done();
}));
`````

The `done` callback function notifies Gulp when the report task has finished. instead of returning streams, and everything inside your task relies purely on other Node functionality."

## Plugins

### Development
 
Plugin       | Description
----------   | -----------
[gulp-useref](https://www.npmjs.com/package/gulp-useref)| Parse build blocks in HTML files to replace references to non-optimized scripts or stylesheets.
[gulp-sourcemaps](https://www.npmjs.com/package/gulp-sourcemaps)  |  Facilitate debugging.
[sprity](https://www.npmjs.com/package/sprity)      |  Create sprites.
[gulp-changed](https://www.npmjs.com/package/gulp-changed)|   Compiling changes files only.
[require-directory](https://www.npmjs.com/package/require-directory)  |  Recursively iterates over specified directory, `require()`ing each file, and returning a nested hash structure containing those modules.
[del](https://www.npmjs.com/package/del) | Delete files and folders.

### JavaScript 

Plugin       | Description
----------   | -----------
[gulp-babel](https://www.npmjs.com/package/gulp-babel)  |   Writing E6.
[gulp-jshint](https://www.npmjs.com/package/gulp-jshint)  |   JSHint plugin for gulp, a tool that helps to detect errors and potential problems in your JavaScript code.


### CSS

Plugin       | Description
----------   | -----------
[gulp-sass](https://www.npmjs.com/package/gulp-sass) | `gulp-sass` is a light-weight wrapper of `node-sass`, a Node binding for `libsass`, which is a port of Sass. 
[gulp-cssnano](https://www.npmjs.com/package/gulp-cssnano)| Minify CSS with cssnano. Cssnano takes your nicely formatted CSS and runs it through many focused optimisations, to ensure that the final result is as small as possible for a production environment.
[gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer) | Write vendor-free CSS.
[gulp-uncss](https://www.npmjs.com/package/gulp-uncss) |   Remove unused CSS.
[gulp-csso](https://www.npmjs.com/package/gulp-csso)        |   Optimize CSS.
[critical](https://www.npmjs.com/package/critical)    |   Generate inline CSS performance.

## Readings

### NodeJS Streams

[substack/stream-handbook](https://github.com/substack/stream-handbook)

## Glob Patterns

Gulp workflows require four globbing patterns:

Pattern | Description
------- | -----------
`*.scss`  | The `*`  wildcard  returns matching patterns in the current directory. 
`**/*.scss`  | The `**/*` returns matching patterns in the root and all child directories.
`!not-me.scss` | The `!` bang excludes matching patterns. 
`*.+(scss|sass)` | The `+`, `()`, and `|` characters enable matches of multiple patterns.

## Troubleshooting

### JShint

Fix for jshint dependency problem: `npm install --save-dev jshint@2.8.0` 

## Glossary

- Browsersync
- build tool
- `del` Node.js package
- dependency chain. A dependency is a relationship between two tasks that specifies their order. "Dependencies can also have other dependencies. The path from the outmost dependency to the very root task is called a dependency chain."
- dependency manager
- destinations (outbound streams)
- execution chain. An execution chain specifies a set of loosely-coupled tasks that are called in order, either sequentially or in parallel.
- generator
- globstar
- input streams (readable streams)
- minification library
- scaffolding tool
- stream
- virtual file
- watch process
