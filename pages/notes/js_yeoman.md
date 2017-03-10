---
title: Yeoman 
tags: [yeoman, tooling]
keywords: yeoman, tooling 
last_updated: February 6, 2017
summary: Yeoman helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. To do so, we provide a generator ecosystem. A generator is basically a plugin that can be run with the `yo` command to scaffold complete projects or useful parts. 
sidebar: notes_sidebar
permalink: js_yeoman.html
folder: notes 
---

[Yeoman](http://yeoman.io/)

"The Yeoman workflow comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Gulp, Grunt etc) and the package manager (like npm and Bower)."

"Yeoman creates the necessary folders, copies initial files (like build scripts), applies boilerplate code, and triggers the installation of dependencies."

## Installation

To install the `yo` command-line tool:

~~~~
$ npm install -g yo
~~~~


To install both Yeoman and the generator plugin:

~~~~
npm install -g yo generator-generator
~~~~

## Generators

By convention, the name of the generator always begins with the _generator-_ prefix.

A generator consists of two parts:

- Assembly instructions file
- Project template

The project template consists of fixed, flexible, optional, and restorable parts.

The `generator-generator` is a predefined Yeoman generator that facilitates the creation of new generators. 

### Creating Local Generators

~~~
$ yo doctor
~~~

## Tutorial Procedure

1. Create a folder named `generator-<project name>` to contain the project templates. The folder must include the name of your generator. Yeoman relies on the file system to find generators.
2. Add six template files to the project folder. You do not need subfolders.
   * `main.js` (empty)
   * `package.json`
   * `gulpfile.js`
   * `main.less` (empty)
   * `bower.json`
   * `index.html`

3. Create a [package.json](https://docs.npmjs.com/files/package.json#files), a Node.js module manifest. The name property must be prefixed by "generator-" and the repo must have a description in order to be indexed by Yeoman.

   ```json
   {
     "name": "generator-name",
     "version": "0.1.0",
     "description": "",
     "files": [
       "generators",
      ],
     "keywords": ["yeoman-generator"],
     "dependencies": {
       "yeoman-generator": "^1.0.0"
     }
   }
   ```

4. Make sure that the latest version of yeoman-generator is a dependency.

   ```
   $ npm install --save yeoman-generator
   ```

5. Create a [bower.json](https://github.com/bower/spec/blob/master/json.md), a file that configures packages can be used as a dependency of another package.

   ```json
   {
     "name": "sample-project-gulp",
     "version": "0.0.0",
     "license": "MIT",
     "ignore": [
     "**/.*",
     "node_modules",
     "bower_components",
     "test",
     "tests"
   ],
   "dependencies": {
      "jquery": "~2.1.4" <% if(includeNormalize) { %>,
      "normalize.css": "~3.0.3" <% } %>
     }
   }
   ```

6. Edit the main.less file.

   ~~~ javascript
   <% if (includeNormalize) { %>
   @import (css)
      '../bower_components/normalize.css/normalize.css';
   <% } %>
   ~~~

7. Edit the index.html file.

   ~~~ html 
   <!DOCTYPE html>
   <html lang="en">
   <head>
   <meta charset="UTF-8">
   <title><%= projectTitle %></title>
      <link rel="stylesheet" href="styles/main.css">
   </head>
   <body>
      <!-- bower:js -->
      <!-- endbower -->
      <script src="scripts/main.min.js"></script>
   </body>
   </html>
   ~~~

8. Install the generator and call it.

   ~~~
   $ npm install -g generator-generator
   $ yo generator
   ~~~

9. Answer the questionnaire.
10. Copy templates into the generators/app/templates folder.
11. Edit the index.js file.

## Glossary

* generator. A generator is essentially a Node.js module. "A Yeoman generator is a tool that sets up new projects and provides the necessary files."
* scaffolding.
- yo. A command-line tool that is the "executor of generators".
