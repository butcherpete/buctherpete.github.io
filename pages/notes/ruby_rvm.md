---
title: RVM 
tags: [rvm, ruby]
keywords: jekyll, notes 
last_updated: February 18, 2017
summary: 
sidebar: notes_sidebar
permalink: ruby_rvm.html
folder: notes 
---

## Installation

1. Install gnupg2.

   ```
   $ brew install gnupg2
   ```

2. Install the mpapis public key.

   ```
   $ gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

   In case of problems: https://rvm.io/help and https://twitter.com/rvm_io
   rvm 1.29.0 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io/]
   Searching for binary rubies, this might take some time.
   No binary rubies available for: osx/10.12/x86_64/ruby-2.4.0.
   Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.

   ``` 

3. Install rvm using the latest stable version of Ruby.

   ```
   $ \curl -sSL https://get.rvm.io | bash -s stable --ruby
   ```

4. Source the rvm scripts in all open shell windows.

   ```
   $ source /Users/toddeugX/.rvm/scripts/rvm 
   ```
5. "Newer versions of OSX deprecated openSSL, leaving lots of stuff broken. You need to reinstall ruby, but specify exactly where your openSSL libraries are. If you're using rvm then that looks like"

   ```
   $ rvm reinstall 2.4.0 --with-openssl-dir=/usr/local/opt/openssl
   ```
6. Because yajl 1.1.0 conflicts with ruby 2.4.0, I hade to revert to Ruby 2.2.0
   ```
   $ rvm use 2.2.0
   ```

## Troubleshooting

Repairing RVM path problems:

```
$ rvm get stable --auto-dotfiles
```

Cleaning up:

```
$ rvm cleanup
```

### Ruby Conflict Errors 

Fixing Ruby conflict errors:

```
$ rvm use <ruby-version>
$ bundle update
```

### Open SSL Mess

[OpenSSL Errors and Rails](https://railsapps.github.io/openssl-certificate-verify-failed.html)

```
$ rvm osx-ssl-certs status all
$ rvm osx-ssl-certs update all
```

