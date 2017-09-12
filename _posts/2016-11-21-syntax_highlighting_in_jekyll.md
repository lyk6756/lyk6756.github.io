---
layout: post
title:  "Syntax Highlighting in Jekyll on GitHub Pages"
---

>If you’re the kind of person who is using Jekyll, then chances are you’ll want to enable syntax highlighting using [Pygments](http://pygments.org/) or [Rouge](http://rouge.jneen.net/).

# Code snippet highlighting

Jekyll has built in support for syntax highlighting of over 60 languages thanks to Rouge. Rouge is the default highlighter in Jekyll 3 and above. To use it in Jekyll 2, set highlighter to rouge and ensure the rouge gem is installed properly.

Alternatively, you can use Pygments to highlight your code snippets. To use Pygments, you must have Python installed on your system, have the `pygments.rb` gem installed and set `highlighter` to `pygments` in your site’s configuration file. Pygments supports over 100 languages

To render a code block with syntax highlighting, surround your code as follows:

{% highlight text %}
{% raw %}{% highlight ruby %}{% endraw %}
def foo
  puts 'foo'
end
{% raw %}{% endhighlight ruby %}{% endraw %}
{% endhighlight %}

Then, it will render as

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

The argument to the `highlight` tag (`ruby` in the example above) is the language identifier. To find the appropriate identifier to use for the language you want to highlight, look for the “short name” on the [Rouge wiki] or the [Pygments' Lexers page].

[Rouge wiki]: https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers
[Pygments' Lexers Page]: http://pygments.org/docs/lexers/

# Line numbers

There is a second argument to `highlight` called `linenos` that is optional. Including the `linenos` argument will force the highlighted code to include line numbers. For instance, the following code block would include line numbers next to each line:

{% highlight text %}
{% raw %}{% highlight ruby linenos %}{% endraw %}
def foo
  puts 'foo'
end
{% raw %}{% endhighlight ruby %}{% endraw %}
{% endhighlight %}

Then, it will render as

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight ruby%}

# Using syntax highlighting on GitHub Pages

>You can have code snippets highlighted so that they are easier to read on your GitHub Pages site using Rouge, Jekyll's default syntax highlighter.

Rouge is Jekyll's default syntax highlighter and is compatible with the Pygments highlighter. If Pygments is set in your `_config.yml` file then your pages site will automatically build with Rouge as the default highlighter instead.

# Escape a liquid templating tag

Just wrap anything with `{% raw %}...{% endraw %}` and it won't be parsed by liquid renderer.

# Further reading

* [Code snippet highlighting - Jekyll docs](https://jekyllrb.com/docs/templates/#code-snippet-highlighting).
* [Using syntax highlighting on GitHub Pages - GitHub Help](https://help.github.com/articles/using-syntax-highlighting-on-github-pages/)
* [Creating and highlighting code blocks - GitHub Help](https://help.github.com/articles/creating-and-highlighting-code-blocks/)
* [Fixing highlighting errors - GitHub Help](https://help.github.com/articles/page-build-failed-config-file-error/#fixing-highlighting-errors)
