---
layout: single
title: "Jekyll Learning Notes"
author-profile: true
comments: true
---

Let us be honest. Building a personal academic website is essential, yet nightmare-ful for a non-cs major. This post summarizes all the experience/suffering that I have.

## Good old days with jemdoc

[jemdoc](https://jemdoc.jaboc.net/) is a light text-based markup language designed for creating websites, developed by Jacob Mattingley. It is popular among researchers, for example, [Stephen P. Boyd](https://web.stanford.edu/~boyd/).

### Setting up jemdoc

Following the official site can fail even if you are the superuser! Instead, follow [here](http://www-personal.umich.edu/~wylguan/using-jemdoc.html).

### Hosting your websites

After you build your badass website, you will want to publish and show off (isn't that all that matters?). If you are a student/faculty/staff in college, contact your Information Technology Services for hosting. Otherwise, try out [Github Pages](https://pages.github.com/).

### jemdoc + Mathjax

As a math major, typing Latex equation becomes a necessity. The original jemdoc loads LATEX equations as PNG image that is pixelated! Then I found Mathjax, which is a JavaScript display engine for mathematics that works in all browsers!

[Wonseok Shin](http://www.mit.edu/~wsshin/jemdoc+mathjax.html) made this possible. The usage is quite simple, just change your `mysite.conf` and do

```
../jemdoc -c mysite.conf *.jemdoc
```

when you compile. Check details [here](https://github.com/wsshin/jemdoc_mathjax).


### Writing blog with jupyter notebook

Since `jemdoc.py` is a python file, I intuitively created a python project with [Pycharm](https://www.jetbrains.com/pycharm/) editor. Later I found it is not necessary but I am happy with my choice, since it comes with Terminal feature and you can just `jemdoc` in there. Besides you can call `jupyter notebook`, which is an amazing markdown tool as it

* supports LATEX display
* exports to `.html` easily

## Migrating to Jekyll

Yes, if you are satisfied with the jemdoc site, then you can close this post right away (save you huge time I guarantee!). Yet I wanted to make my website a little bit fancier. Let me cut to the chase, after going to hell and back, I found my treasure - Jekyll.

Just like jemdoc, [Jekyll](https://jekyllrb.com/) is also a static site generator. It has the following pro

* Blog-aware
* Free hosting with GitHub Pages
* Good community with rich choice of theme templates

Nonetheless, it has the following con

* It is heavy in coding and I know nothing about it!

Jekyll is a [Ruby](https://www.ruby-lang.org/en/) [Gem](https://guides.rubygems.org/what-is-a-gem/) that can be installed on most systems. If you are on macOS like me, you probably have it pre-installed. Without knowing anything about Ruby, all you have to do now is to install the jekyll and [bundler](https://bundler.io/) gems.

```
gem install jekyll bundler
```

### Life saver: Minimal Mistakes

[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) is a flexible two-column Jekyll theme, perfect for building personal sites, blogs, and portfolios.

I didn't install the theme following the [guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/), instead, I forked the repository and rename it as `username.github.io`. And then I `git clone` my own repository to remove the unnecessary as [suggested](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).

Do not remove `minimal-mistakes-jekyll.gemspec` if you are not planing to mess up with Ruby like me!

### First time builing...

To build the website locally, `cd` into your local repository and run

```
bundle install
bundle exec jekyll serve
```

Here `bundle install` will download the necessary gem packages and create a `Gemfile.lock` file and `bundle exec` will stick your gem packages version to `Gemfile.lock`. `jekyll serve` will build your website locally. 
