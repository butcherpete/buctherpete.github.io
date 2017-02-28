---
title: Bundler 
tags: [bundler, ruby]
keywords: bundler, ruby 
last_updated: February 18, 2017
summary: 
sidebar: notes_sidebar
permalink: ruby_bundler.html
folder: notes 
---

## Gemfile

### Version Specifiers

"Most of the version specifiers, like >= 1.0, are self-explanatory. The specifier ~> has a special meaning, best shown by example. ~> 2.0.3 is identical to >= 2.0.3 and < 2.1. ~> 2.1 is identical to >= 2.1 and < 3.0. ~> 2.2.beta will match prerelease versions like 2.2.beta.12. ~> 0 is identical to >= 0.0 and < 1.0."

### Gemfile.lock

> After developing your application for a while, check in the application together with the Gemfile and Gemfile.lock snapshot. Now, your repository has a record of the exact versions of all of the gems that you used the last time you know for sure that the application worked...
>
>This is important: the Gemfile.lock makes your application a single package of both your own code and the third-party code it ran the last time you know for sure that everything worked. Specifying exact versions of the third-party code you depend on in your Gemfile would not provide the same guarantee, because gems usually declare a range of versions for their dependencies.
