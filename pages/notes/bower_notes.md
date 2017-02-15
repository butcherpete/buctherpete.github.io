---
title: Bower Notes 
tags: [bower, tooling]
keywords:  
last_updated: February 6, 2017
summary: Web sites are made of lots of things — frameworks, libraries, assets, and utilities. Bower manages all these things for you. 
sidebar: notes_sidebar
permalink: bower_notes.html
folder: notes 
---

## Resources 

[Bower Documentation](https://bower.io/)

## Installing Bower

To install make the Bower command-line tool available globally:

```
$ npm install -g bower
```

### Bower.json

To interactively create a `bower.json` file:

```
$ bower init 
```
The command initializes the project as a component and stores project dependencies. 

[bower.json specification](https://github.com/bower/spec/blob/master/json.md)

Component dependency information is saved in a `bower.json` metadata file. The `bower.json` identifies packages that can be used as dependencies of other packages. 

### Maintaining Dependencies

To add a `<package>` to the project's `bower.json` dependency array:

```
$ bower install jquery --save
```

To add a `<package>` to the project's `bower.json` devDependencies:

```
$ bower install jquery --save-dev
```

## Bower and Gulp

"Installing a Bower package with `--save` adds the package as a dependency in the project's `bower.json` file. The `wiredep` library reads that file, then reads the `bower.json` files for each of those dependencies. Based on these connections, `wiredep` determines the order your scripts must be included before injecting them between placeholders in your source code."


### Installing wiredep Module

To wire Bower dependencies to source code, install the wiredep module using npm.

```
$ npm install --save wiredep
```

### Installing Dependencies

Install dependencies using Bower.

```
$ bower install --save <dependency>
```

### Inserting Placeholders in Markup

Insert placeholders in the markup where the dependencies will be injected.

``` 
<html>
<head>
<!-- bower:css -->
<!-- endbower -->
</head>
<body>
<!-- bower:js -->
<!-- endbower -->
</body>
</html>
```

### Importing Libraries 

The `wiredep` library works with Gulp streams: 

```
var wiredep = require('wiredep').stream;
 
gulp.task('bower', function () {
  gulp.src('./src/footer.html')
    .pipe(wiredep({
      optional: 'configuration',
      goes: 'here'
    }))
    .pipe(gulp.dest('./dest'));
});
```

## Glossary

- component
- component repository
- component registry
- dependency
- dependency tree
- component repository
- flat dependency tree
- nested dependency tree

