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

As a math major, typing $\LaTeX$ equation becomes a necessity. The original jemdoc loads LATEX equations as PNG image that is pixelated! Then I found Mathjax, which is a JavaScript display engine for mathematics that works in all browsers!

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

To add your avator, create a folder named `images` in `assets` folder. Put your avator picture inside.

To edit the links, find your font awesome icons [here](https://www.w3schools.com/icons/default.asp). I did not find the brand icon for Google Scholar so I used `fas fa-fw fa-graduation-cap`.

You also want to edit the site settings. If you intend to write blog and enable comments. Follow the instruction for how to use [disqus](https://disqus.com/).

One additional thing I did is to add Google Analytics. See how to sign up for an Analytics account and Find your Analytics tracking ID at [here](https://support.google.com/sites/answer/97459?hl=en). In your `_config.yml`, you need to choose the provider as `provider: google-gtag` and put down your `tracking_id`.

### Adding favicons

Go to `custom.html` located in `/_includes/head`. Follow the instruction to add your favicons.

### Adding Mathjax supports

Go to `scripts.html` located in `/_includes`. Add this snippet at the end

```
<script type="text/javascript" async
	src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML">
</script>

<script type="text/x-mathjax-config">
   MathJax.Hub.Config({
     extensions: ["tex2jax.js"],
     jax: ["input/TeX", "output/HTML-CSS"],
     tex2jax: {
       inlineMath: [ ['$','$'], ["\\(","\\)"] ],
       displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
       processEscapes: true
     },
     "HTML-CSS": { availableFonts: ["TeX"] }
   });
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

### Editing home layout

The default homepage layout shows your recent posts, which is good if your website is just a blog. However, if you intend to display your website as a personal academic site like me, you will want the homepage to include basic information and disable the recent posts.

I have not found a perfect way, so I go to `home.html` located in `/_layouts` and delete the snippet after

```
<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>
```


Now go ahead to `index.html` and change the name to `index.md`, which enables you to write in markdown mode. If your website is hosted by Github Pages this is fine. Otherwise, you need to exports your `.md` file to `.html` file.

### ClustrMaps

[ClustrMaps](https://clustrmaps.com/) is a fancy widget that can track your website visitors from all over the world and visualize it using a real-time map. Follow the instruction from the official site to create your widget.

Go to `home.html` located in `/_layouts` and paste your Javascript at the end. Now you will see the change.

### Creating pages

Pages are aside from homepage. For a academic site, I need at least Publication page and Blog page.

Firstly, go to `navigation.yml` located in `/_data` to state your pages, mine looks like

```
# main links
main:
  # - title: "Quick-Start Guide"
  #   url: https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/
  - title: "Publications"
    url: /publications/
  - title: "Projects"
    url: /projects/
  - title: "Teaching"
    url: /teaching/
  - title: "Blog"
    url: /blog/
```

Next, create a folder `_pages` together with page files according the `navigation.yml`. Specify `layout: archive` and specify the `permalink` in each page corresponding to `navigation.yml`.

All the files ends with `.md` besides `blog.html`. This is because blog awareness, add the snippets inside thanks to [Liquid](https://shopify.dev/docs/themes/liquid/reference/basics)

```javascript
<ul>
  ...
</ul>
```

What if you want to create two different blog-like pages? Not sure yet, might have something to do with specifying the `category` in the post.

### Creating posts

Firstly, create a folder named `_posts` and then put all your posts in here.

To name your post, use `yyyy-mm-dd-title.md` as the post name. It will tell jekyll the date and title. Set your layout as `layout: single` and enable `comments: true` if you added comment provider in your `_config.yml`.

Happy blogging!
