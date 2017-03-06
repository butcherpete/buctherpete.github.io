---
title: Image Processing 
tags: [javascript]
keywords:  
last_updated: March 1, 2017
summary: A list of image processing commands.
sidebar: notes_sidebar
permalink: image_notes.html
folder: notes 
---

[Efficient Image Resizing](https://www.smashingmagazine.com/2015/06/efficient-image-resizing-with-imagemagick/)

[nwtn/image-resize-tests](https://github.com/nwtn/image-resize-tests/tree/optimization)

~~~
var im = require('imagemagick');

var inputPath = 'path/to/input';
var outputPath = 'path/to/output';
var width = 300; // output width in pixels

var args = [
   inputPath,
   '-filter',
   'Triangle',
   '-define',
   'filter:support=2',
   '-thumbnail',
   width,
   '-unsharp 0.25x0.25+8+0.065',
   '-dither None',
   '-posterize 136',
   '-quality 82',
   '-define jpeg:fancy-upsampling=off',
   '-define png:compression-filter=5',
   '-define png:compression-level=9',
   '-define png:compression-strategy=1',
   '-define png:exclude-chunk=all',
   '-interlace none',
   '-colorspace sRGB',
   '-strip',
   outputPath
];

im.convert(args, function(err, stdout, stderr) {
   // do stuff
});
~~~

## Grunt Resampling

[nwtn/grunt-respimg](https://github.com/nwtn/grunt-respimg)

## Gulp Image Manipulation
[gulp-gm](https://www.npmjs.com/package/gulp-gm)

## Gulp Image Resizing

[scalableminds/gulp-image-resize](https://github.com/scalableminds/gulp-image-resize)
