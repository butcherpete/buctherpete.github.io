---
title: Conda 
tags: [python]
keywords:  
last_updated: March 7, 2017
summary: Conda is a cross-platform, language-agnostic binary package manager. It is the package manager used by Anaconda installations, but it may be used for other systems as well. Conda makes environments first-class citizens, making it easy to create independent environments even for C libraries. Conda is written entirely in Python, and is BSD licensed open source.
sidebar: notes_sidebar
permalink: python_conda.html
folder: notes 
---

- [conda/conda](https://github.com/conda/conda)
- [Conda docs](https://conda.io/docs/)

## View Installed Packages

~~~python
$ conda list
~~~

## Search for Packages

~~~python
$ conda search 
~~~

## Install Packages

~~~python
$ conda install <package-name> 
~~~

## Activate Environment 

~~~python
$ conda create -n numpy16 ipython-notebook numpy=1.6 
$ source activate numpy16
~~~


~~~python
$ conda create -n python2 python=2.7 anaconda
$ source activate python2
~~~

## Deactivate Environment

~~~python
$ source deactivate 
~~~
