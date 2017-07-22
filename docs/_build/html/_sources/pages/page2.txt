# Introduction

Jekyll is a text transformation engine and static site generator. The concept behind the system is this: you give it text written in your favorite markup language, be that Markdown, Textile, or just plain HTML, and it churns that through a layout or a series of layout files. 

See https://jekyllrb.com/docs/structure/

[See Markdown](/markdown/index.html)

Jekyll and GitHub Pages:

https://24ways.org/2013/get-started-with-github-pages/
http://jmcglone.com/guides/github-pages/

# Basic Setup

Do this after installation.

1: Run `jekyll new <name>` to create a new site, bundle install, resolve default dependencies, and create default config files:

```
jekyll new mynewsite
cd mynewsite
```

These files were autogen'd at the root of the source directory:

```
_config.yml	
Gemfile		
Gemfile.lock
_posts		
about.md	
index.md
```

Jekyll's configuration file is `_config.yml`. Bundler uses `Gemfile` and `Gemfile.lock` to keep track of required gems.

2: Open the `_config.yml` configuration file:

```
vi _config.yml
```

then add some basic info:

```
title: Kringle KB
name: Greg McMillan
email: gmcmillan100@gmail.com
```

3: Build the site on the local preview server then visit http://127.0.0.1:4000/ when prompted:

```
jekyll serve
```

When `jekyll serve` runs, it automatically creates a `_site` directory at the project's root. That’s where files are saved when they’re turned into static HTML. Don’t touch the files in here — they’re the generated files and will get overwritten every time changes are made.

4: Create `.gitignore` and ignore the `_site` directory that Jekyll automatically generates each time you commit:

```
vi .gitignore
```

and put this in it:

```
_site
```

# Baseurl

In `_config.yml`, set baseurl to the subpath of your site:

``
baseurl: "/docs"
``

For example on github, the URL above resolves to this:

```
https://gmcmillan100.github.io/docs/
```
On an .md page, add the `site.baseurl` to the `page.url` to resolve:

```ruby
 <li><a href="{{ site.baseurl }}{{ page.url }}">{{ page.title }}</a></li>
```