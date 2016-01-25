---
title: "simiki-介绍"
layout: page
date: 2016-01-25 00:00
---

# Simiki #

Simiki is a simple wiki framework, written in [Python](https://www.python.org/).

* Easy to use. Creating a wiki only needs a few steps
* Use [Markdown](http://daringfireball.net/projects/markdown/). Just open your editor and write
* Store source files by category
* Static HTML output
* A CLI tool to manage the wiki

Simiki is short for `Simple Wiki` :)

## Quick Start ##

### Install ###

	pip install simiki

### Update ###

	pip install -U simiki

### Init Site ###

	mkdir mywiki && cd mywiki
	simiki init

### Create a new wiki ###

	simiki new -t "Hello Simiki" -c first-catetory

### Generate ###

	simiki generate

### Preview ###

	simiki preview

For more information, `simiki -h` or have a look at [Simiki.org](http://simiki.org)

## Others ##

* [simiki.org](http://simiki.org)
* <https://github.com/tankywoo/simiki>
* Email: <me@tankywoo.com>

## License ##

The MIT License (MIT)

Copyright (c) 2013 Tanky Woo

