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

Just like jemdoc, [Jekyll](https://jekyllrb.com/) is also a static site generator. It has the following pros

* Blog-aware
* Free hosting with GitHub Pages
* Good community with rich choice of theme templates

Nonetheless, it has the following cons

* It is heavy in coding and I know nothing about it!

Jekyll is a [Ruby](https://www.ruby-lang.org/en/) [Gem](https://guides.rubygems.org/what-is-a-gem/) that can be installed on most systems. If you are on macOS like me, you probably have it pre-installed. Without knowing anything about Ruby, all you have to do now is to install the jekyll and [bundler](https://bundler.io/) gems.

```
gem install jekyll bundler
```

### Life saver: Minimal Mistakes

[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) is a flexible two-column Jekyll theme, perfect for building personal sites, blogs, and portfolios.

I didn't install the theme following the [guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/), instead, I forked the repository and rename it as `username.github.io`. And then I `git clone` my own repository to remove the unnecessary as [suggested](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/). Whenever you have made changes to your local repository, you have to stage, commit and push.

```
git add
git commit -a
git push origin master
```

Do not remove `minimal-mistakes-jekyll.gemspec` if you are not planing to mess up with Ruby like me! I accidentally deleted it so I have to `cd` into your local repository and run

```
touch minimal-mistakes-jekyll.gemspec
vim minimal-mistakes-jekyll.gemspec
```


### First time building...

To build the website locally, `cd` into your local repository and run

```
bundle install
bundle exec jekyll serve
```

Here `bundle install` will download the necessary gem packages and create a `Gemfile.lock` file and `bundle exec` will stick your gem packages version to `Gemfile.lock`. And `jekyll serve` will build your website locally. You can now check out your local website from your local server (check your terminal message).

Alternatively, I use [Atom](https://atom.io/) instead of terminal directly. Atom is an amazing editor built with HTML, JavaScript, CSS, and Node.js integration. Therefore you can easily bulid your jekyll website by installing the Atom jekyll package. Furthermore, Atom can be configured with your Github account and repo, allows you to git without command line!

### Editing `_config.yml`

To make the website looks like yours, start with editing `_config.yml` to the site author with your information.

To edit the links, find your font awesome icons [here](https://www.w3schools.com/icons/default.asp). I did not find the brand icon for Google Scholar so I used `fas fa-fw fa-graduation-cap`.

You also want to edit the site settings. If you intend to write blog and enable comments. Follow the instruction for how to use [disqus](https://disqus.com/).

One additional thing I did is to add Google Analytics. See how to sign up for an Analytics account and Find your Analytics tracking ID at [here](https://support.google.com/sites/answer/97459?hl=en). In your `_config.yml`, you need to choose the provider as `provider: google-gtag` and put down your `tracking_id`.

### Adding favicons

Go to `custom.html` located in `/_includes/head`. Follow the instruction to add your favicons.

### Adding Mathjax supports

Go to `scripts.html` located in `/_includes`. Add this snippet at the end

```
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" defer
        src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
```

Enable MathJax in `_config.yml` by adding `mathjax: true` to the page defaults

```
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      mathjax: true
```
