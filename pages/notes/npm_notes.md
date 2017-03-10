---
title: NPM 
tags: [tooling, npm]
keywords: npm 
last_updated: February 9, 2017
summary: npm makes it easy for JavaScript developers to share and reuse code, and it makes it easy to update the code that you're sharing. 
sidebar: notes_sidebar
permalink: npm_notes.html
folder: notes 
---

## Resources
[NPM documentation](https://docs.npmjs.com/)

## Global Installation

### Updating

To update npm:

~~~
$ npm install npm@latest -g
~~~

## Installing Locally

"A package can be downloaded with the command"

~~~
npm install <package_name>
~~~

## Package.JSON

To create a package.json:

~~~
$ npm init
~~~

Two required fields in the package.json:

- name
- version

To add a package to the package.json:

~~~
$ npm install <package_name> --save
~~~

When you install a package using this method, the package is saved to the package.json. The version number is prefixed with a `^` to indicate that the latest stable version was installed. For example, `"generator-mocha": "^0.3.1"`.

To install packages from package.json:

~~~
$ npm install
~~~

### Updating Deprecated Packages

If you see an error that indicates that the required package is deprecated, install the package globally specifying the correct version:

~~~
npm WARN deprecated minimatch@2.0.10: Please update to minimatch 3.0.2 or higher to avoid a RegExp DoS issue
- cross-spawn-async@2.2.5 node_modules/cross-spawn-async

$ npm install -g minimatch@3.0.2
~~~

## Semantic Versioning

Semantic versioning (or semvar) is a standard notation method for identifying changes to releases.
