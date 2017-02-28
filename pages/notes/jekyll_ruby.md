---
title: Ruby Notes 
tags: [jekyll, ruby]
keywords: jekyll, ruby
last_updated: February 15, 2017
summary: Basically, I hate Ruby.
sidebar: notes_sidebar
permalink: jekyll_ruby.html
folder: notes 
---

## RVM

### Installing

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

## Bundler

[Bundler Docs](https://bundler.io/v1.13/man/bundle-update.1.html)

## Getting System Information

~~~
$ gem -v
2.4.6

$ ruby -v
ruby 2.2.0p0 (2014-12-25 revision 49005) [x86_64-darwin14]

$ rvm -v
rvm 1.29.0 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io/]

$ rvm -env
export PATH="/Users/toddeugX/.rvm/gems/ruby-2.2.0/bin:/Users/toddeugX/.rvm/gems/ruby-2.2.0@global/bin:/Users/toddeugX/.rvm/rubies/ruby-2.2.0/bin:$PATH"
export GEM_HOME='/Users/toddeugX/.rvm/gems/ruby-2.2.0'
export GEM_PATH='/Users/toddeugX/.rvm/gems/ruby-2.2.0:/Users/toddeugX/.rvm/gems/ruby-2.2.0@global'
export MY_RUBY_HOME='/Users/toddeugX/.rvm/rubies/ruby-2.2.0'
export IRBRC='/Users/toddeugX/.rvm/rubies/ruby-2.2.0/.irbrc'
unset MAGLEV_HOME
unset RBXOPT
export RUBY_VERSION='ruby-2.2.0'

$ bundle -v
Bundler version 1.14.3

$ openssl s_client -showcerts -connect rubygems.org:https
# Returns nothing

~~~

To view a list of gems, run `gem list`:

~~~
*** LOCAL GEMS ***

activesupport (4.2.7)
addressable (2.5.0)
bigdecimal (default: 1.3.0)
blankslate (2.1.2.4)
bundler (1.14.3)
CFPropertyList (2.3.5)
claide (1.0.1)
classifier (1.3.4)
cocoapods (1.2.0)
cocoapods-core (1.2.0)
cocoapods-deintegrate (1.0.1)
cocoapods-downloader (1.1.3)
cocoapods-plugins (1.0.0)
cocoapods-search (1.0.0)
cocoapods-stats (1.0.0)
cocoapods-trunk (1.1.2)
cocoapods-try (1.1.0)
coffee-script (2.4.1)
coffee-script-source (1.12.2)
colorator (1.1.0, 0.1)
colored (1.2)
commander (4.1.6)
did_you_mean (1.1.0)
escape (0.0.4)
ethon (0.10.1)
execjs (2.7.0)
faraday (0.11.0)
fast-stemmer (1.0.2)
ffi (1.9.17)
forwardable-extended (2.6.0)
fourflusher (2.0.1)
fuzzy_match (2.0.4)
gemoji (2.1.0)
gh_inspector (1.0.3)
github-pages (117)
github-pages-health-check (1.3.0)
highline (1.6.21)
html-pipeline (2.5.0)
i18n (0.8.0)
io-console (default: 0.4.6)
jazzy (0.7.3)
jekyll (3.3.1)
jekyll-avatar (0.4.2)
jekyll-coffeescript (1.0.1)
jekyll-default-layout (0.1.4)
jekyll-feed (0.8.0)
jekyll-gist (1.4.0)
jekyll-github-metadata (2.3.1)
jekyll-mentions (1.2.0)
jekyll-optional-front-matter (0.1.2)
jekyll-paginate (1.1.0)
jekyll-readme-index (0.0.3)
jekyll-redirect-from (0.11.0)
jekyll-relative-links (0.2.1)
jekyll-sass-converter (1.5.0)
jekyll-seo-tag (2.1.0)
jekyll-sitemap (0.12.0)
jekyll-swiss (0.4.0)
jekyll-theme-architect (0.0.3)
jekyll-theme-cayman (0.0.3)
jekyll-theme-dinky (0.0.3)
jekyll-theme-hacker (0.0.3)
jekyll-theme-leap-day (0.0.3)
jekyll-theme-merlot (0.0.3)
jekyll-theme-midnight (0.0.3)
jekyll-theme-minimal (0.0.3)
jekyll-theme-modernist (0.0.3)
jekyll-theme-primer (0.1.7)
jekyll-theme-slate (0.0.3)
jekyll-theme-tactile (0.0.3)
jekyll-theme-time-machine (0.0.3)
jekyll-titles-from-headings (0.1.4)
jekyll-watch (1.5.0)
jemoji (0.7.0)
json (default: 2.0.2, 1.8.6)
kramdown (1.13.2, 1.11.1)
liferaft (0.0.6)
liquid (3.0.6, 2.5.5)
listen (3.0.8, 3.0.6)
maruku (0.7.3)
mercenary (0.3.6)
mini_portile2 (2.1.0)
minima (2.1.0, 2.0.0)
minitest (5.10.1)
molinillo (0.5.5)
multipart-post (2.0.0)
mustache (0.99.8)
nanaimo (0.2.3)
nap (1.1.0)
net-dns (0.8.0)
net-telnet (0.1.1)
netrc (0.7.8)
nokogiri (1.6.8.1)
octokit (4.6.2)
open4 (1.3.4)
openssl (default: 2.0.2)
parslet (1.5.0)
pathutil (0.14.0)
posix-spawn (0.3.13)
power_assert (0.4.1)
psych (default: 2.2.2)
public_suffix (2.0.5)
rake (12.0.0)
rb-fsevent (0.9.8)
rb-inotify (0.9.8)
rb-kqueue (0.2.4)
rdoc (default: 5.0.0)
redcarpet (3.4.0, 2.3.0)
rouge (1.11.1)
ruby-macho (0.2.6)
safe_yaml (1.0.4, 0.9.7)
sass (3.4.23)
sawyer (0.8.1)
sqlite3 (1.3.13)
terminal-table (1.7.3)
test-unit (3.2.3)
thread_safe (0.3.5)
typhoeus (0.8.0)
tzinfo (1.2.2)
unicode-display_width (1.1.3)
xcinvoke (0.3.0)
xcodeproj (1.4.2)
xmlrpc (0.2.1)
~~~

## Ruby Configurations

To view ruby config, run `gem env`:

~~~
RubyGems Environment:
  - RUBYGEMS VERSION: 2.6.10
  - RUBY VERSION: 2.4.0 (2016-12-24 patchlevel 0) [x86_64-darwin16]
  - INSTALLATION DIRECTORY: /usr/local/lib/ruby/gems/2.4.0
  - USER INSTALLATION DIRECTORY: /Users/toddeugX/.gem/ruby/2.4.0
  - RUBY EXECUTABLE: /usr/local/opt/ruby/bin/ruby
  - EXECUTABLE DIRECTORY: /usr/local/bin
  - SPEC CACHE DIRECTORY: /Users/toddeugX/.gem/specs
  - SYSTEM CONFIGURATION DIRECTORY: /usr/local/Cellar/ruby/2.4.0/etc
  - RUBYGEMS PLATFORMS:
    - ruby
    - x86_64-darwin-16
  - GEM PATHS:
     - /usr/local/lib/ruby/gems/2.4.0
     - /Users/toddeugX/.gem/ruby/2.4.0
     - /usr/local/Cellar/ruby/2.4.0/lib/ruby/gems/2.4.0
  - GEM CONFIGURATION:
     - :update_sources => true
     - :verbose => true
     - :backtrace => false
     - :bulk_threshold => 1000
  - REMOTE SOURCES:
     - https://rubygems.org/
  - SHELL PATH:
     - /usr/local/var/rbenv/shims
     - /Users/toddeugX/bin
     - /usr/local/bin
     - /usr/bin
     - /bin
     - /usr/sbin
     - /sbin
~~~

## Open SSL

To view openSSL version:

~~~
$ ruby -ropenssl -e 'p OpenSSL::OPENSSL_VERSION'
"OpenSSL 1.0.2j  26 Sep 2016"
~~~
