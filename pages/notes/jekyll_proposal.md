---
title: Jekyll Proposal 
tags: [jekyll]
keywords: jekyll 
last_updated: February, 2017
summary: A list of useful Jekyll resources.
sidebar: notes_sidebar
permalink: jekyll_proposal.html
folder: notes 
---

## Problem Statement

We need to integrate ASW and CSW documentation.

### Requirements

* Requirement 1: CSW documentation must be maintained in its own repository.
* Requirement 2: Initial CSW docs are written in Markdown if possible. 
* Requirement 3: Initial explanation of new APIs is written by a developer
* Requirement 4: Feature description is modified as necessary by technical writer and changes are committed back to the repository.
* Requirement 5: Custom CSS themes must be applied during final document generation to get a uniform theme for all docs.
* Requirement 6: Documentation is automatically generated and published along with the binary release.
* Requirement 7: Bug fixes to code samples in documentation done by tech writer and verified by developer (tech writer assumed to have working dev environment)

## Proposed Solution

I propose a solution that uses the following elements:

* A static webpage generator.
* kramdown.
* CSS will need to change: use a new syntax highlighting.

### Requirement 1

ASW (Android), ASW (iOS/DSW), and CSW documentation will contnue to be stored in distinct Stash repositories.

Jekyll generates a static HTML site from Markdown (kramdown) and saves the generated HTML files in the `_site` folder.

### Requirement 2: Inital Documentation Written in Markdown

Documents can be written in either Markdown (kramdown) or HTML5.

Jekyll ignores HTML files and generates new web pages from Markdown files only. The generated HTML files and the HTML file share the same 

### Requirement 3: Initial Documentation Written by Developer

Developers can write in Markdown. Kramdown is (mostly) compatible with Github Flavored Markdown (GFM).

Developers can check the docs into the repository.

## Prototype
