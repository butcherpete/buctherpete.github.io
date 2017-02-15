---
title: Yeoman Notes 
tags: [yeoman, tooling]
keywords: yeoman, tooling 
last_updated: February 6, 2017
summary: Yeoman helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. To do so, we provide a generator ecosystem. A generator is basically a plugin that can be run with the `yo` command to scaffold complete projects or useful parts. 
sidebar: notes_sidebar
permalink: yeoman_notes.html
folder: notes 
---

[Yeoman](http://yeoman.io/)

"The Yeoman workflow comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Gulp, Grunt etc) and the package manager (like npm and Bower)."

"Yeoman creates the necessary folders, copies initial files (like build scripts), applies boilerplate code, and triggers the installation of dependencies."

## Generators

The generator-generator enables you to create your own generator. 

### Creating Local Generators

## Tutorial Procedure

1. Create a folder to contain sample-project files.
2. Copy files from the original project.
   * main.js
   * package.json
   * gulpfile.js
   * main.less
   * bower.json
   * index.html

3. Copy files to the folder. 
4. Edit the bower.json file.

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

5. Edit the main.less file.

   ~~~ javascript
   <% if (includeNormalize) { %>
   @import (css)
      '../bower_components/normalize.css/normalize.css';
   <% } %>
   ~~~

6. Edit the index.html file.

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

7. Install the generator and call it.

   ~~~
   $ npm install -g generator-generator
   $ yo generator
   ~~~

8. Answer the questionnaire.
9. Copy templates into the generators/app/templates folder.
10. Edit the index.js file.

## Glossary

* generator. A generator is essentially a Node.js module. "A Yeoman generator is a tool that sets up new projects and provides the necessary files."
* scaffolding.
