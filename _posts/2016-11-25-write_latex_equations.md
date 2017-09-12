---
layout: post
title:  "Write LaTeX Equations in Jekyll Using MathJax & Kramdown"
---

# What is MathJax

MathJax is a javascript library that uses the TeX algorithms and fonts to display math formulas on HTML pages. It allows for very fine-grained configuration, is widely used and works on all modern browsers.

This engine marks up math formulas with HTML `<script type="math/tex">` tags that MathJax understands. The only other thing to do is to include the MathJax library itself on the HTML page.

# Choose Markdown converter

Kramdown, a fast, pure-Ruby Markdown-superset converter, has built-in support for block and span-level mathematics written in $$\LaTeX$$. What's more, for Jekyll sites hosted on GitHub Pages, only the `kramdown` engine is supported.

If you are using other Markdown converter, like `redcarpet`, you need to change to `markdown: kramdown` in your `_config.yml` file.

Note that kramdown does **not** ship with the MathJax library and that therefore the “default” template does **not** include a link to it! we need to add a link to MathJax to our page.

# Implement MathJax with Jekyll

MathJax provides varies kinds of plugins for different websites and frameworks, like WordPress. Check [MathJax In Use](http://docs.mathjax.org/en/latest/misc/mathjax-in-use.html?highlight=kramdown#mathjax-in-use) and [Using MathJax in popular web platforms](http://docs.mathjax.org/en/latest/misc/platforms.html?highlight=jekyll#using-mathjax-in-popular-web-platforms) to learn more.

To get MathJax support, add the lines to your theme layouts:

```html
<!-- Mathjax Support -->
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

either just before the `</head>` tag in your theme file, or at the end of the file if it contains no `</head>`.

As for my site, you can find the above lines in `/_includes/head.html`.

**Note** that this will enable MathJax for your current theme/template **only**. If you change themes or update your theme, you will have to repeat these steps.

# Math syntax in Kramdown

**Note** that this syntax feature is not part of the original Markdown syntax.

The default math delimiters are `$$...$$` and `\[...\]` for displayed mathematics, and `\(...\)` for in-line mathematics.

**Note** in particular that the `$...$` in-line delimiters are **not** used by default. Since dollar signs appear too often in non-mathematical settings.

The following kramdown fragment:

```TeX
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$
```

will render as

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

**Note** that LaTeX code that uses the pipe symbol `|` in inline math statements may lead to a line being recognized as a table line. This problem can be avoided by using the `\vert` command instead of `|`

If you have a paragraph that looks like a math block but should actually be a paragraph with just an inline math statement, you need to escape the first dollar sign:

```
The following is a math block:$$ 5 + 5 $$

But next comes a paragraph with an inline math statement:\$$ 5 + 5 $$
```

will render as

The following is a math block:$$ 5 + 5 $$

But next comes a paragraph with an inline math statement:\$$ 5 + 5 $$

If you don’t even want the inline math statement, escape the first two dollar signs:


\$\$ 5 + 5 $$


# Further reading

* MathJax: [Home](https://www.mathjax.org) / [Using the MathJax Content Delivery Network (CDN)](http://docs.mathjax.org/en/latest/start.html#using-the-mathjax-content-delivery-network-cdn) / [Using MathJax in a Theme File](http://docs.mathjax.org/en/latest/misc/platforms.html?highlight=jekyll#using-mathjax-in-a-theme-file)
* Jekyll: [Math Support - Jekyll Doc](https://jekyllrb.com/docs/extras/#math-support)
* Kramdown: [Math Blocks](http://kramdown.gettalong.org/syntax.html#math-blocks) / [Math Support](http://kramdown.gettalong.org/converter/html.html#math-support) / [Math Engine MathJax](http://kramdown.gettalong.org/math_engine/mathjax.html)
* [Displaying Math in RSS feeds - Noam Ross](http://www.noamross.net/blog/2012/4/4/math-in-rss-feeds.html)
* [Using Jekyll and Mathjax - Dason Kurkiewicz](http://dasonk.github.io/blog/2012/10/09/Using-Jekyll-and-Mathjax.html)
* [MathJax with Jekyll - Gaston Sanchez](http://gastonsanchez.com/opinion/2014/02/16/Mathjax-with-jekyll/)
* [How to use MathJax in Jekyll generated Github pages - Haixing Hu](http://haixing-hu.github.io/programming/2013/09/20/how-to-use-mathjax-in-jekyll-generated-github-pages/)
* [在github pages上使用MathJax - Kung Hiu](http://www.anaharb.com/2014/0215/Jekyll-MathJax/)
* [MathJax with Kramdown - Toban Wiebe](http://tobanwiebe.com/blog/2016/02/mathjax-kramdown)
