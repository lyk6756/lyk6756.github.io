---
layout: post
title:  "Use Pygments for Code Snippet Highlighting in Jekyll"
---

If Pygments is set in your `_config.yml` file then your pages site will automatically build with Rouge as the default highlighter instead.

# What is pygments

Pygments is a generic syntax highlighter written in python, suitable for use in code hosting, forums, wikis or other applications that need to prettify source code.

# Install pygments on Ubuntu 16.04

There are varies ways to install pygments.

According to the [official download and installation guide](http://pygments.org/download/), we can download Pygments from the [Python Package Index](https://pypi.python.org/pypi/Pygments), or install it with [pip](https://pip.pypa.io/en/stable/), which is a package management system used to install and manage software packages written in Python:

```shell
$ sudo pip install Pygments
```

If the program `pip` is currently not installed. You can install it by typing:

```shell
$ sudo apt install python-pip
```

under a ubuntu system. Follow the [Pip Installation Page](https://pip.pypa.io/en/stable/installing/#installation) to learn more.

Under Linux, most distributions include a package for Pygments, usually called `pygments` or `python-pygments`. You can install it with the package manager as usual.

As for ubuntu system, an alternative way installing pygments is by using `apt-get` command:

```shell
$ sudo apt-get install python-pygments
```

# Code style

Pygments provides multiple builtin code styles work for both the HTML and LaTeX formatter.

To get a list of known styles we can use this snippet:

{% highlight python %}
>>> from pygments.styles import STYLE_MAP
>>> STYLE_MAP.keys()
['manni', 'igor', 'lovelace', 'xcode', 'vim', 'autumn', 'vs', 'rrt', 'native', 'perldoc', 'borland', 'tango', 'emacs', 'friendly', 'monokai', 'paraiso-dark', 'colorful', 'murphy', 'bw', 'pastie', 'algol_nu', 'paraiso-light', 'trac', 'default', 'algol', 'fruity']
{% endhighlight %}

Here shows all the available styles on my laptop.

For a direct and clear review of all these styles, check the [Pygments online demo](http://pygments.org/demo/) page to learn more.

# Enable pygments in jekyll

A few settings are needed to enable pygments in jekyll.

Since Rouge is the default highlighter in Jekyll and GitHub Pages, if Pygments is set in your `_config.yml` file then your pages site will automatically build with Rouge as the default highlighter instead.

However, Rouge themes are 100% compatible with Pygments' stylesheets. So we can replace rouge's stylesheets with Pygments' manually.

First, we should get the syntax highlighting stylesheet file. To generate  it, execute the following command from the Shell:

```shell
$ pygmentize -S colorful -f html > _syntax-highlighting.scss
```

where `-S` option gives a specific style name, here I choose `colorful` for my snippet; `-f` option selects a formatter. This command will generate a [`_syntax-highlighting.scss`](https://github.com/lyk6756/lyk6756.github.io/blob/master/_sass/minima/_syntax-highlighting.scss) file in current directory.

Then, call this file in your website layout configuration.

As for my site, I simply put this file under the directory `/_sass/minima/`, replacing the old [`_syntax-highlighting.scss`](https://github.com/jekyll/minima/blob/master/_sass/minima/_syntax-highlighting.scss) file.

Now push your new settings onto GitHub Pages. You will see the difference. Enjoy!

# Disable syntax Highlighting

Simply change `highlighter: rouge` to `highlighter: false` in your `_config.yml` file.

# Further reading

* [Jekyll高亮的另一个选择:JS高亮](https://ruby-china.org/topics/6168)
* [Jekyll 中的语法高亮：Pygments](http://havee.me/internet/2013-08/support-pygments-in-jekyll.html)
* [用Jekyll和Pygments配置代码高亮](http://zyzhang.github.io/blog/2012/08/31/highlight-with-Jekyll-and-Pygments/)
