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

### Installing Gulp Globally 

To install gulp globally (the Gulp CLI):

`````
$ node --version
$ npm --version
$ npm install -g gulp-cli
$ gulp --version
`````

### Installing Gulp Locally 

To install gulp locally in the project directory:

~~~
// Creates the package.json file.
$ npm init      

// Saves the Gulp version to the package.json.
$ npm install --save-dev gulp

// Ensures that Gulp 4 is installed.
$ npm install --save-dev gulpjs/gulp.git#4.0  
$ gulp --version
~~~

### Installing Gulp Plugins

To install gulp plugins locally in the project directory:

`````
$ npm install --save-dev <gulp-plugin>
`````

## Gulpfiles

The `gulpfile.js` specifies all of the tasks to be executed. This gulpfile is saved to the project's root directory.

`````
// Requires local Gulp installation
var gulp = require('gulp');  
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

A *build cache* is an in-memory store of files. The `gulp-cached` plugin  checks if files are already in the cache. If the file is already in the cache, the plugin checks to see if the file is newer than the cached version. If it is older, it is discarded. Otherwise, the newer version is passed through to the stream and updated to the cache.

~~~ javascript
var cached    = require('gulp-cached');
var remember  = require('gulp-remember');
...

gulp.task('scripts',
  gulp.series('test', function scriptsInternal() {
    var glob = mainBowerFiles('**/*.js');
    glob.push = ('app/scripts/**/*.js');

    // since flag ensures only new files are read
    return gulp.src(glob, { since: gulp.lastRun('scripts') })

      // Pipe through cache to update cache
      .pipe(cached('ugly'))
      .pipe(uglify())

      // Remember files from previous iteration
      .pipe(remember('ugly'))

      // All files are available again
      .pipe(concat('main.min.js'))
      .pipe(gulp.dest('dist/scripts'));
~~~

The build cache recalls processed files when needed. The `gulp-remember` plugin adds incremental builds from a previous iteration back into the stream.

> "With every cached call, you update your memory, and with every remember call, you put the files back into a stream that will end up on the real file system."

[osscafe/gulp-cheatsheet](https://github.com/osscafe/gulp-cheatsheet/blob/master/README.md)

~~~ javascript
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
~~~

### File Deletions

The `gulp-remember` plugin adds all files in the in-memory cache to  the stream regardless of whether they still exist on the file system.

Add an event handler to `gulp-watch` to ensure that deleted file are removed from the in-memory cache:

~~~ javascript
// The slash plugin manages system-neutral file paths
var slash = require('slash'); 
var path  = require('path');

// gulp.watch returns a watcher object
var watcher =   gulp.watch(['app/scripts/**/*.js'], gulp.parallel('scripts'));

// unlink event is fired when a file is deleted from the file system. 
watcher.on('unlink', function (filepath) {
  // remove deleted file from gulp-remember cache
  delete cached.caches['ugly'][slash(path.join(__dirname,filepath))]; 
  remember.forget('ugly', slash(path.join(__dirname,filepath)));
~~~

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

~~~
gulp.task('css',['font', 'less'], function(){
  // do something after font and less
});
~~~

### Converting SASS to CSS

~~~
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
~~~

### Watching HTML or JS Changes 

~~~
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
~~~

### Useref Task 

~~~
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
~~~

### Clean Task

The `del` package is a Node.js module that enables you to remove the products (files and folders) of a previous build. The module supports multiple files and globbing.

~~~
var del = require('del');

gulp.task('clean', function() {
  return del(['dist']);
});
~~~

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

## Sourcemaps

Sourcemaps enable browsers to locate the source of loaded files. A sourcemap maintains a record of the position of a snippet in the original file by storing the name of the original file and the beginning and end of the snippet. 

Two methods of identifying a sourcemap:

- Add a reference URL in an output file comment
- Include the encoded sourcemap, a relatively large file. You do not want to do this in production code.

> "The browser-wide standard for sourcemaps brings back the original source in a browser’s developer tools, while still executing the compiled and optimized bundle. This helps you identify the error with ease, running the same code as you would in production."

> browser vendors Google and Mozilla combined their efforts to create sourcemaps, which are a way of tracking the output back to its original source files. 

> Built-in sourcemaps create a new property for your virtual file objects called `sourcemap`. These properties will be filled with information about the transformations you make: which line and which character have been changed, what the original was, and what the new output is. Those sourcemaps can be interpreted by browsers, reimagining the original file, even though they don’t have to be physically available anymore. Gulp sourcemaps are combinable, which means that every new task will modify the sourcemap with new data, so that the end sourcemap still has the references to the original files.

~~~ javascript
var sourcemaps = require('gulp-sourcemaps');
...

# Activate sourcemaps by calling plugin
.pipe(sourcemaps.init())
...

# Call the sourcemap plugin after a transformation 
.pipe(sourcemaps.write('.', {
  sourceRoot: 'js-source'
}))
...
~~~ 

## Environment-specific Switches

> "Switches deal with the optional addition of sourcemaps and incremental builds depending on which environment (production or development environment) you’re building for."


Environment  | Features
----------   | -----------
Development  | Sourcemaps Development server Watchers
Production   | 

> Principle: Never Duplicate a Pipeline


## Streams

[Understanding Streams](https://gulp.readme.io/docs/understanding-streams)

### Passthrough Streams

[Gulp 4: Passthrough source streams](https://fettblog.eu/gulp-4-passthrough/)

Use passthrough streams to carry over the intermediate results from the earlier steps to merge streams. 

Passthrough streams enable you to add sources to pipelines midstream. So, you can *compile* and *transpile* code (for example, CoffeeScript files) and add the results (JavaScript files) to a common stream for processing.

~~~javascript
gulp.task('scripts', function() {

  // Select CoffeeScripts & pipe through coffee plugin
  return gulp.src('src/scripts/**/*.coffee')
    .pipe(coffee())
    // Create a passthrough that can pipe results to gulp.src call 
    .pipe(gulp.src('src/scripts/**/*.js', {passthrough: true}))
    .pipe(concat('main.js'))
    .pipe(uglify())
    .pipe(gulp.dest('dist/scripts'));
   });
~~~

Passthrough source streams enable `gulp.src` to be both readable and writable. In Gulp3, `gulp.src` had to appear at beginning of a stream. Now, you can use these plugins anywhere in your pipeline. 

To lint JavaScript files and concatenate them into a single, vendor-specific file.

~~~javascript
gulp.task('default', function() {
  // Glob the JS files
  return gulp.src('src/**/*.js') 
    // Pass to linter
    .pipe(jshint()) 
    .pipe(jshint.reporter('default'))
    .pipe(jshint.reporter('fail'))
    // Glob the venor (JQuery, lodash, etc.) JS & our linted JS
    .pipe(gulp.src('vendor/**/*.js', {passthrough: true})) 
    .pipe(uglify())
    .pipe(concat('main.min.js'))
    .pipe(gulp.dest('dest'));
});
~~~

"With Gulp, you usually deal with readable streams at the beginning when selecting files and use writeable streams when you pipe them through each task and store the contents at the end. Passthrough streams allow for both being written to and being read from. It turns out that gulp.src is capable of creating both readable and writeable streams. At any time in your build pipeline, you can add (or pass through) new files to the stream that skip the early process and are piped through the tasks that follow." 

> To do: Experiment with passthrough streams, Markdown, Asciidoc, and HMTL5.

### Merge Streams

Merge streams enable you to independently process two streams in parallel and merge and process the results of those streams in a third stream. 

~~~javascript
var coffeelint  = require('gulp-coffeelint');
var coffee      = require('gulp-coffee');
var merge       = require('merge2');
...

gulp.task('scripts', function() {

  // Glob and process CoffeeScript into JS
  var coffeeStream = gulp.src('src/scripts/**/*.coffee')
    .pipe(coffeelint())
    .pipe(coffeelint.reporter())
    .pipe(coffeelint.reporter('fail'))
    .pipe(coffee());

  // Glob and process JavaScript 
  var jsStream = gulp.src('src/scripts/**/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('default'))
    .pipe(jshint.reporter('fail'));

  // Merge both streams 
  return merge(coffeeStream, jsStream)
    // Pipe through minify and concat
    .pipe(concat('main.js'))
    .pipe(uglify())
    .pipe(gulp.dest('dist/scripts'));
});
~~~

`gulp-concat` concatenates all processed scripts into a singel output.

### Parameterized Streams 

Parametrized streams enable you to use placeholders instead of tasks and pass those parameters to a function. The function can be called by any task. For example, two tasks that use different transpilers.

The compilation process is defined once.

~~~javascript
/** new plugins **/
var eslint = require('gulp-eslint');
var babel  = require('gulp-babel');

function compileScripts(param) {
  // compileScript: a stream defined in previous task
  var transpileStream = gulp.src(param.directory + '**/*.' + param.type)
    .pipe(param.linttask())
    .pipe(param.fail)
    .pipe(param.compiletask());

  var jsStream = gulp.src(param.directory + '**/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('fail'));

  return merge(transpileStream, jsStream)
    .pipe(concat(param.bundle))
    .pipe(uglify())
    .pipe(gulp.dest('dist'));
}

gulp.task('core', function() {
  // Build stream dynamically for CoffeeScript files
  return compileScripts({
    linttask: coffeelint,
    fail: coffeelint.reporter('fail'),
    compiletask: coffee,
    directory: 'core/',
    type: 'coffee',
    bundle: 'core.js'
  });

 gulp.task('ui', function() {
  // Build again for ES2015/ES2016 using Babel transpiler
  return compileScripts({
    linttask: eslint,
    fail: eslint.failAfterError(),
    compiletask: babel,
    directory: 'ui/',
    type: 'es',
    bundle: 'ui.js'
  }); 
});
~~~

> The parts where you compile your files to be transpiled have been replaced with params that you pass to that function B. The major benefit of this setup is to have the process specified and defined in one place and replace just the flexible elements through configuration objects.

### Stream Arrays

> Let’s expand on the idea of having a set of similar configured stream properties and trying to reuse the same stream over and over again. Although the setup in section 7.2.1 works well, it has one drawback: it requires you to instantiate the stream for each of your configuration objects manually. Also, in the setup just shown you place each stream in a separate task.

> Stream arrays and parameterized streams take this idea even further. Instead of just creating one bundle, you can create multiple bundles with variations by using just one stream definition. This stream can be initialized as many times as you like and executed in one task.

A stream array is an array of streams that are executed simutaneously. They make use of standard array functions such as Array object's `map` function. 

~~~javascript
// Define the variations array
var variations = [{
  linttask: coffeelint,
  fail: coffeelint.reporter('fail'),
  compiletask: coffee,
  directory: 'core/',
  type: 'coffee',
  bundle: 'core.js'
},{
  linttask: coffeelint,
  fail: coffeelint.reporter('fail'),
  compiletask: coffee,
  directory: 'vendor/',
  type: 'coffee',
  bundle: 'vendor.js'
},{
  linttask: eslint,
  fail: eslint.failAfterError(),
  compiletask: babel,
  directory: 'ui/',
  type: 'es',
  bundle: 'ui.js'
}];

// Create a stream for each configuration object
gulp.task('scripts', function() {
  var streams = variations.map(function(el) {
     // Function defined in Parameterized Streams example
     return compileScripts(el);
});
  // Merge streams for execution in gulp
  return merge(streams);
});
~~~

From an array of configurations, you get an array of streams. Use `merge` to combine them into a single stream for execution.


### Stream snippets 

> Stream snippets allow you to bundle common tasks into a function that can be added like any other Gulp task to your streaming pipeline. This ensures that you avoid repeating yourself when you see that certain tasks have to be used together multiple times.

> To create such a snippet, you can use one of the packages from the Node.js stream ecosystem: `stream-combiner2`.

~~~javascript
var combiner = require('stream-combiner2');

// Add tasks to the stream combinator
function combine(output) {
  return combiner.obj(
    uglify(),
    concat(output)
  );
}

gulp.task('vendor', function() {
  return gulp.src('vendor/**/*.js')
    // Use the snippet like any other task
    .pipe(combine('vendor.js'))
    .pipe(gulp.dest('dist'));
});

gulp.task('scripts', function() {
  return gulp.src('src/**/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('fail'))
    .pipe(combine('bundle.js'))
    .pipe(gulp.dest('dist'));
});
~~~

### Stream queues 

> Stream queues are useful for keeping the order of output files intact. This is helpful if your code requires you to hold onto a certain sequence and execu- tion of some stream parts take longer than others.

~~~javascript

~~~

### Gulp filters 

> After adding new files into a stream, you learned how to remove files again if they’re not needed in subsequent tasks. For that, you use gulp filters.

~~~javascript

~~~

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
