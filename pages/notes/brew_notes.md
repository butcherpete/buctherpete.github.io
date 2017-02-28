---
title: Homebrew 
tags: [homebrew]
keywords:  
last_updated: February 19, 2017
summary: Homebrew notes
sidebar: notes_sidebar
permalink: brew_notes.html
folder: notes 
---


## Homebrew Bundle
[Homebrew/homebrew-bundle](https://github.com/Homebrew/homebrew-bundle)

### Install

~~~
$ brew tap Homebrew/bundle
~~~

### Install Dependencies from Brewfile 

~~~
$ brew bundle
~~~

### Generate Brewfile

~~~
$ brew bundle dump

tap 'caskroom/cask'
tap 'homebrew/bundle'
tap 'homebrew/core'
tap 'homebrew/services'
tap 'raggi/ale'
brew 'ack'
brew 'docbook'
brew 'asciidoc'
brew 'autoconf'
brew 'automake'
brew 'carthage'
brew 'coreutils'
brew 'cowsay'
brew 'libgpg-error'
brew 'libassuan'
brew 'libgcrypt'
brew 'libksba'
brew 'pth'
brew 'dirmngr'
brew 'docker'
brew 'docker-machine'
brew 'docx2txt'
brew 'exiftool'
brew 'lame'
brew 'x264'
brew 'xvid'
brew 'ffmpeg'
brew 'libpng'
brew 'freetype'
brew 'gdbm'
brew 'jpeg'
brew 'libtiff'
brew 'little-cms2'
brew 'ghostscript'
brew 'gnupg'
brew 'pinentry'
brew 'gpg-agent'
brew 'libusb'
brew 'libusb-compat'
brew 'gnupg2'
brew 'grip'
brew 'heroku'
brew 'htmldoc'
brew 'hub'
brew 'icu4c'
brew 'libtool'
brew 'perl'
brew 'xz'
brew 'imagemagick'
brew 'libyaml'
brew 'markdown'
brew 'openssl'
brew 'mongodb', restart_service: true
brew 'openssl@1.1'
brew 'pandoc'
brew 'pcre'
brew 'pdf-redact-tools'
brew 'pkg-config'
brew 'readline'
brew 'sqlite'
brew 'python'
brew 'postgresql'
brew 'ruby-build'
brew 'rbenv'
brew 'ruby'
brew 'the_silver_searcher'
brew 'tidy-html5'
brew 'unrar'
brew 'vim'
brew 'raggi/ale/openssl-osx-ca'
cask 'diffmerge'
cask 'kdiff3'
cask 'ngrok'
~~~
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
