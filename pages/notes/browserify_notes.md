---
title: Browserify
tags: [gulp, tooling, npm, javascript, sass]
keywords: gulp, tooling, npm, javascript, sass 
last_updated: March 5, 2017
summary: browserify is a tool for compiling node-flavored commonjs modules for the browser. You can use browserify to organize your code and use third-party libraries even if you don't use node itself in any other capacity except for bundling and installing packages with npm. The module system that browserify uses is the same as node, so packages published to npm that were originally intended for use in node but not browsers will work just fine in the browser too. 
sidebar: notes_sidebar
permalink: browserify_notes.html
folder: notes 
---

## References

- [substack/browserify-handbook](https://github.com/substack/browserify-handbook)
- [substack/node-browserify](https://github.com/substack/node-browserify) 
- [Using Browserify](https://gulp.readme.io/docs/browserify-uglify2-with-sourcemaps)


## Installing Browserify

## Integrating Browserify with Gulp

[Gulp + Browserify: The Everything Post](https://www.viget.com/articles/gulp-browserify-starter-faq)

Browserify is a stream-based processor designed to handle JavaScript modules. Browserify emits text-based streams that can be easily integrated with Gulp.  

Browserify bundles modules and resolves dependencies by adapting Node.js to enable browsers to use modules.

"Browserify adds the `require` and `module` additions to the global namespace and creates a bundle in which the required modules are added and made available in the browser."

"All JavaScript modules are allowed to use `require` and `module.exports` statements. Those are recognized by Browserify, which knows which modules to add to the bundle. It bundles everything, resolves dependency graphs, and adds the required functionality of require and module.exports to the browser."

- "`Browserify` adds easy-to-use module support for client-side scripting via a preprocessing step and enables you to load dependencies from `npm` and `bower` (via `debowerify`) directly into your bundles."


### Transforming Stream Contents

The `vinyl-source-stream` and `vinyl-buffer` plugins enable you to transform standard readable text streams into object-based virtual file streams that are compatible with Gulp and Gulp plugins.

- The `vinyl-source-stream` module creates a new virtual file object by wrapping the content of a text stream into a *vinyl file object* and providing it with a filename. 
- The `vinyl-buffer` transforms the `content` property. It enables you to read the streaming contents at once and make them accessible in a buffer. Some plugins cannot do line-by-line transformations. For example, `gulp-uglify` must change code throughout the file, which requires the plugin to operate on multiple parts of the document.

~~~javascript
var browserify  = require('browserify');
var source      = require('vinyl-source-stream');
var buffer      = require('vinyl-buffer');

/* Browserify API defines new information */
var bundle      = browserify({
  /* Takes entries you want to compile as parameters */ 
  entries: ['app/scripts/main.js'],
  /* Create a sourcemap that is emitted from the stream after bundling */
  debug: true
});

gulp.task('scripts', function() {
  /* Creates a new stream of compiled contents */
  return bundle.bundle()
    /* Pipe through the vinyl-source-stream module */
    .pipe(source('main.min.js'))
    /* Transform content property to buffer so that it can be used with uglify */
    .pipe(buffer())
    /* Transform the sourcemap into a virtual file system property */ 
    .pipe(sourcemaps.init({loadMaps: true}))
    .pipe(uglify())
    .pipe(gulp.dest('dist/scripts'));
});
~~~

> "With vinyl-source-stream wrappers, you can transform standard readable text streams into object-based virtual file streams. In doing so, you make them compatible with Gulp and some Gulp plugins. The stream you create is entirely new; its contents are from the original text stream of its original tool (in this example Browserify). But Gulp plugins have the ability to deal with either streamable contents or buffered con- tents or both. vinyl-buffer is a great way provided by the Vinyl file system to deal with such plugins."

### Another Example 
> Browserify has become an important and indispensable tool but requires being wrapped before working well with gulp. Below is a simple recipe for using Browserify with transforms and full sourcemaps that resolve to the original individual files.

~~~javascript
'use strict';

var gulp = require('gulp');
var uglify = require('gulp-uglify');
var transform = require('vinyl-transform');
var browserify = require('browserify');
var sourcemaps = require('gulp-sourcemaps');

gulp.task('javascript', function () {
  // transform regular node stream to gulp (buffered vinyl) stream 
  var browserified = transform(function(filename) {
    var b = browserify({entries: filename, debug: true});
    return b.bundle();
  });
  
  return gulp.src('./app.js')
    .pipe(browserified)
    .pipe(sourcemaps.init({loadMaps: true}))
        // Add transformation tasks to the pipeline here.
        .pipe(uglify())
    .pipe(sourcemaps.write('./'))
    .pipe(gulp.dest('./dist/js/'));
});
~~~

## Debowerify & Deamdify

Debowerify enables you to use Browserify to load `bower` dependencies directly into your bundles. 

- [eugeneware/debowerify](https://github.com/eugeneware/debowerify) A browserify transform to enable the easy use of bower components in browserify client javascript projects. This can be used in conjunction with deamdify to require AMD components from bower as well.
- [jaredhanson/deamdify](https://github.com/jaredhanson/deamdify) This module is a browserify plugin that will transform AMD modules into Node.js-style modules so that they can be included in browser-ified bundles. With this transform in place, Node and AMD modules can be freely intermixed, and the resulting bundle can be used without the need for a separate loader such as RequireJS.

## Glossary

- Buffers
- Streams
- "Vinyl file objects are lightweight wrappers around file contents, which allow quick access to the content and in-memory storage. Additionally, vinyl file objects offer easy access to paths and filenames."
- virtual file objects
