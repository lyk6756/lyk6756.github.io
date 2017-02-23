---
layout: post
title:  "欢迎使用Jekyll！"
date:   2015-04-18 08:43:59
author: Ben Centra
categories: Jekyll
tags:	jekyll
cover:  "/assets/instacode.png"
---

> 本文由李宇琨翻译自Ben Centra为主题centrarium撰写的欢迎文章[Welcome to Jekyll!](https://bencentra.com/centrarium/jekyll/2015/04/18/welcome-to-jekyll.html)

你将在目录`_posts`下找到本文的原稿。尝试着编辑本文后重新编译来查看你的修改。虽然有很多种编译本网页的方法，但最常见的方法就是运行`jekyll serve`。这会启动jekyll网络服务器来自动生成你的网站。

## 添加新博文

只需要将新的文章放在目录`_posts`下，并将文件名改为`YYYY-MM-DD-name-of-post.ext`即可。你可参考本文的源文件来撰写你自己的博文。

### 标签和分类

如果你在博文的头信息中添加了若干分类或是标签，它们就会以链接的形式出现在文章页面的底部。通过点击这些链接，你将会得到有关此分类或是标签的目录页面。此功能是利用[jekyll-archive][jekyll-archive]gem实现的。

### 封面图片

如果想要更改文章的封面，只需在头信息中的"cover"属性中添加相关图片的URL即可(例如： <code>cover: "/assets/cover_image.jpg"</code>)。

### 代码段

你可以利用[highlight.js][highlight]来添加高亮代码段：

使用[Liquid][liquid] `{% raw %}{% highlight <language> %}{% endraw %}` 标记来为代码段添加语法高亮。

例如，此模板...
{% highlight html %}
{% raw %}{% highlight javascript %}    
function demo(string, times) {    
  for (var i = 0; i < times; i++) {    
    console.log(string);    
  }    
}    
demo("hello, world!", 10);
{% endhighlight %}{% endraw %}
{% endhighlight %}

...将产生如下效果：

{% highlight javascript %}
function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);
{% endhighlight %}

语法高亮是由[highlight.js][highlight]实现的。你可以在`head.html`文件中进行修改。

### 图片

图片可添加Lightbox功能。想要启用此效果，用<code>&lt;a&gt;</code>标记包括住图片标记<code>&lt;img&gt;</code>，同时在<code>&lt;a&gt;</code>中添加<code>data-lightbox</code>和<code>data-title</code>。得到的结果为：

<a href="//bencentra.com/assets/images/falcon9_large.jpg" data-lightbox="falcon9-large" data-title="Check out the Falcon 9 from SpaceX">
  <img src="//bencentra.com/assets/images/falcon9_small.jpg" title="Check out the Falcon 9 from SpaceX">
</a>

请参考[Lightbox][lightbox]网站以获取更多信息。

[jekyll]:      http://jekyllrb.com
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
[liquid]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
