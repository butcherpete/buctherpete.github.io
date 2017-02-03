---
title: Jazzy 
tags: [ios]
keywords: jazzy 
last_updated: February 2, 2017
summary: A list of useful Jazzy resources.
sidebar: notes_sidebar
permalink: jazzy_notes.html
folder: notes 
---

Setting up jazzy to produce documentation for public APIs.

Jazzy produces documentation similar in style to what Apple produces post WWDC 2014.

The documentation generated is a set of web pages and a docset that can be used with the Dash documentation viewer. Dash is free to download from the App Store, but will nag you to purchase.

## Installing Jazzy

To install Jazzy, open a Terminal session and run the command:

~~~~
$ sudo gem install --http-proxy https://proxy-chain.intel.com:912 --verbose jazzy
~~~~

## Generating Jazzy Docs

To generate Jazzy docs, run the commands:

~~~~
$ cd <directory for your Xcode project>   
$ jazzy -o com.intel.wearable.core.CoreIQ.docs -m CoreIQ
~~~~

## Packaging Jazzy Docs for Distribution

To package Jazzy docs, run the commands:

~~~~
$ zip -r CoreIQDocs.zip com.intel.wearable.core.CoreIQ.docs 
~~~~

Production and packaging will be integrated into Xcode so it can be released with the SDK

## Jazzy Command Line Options

 Command      |  Description                      
 --------     |  ------------
`-o`, `--output FOLDER` | Folder to output the HTML docs to.                               
`-c`, `--[no-]clean`    | Delete contents of output directory before running. WARNING: If --output is set to `~/Desktop,` this will delete the `~/Desktop` directory.            
`--[no-]objc`         | Generate docs for Objective-C.    
`--umbrella-header PATH` | Umbrella header for your Objective-C framework.
`--framework-root PATH` | The root path to your Objective-C framework.
`--sdk [iphone|watch|appletv][os|simulator]|mac osx]` | The SDK for which your code should be built.
`--config PATH`       | Configuration file (`.yaml` or `.json`) Default: `.jazzy.yaml` in source directory or ancestor.  
-x arg1,arg2,…argN, --xcodebuild-arguments | Arguments to forward to xcodebuild.                       
`-s FILEPATH`, `--sourcekitten-sourcefile` | File generated from sourcekitten output to parse.
`--source-directory DIRPATH`    | The directory that contains the source to be documented.          
`-e file1,file2,directory3,…fileN,--exclude`  | Files/directories to be excluded from documentation.
`--swift-version VERSION` | .
`-a`, `--author AUTHOR_NAME` | Name of author to attribute in docs (e.g. Realm)
`-u`, `--author_url URL` | Author URL of this project (e.g. http://realm.io)    
`-m`, `--module MODULE_NAME` | Name of module being documented (e.g. RealmSwift).                
`--module-version VERSION` | Module version; Used when generating docset.              
`--copyright COPYRIGHT_MARKDOWN` | Copyright markdown rendered at the bottom of the docs pages.   
`--readme FILEPATH README` [file]   | The path to a Markdown file.                    
`--documentation GLOB` | Glob that matches available documentation.                  
`--abstract GLOB`     | Glob that matches available abstracts for categories.       
`--docset-icon FILEPATH` | The relative path for the generated docset.               
`--docset-path DIRPATH`         |                                   
`--podspec FILEPATH`  |                                   
`-r`, `--root-url URL`  | Absolute URL root where these docs will be stored.              
`-d`, `--dash_url URL`  | Location of the dash XML feed e.g.`http://realm.io/docsets/realm.xml`)       
`-g`, `--github_url URL` | GitHub URL of this project (e.g.https://github.com/realm/realm-cocoa)&gt;   
`--github-file-prefix PREFIX` | GitHub URL file prefix of this project (e.g. https://github.com/realm/realm-cocoa/tree/v0.87.1)         
`--skip-documentation` | Will skip the documentation generation phase.             
`--min-acl [private`  | Minimum access control level to document.
`--[no-]skip-undocumented` | Don't document declarations that have no documentation comments.
`--[no-]hide-documentation-coverage` | Hide "(X% documented)" from the generated documents.
`--head HTML`         | Custom HTML to inject into.
`--theme [apple | fullwidth | DIRPATH]` | Which theme to use. Specify either 'apple' (default),'fullwidth' or the path to your mustache templates and other assets for a custom theme.     
-t, --template-directory DIRPATH | DEPRECATED: Use `--theme` instead.  
`--assets-directory DIRPATH`  | DEPRECATED: Use `--theme` instead.                       
`-v`, `--version`   | Print version number. 
`-h`, `--help [TOPIC]`     | Available topics: usage Command line options (this help message) config Configuration file options ...or an option keyword, e.g."dash"                            

## Jazzy Lint

<https://github.com/google/arc-jazzy-linter>

 

## Reference Materials

<http://nshipster.com/swift-documentation/> 



