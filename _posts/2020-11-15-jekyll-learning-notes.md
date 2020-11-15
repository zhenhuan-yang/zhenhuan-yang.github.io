---
layout: single
title: "Jekyll Learning Notes"
author-profile: true
comments: true
---

Let us be honest. Building a personal academic website is essential, but nightmare-ful for a non-cs major PhD. This post summarizes all the experience/suffering that I have.

## Good old days with jemdoc

[jemdoc](https://jemdoc.jaboc.net/) is a light text-based markup language designed for creating websites, developed by Jacob Mattingley. It is popular among researchers, for example, [Stephen P. Boyd](https://web.stanford.edu/~boyd/).

### Setting up jemdoc

Following the official site can fail even if you are the superuser! Instead, follow [here](http://www-personal.umich.edu/~wylguan/using-jemdoc.html).

### jemdoc + Mathjax

As a math major, typing Latex equation becomes a necessity. The original jemdoc loads LATEX equations as PNG image that is pixelated! Then I found Mathjax, which is a JavaScript display engine for mathematics that works in all browsers!

[Wonseok Shin](http://www.mit.edu/~wsshin/jemdoc+mathjax.html) made this possible. The usage is quite simple, just change your `mysite.conf` and do

```
../jemdoc -c mysite.conf *.jemdoc
```

when you compile. Check details [here](https://github.com/wsshin/jemdoc_mathjax).
