---
layout: post
title:  "使用Jekyll在GitHub上搭建个人博客"
date:   2017-02-26
author: 李宇琨
categories: Jekyll
tags:	jekyll
cover:  "https://qnpeqw-dm2305.files.1drv.com/y3meKoP7pUDPSshru6OB2ZR5Zc3floxaUCVQg_Dt6DN2-2sAOO8rqFCp35_wNxpyYvvIs83sIyfWfeL6qdE7rFniM3uRgSIX0XIU2YP3R0HH_fQoXsqww7HlR4qwMhAWBkMzRsALGOVxVoe1SRi7q0L5lAbgVmCEb6ccHY4RiFDBNw?width=1800&height=1200&cropmode=none"
---

<!-- TOC -->

- [博客解决方案](#博客解决方案)
- [平台简介](#平台简介)
    - [为何选择GitHub Pages](#为何选择github-pages)
    - [什么是Jekyll](#什么是jekyll)
- [环境搭建](#环境搭建)
- [创建站点](#创建站点)
    - [更换主题](#更换主题)
- [撰写文章](#撰写文章)
    - [Markdown](#markdown)
    - [发布文章](#发布文章)
- [网站部署](#网站部署)
- [延伸阅读](#延伸阅读)

<!-- /TOC -->

# 博客解决方案

有各种各样的方法来创建你的个人博客网站。这里，我们不加比较地列举几种比较常见的博客平台以及开发框架：

平台：

* [Blogger.com - Create a unique and beautiful blog. It's easy and free.](https://www.blogger.com/)
* [Tumblr - Come for what you love. Stay for what you discover.](https://www.tumblr.com/)
* [GitHub Pages - Websites for you and your projects, hosted directly from your GitHub repository.](https://pages.github.com/)
* [LOFTER (乐乎) - 记录生活，发现同好](http://www.lofter.com/)
* [简书 - 交流故事，沟通想法](http://www.jianshu.com/)
* [博客园 - 开发者的网上家园](http://www.cnblogs.com/)

框架：

* [WordPress.com - Create a free website or blog](https://wordpress.com/)
* [Hexo - A fast, simple & powerful blog framework powered by Node.js.](https://hexo.io/)
* [Jekyll - Simple, blog-aware, static sites - Transform your plain text into static websites and blogs](https://jekyllrb.com/)
* [Django - The Web framework for perfectionists with deadlines](https://www.djangoproject.com/)

这里我们使用Jekyll来生成我们的网站，并将其部署在GitHub Pages上。之后就可以使用轻量级的标记语言Markdown来进行创作。

# 平台简介

## 为何选择GitHub Pages

[GitHub](https://github.com/)是一个著名的项目托管平台，其利用Git进行代码版本管理。目前有无数的优秀开源项目托管在GitHub上供人们学习使用。只要保证代码的开源性，你就可以免费享受GitHub提供的服务，这被看做是互联网精神的象征。

[GitHub Pages](https://pages.github.com/)是GitHub提供的一个网站托管部署解决方案。 相比于其他的建站方法，它不需要另外租用网络服务器，也不需要和数据库打交道，甚至不需要对HTML了解得太多。GitHub Pages提供的向导将帮助你得到用来发布的网页。而你需要做的，只是将这些代码放在一个新的仓库（repository）里而已，就像管理你在GitHub上的其他项目一样。一切就是这么简单。而且，它依然是**免费**的。

在GitHub Pages的[官方网站](https://pages.github.com/)上，你能够看到*What is GitHub Pages?*主题的介绍视频（YouTube源），并一步一步地教你如何在GitHub上创建自己的第一个网页来向世界问好。

## 什么是Jekyll

除了简单的HTML页面，GitHub Pages还提供了一个简单的博客形态的静态网站生成器——[Jekyll](https://jekyllrb.com/)。Jekyll有一个相对确定的模板，利用渲染器[Liquid](https://github.com/Shopify/liquid/wiki)来生成最终的静态网站。它能够识别Markdown语句，Liquid标签以及原始的HTML和CSS。

由于GitHub Pages默认支持Jekyll框架，因此我们就可以轻松地将Jekyll生成的代码直接上传到GitHub上来搭建我们的博客网站，而且是**完全免费**的。

请访问[Jekyll docs](https://jekyllrb.com/docs/home/)，它将详细地告诉你如何搭建和运行你的网站，创建以及管理内容，定制网站的展示和外观，以及在不同的平台上部署你的网站。

如果你不得不承认英文阅读对于你来说是一件巨大的难事，这里还有[Jekyllcn中文站](http://jekyllcn.com/)来将你解脱苦海。

# 环境搭建

想要使用Jekyll，你就必须在本地安装Jekyll。

Jekyll是用Ruby语言开发的，所以最简单的安装方式就是使用RubyGems（RubyGems简称gems，是一个用于对Ruby组件进行打包的Ruby打包系统）。

如果你的电脑中已经安装了最新版本的RubyGems，在终端中运行如下命令就可以安装了：

```shell
$ gem install jekyll
```

由于大部分网页模板中都需要安装其他的插件，Bundler就显得很有必要了。它将帮助你打包管理这些插件。因此安装命令变为：

```shell
$ gem install jekyll bundler
```

如果你的电脑里缺少Ruby和RubyGems，请参考[Download Ruby](http://www.ruby-lang.org/en/downloads/)和[Download RubyGems](https://rubygems.org/pages/download)来获取相应帮助。

需要指出的是，官方**不推荐**在MS Windows操作系统上安装。除此以外，Mac用户还需要安装Xcode和Command-Line Tools。

更详细的安装说明请移步[Jekyll docs: Installation](https://jekyllrb.com/docs/installation/)。

# 创建站点

有了Jekyll，只需要短短的几行指令就可以得到一个简洁的博客页面：

```shell
~ $ gem install jekyll bundler
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle exec jekyll serve
```

然后打开浏览器访问http://localhost:4000，就能立刻看到效果。

这里是一些常用的Jekyll指令：

```shell
$ jekyll build
# => The current folder will be generated into ./_site

$ jekyll build --destination <destination>
# => The current folder will be generated into <destination>

$ jekyll build --source <source> --destination <destination>
# => The <source> folder will be generated into <destination>

$ jekyll build --watch
# => The current folder will be generated into ./_site,
#    watched for changes, and regenerated automatically.

$ jekyll serve
# => A development server will run at http://localhost:4000/
# Auto-regeneration: enabled. Use `--no-watch` to disable.

$ jekyll serve --detach
# => Same as `jekyll serve` but will detach from the current terminal.
#    If you need to kill the server, you can `kill -9 1234` where "1234" is the PID.
#    If you cannot find the PID, then do, `ps aux | grep jekyll` and kill the instance.

$ jekyll serve --no-watch
# => Same as `jekyll serve` but will not watch for changes.
```

## 更换主题

除了使用默认生成的模板外，你还可以使用网络上人们分享的各种主题。你只需根据主题中的说明文档进行相应设置，即可得到美丽酷炫的页面。

这里是几个提供下载服务的Jekyll主题网站：

* [Jekyll Themes](http://jekyllthemes.org/)
* [Jekyll Themes](http://themes.jekyllrc.org/)
* [Jekyll Themes & Templates](https://jekyllthemes.io/)
* [Themes · jekyll/jekyll Wiki · GitHub](https://github.com/jekyll/jekyll/wiki/Themes)

除此之外，[Sites · jekyll/jekyll Wiki · GitHub](https://github.com/jekyll/jekyll/wiki/sites)页面列举了许多使用Jekyll发布在GitHub的网站。你可以直接去他们的仓库中派生（fork）到自己的账号下进行修改。

更详细的主题配置说明请移步[Jekyll docs: Themes](https://jekyllrb.com/docs/themes/)。

# 撰写文章

终于，你可以写一些属于自己的东西了！Jekyll的核心其实是一个文本转换引擎，它能够识别多种标记语言：Markdown，Textile，或者就是原始的HTML。目前最受欢迎的，就当属Markdown了。

## Markdown

Markdown（[项目主页](http://daringfireball.net/projects/markdown/)）是由John Gruber发明的一种轻量化文本标记语言，广泛地被互联网内容创作者们所使用。它允许人们使用易读易写的纯文本格式编写文档，然后转换成有效的XHTML(或者HTML)文档（[Markdown - 维基百科](https://zh.wikipedia.org/zh-hans/Markdown)）。关于Markdown语法的快速入门可以参考：

* [Markdown 语法说明(简体中文版)](http://www.appinn.com/markdown/)
* [认识与入门 Markdown - 少数派](http://sspai.com/25137/)
* [Markdown——入门指南 - 简书](http://www.jianshu.com/p/1e402922ee32/)
* [献给写作者的Markdown 新手指南 - 简书](http://www.jianshu.com/p/q81RER)

Jekyll默认使用[kramdown](http://kramdown.gettalong.org/index.html)来对Markdown语法进行解释。另外，在[kramdown Syntax](https://kramdown.gettalong.org/syntax.html)页面上还能够看到kramdown在Markdown语法基础上衍生出的更加丰富的语法功能，诸如数学公式，复杂表格等。使用[Online Kramdown Editor](http://kramdown.herokuapp.com/)你就能直接在网页上方便地编辑你的文章了。

当然，如果你想用Markdown来代替LaTeX写论文、出幻灯片的话，可以关注MS Research开源的[Madoko](https://www.madoko.net/)项目。简单的了解可以查看[用Markdown 写作用什么文本编辑器? - 王铭烨 Arthur2e5 的回答 - 知乎](https://www.zhihu.com/question/19637157/answer/78063239)。

##  发布文章

Jeklly 的一个最好的特点是让作者**关注blog本身**。这是指什么呢？简单的说就是写博客的过程被融入了Jekyll的功能中。你只需简单的管理你电脑中的一个文件夹下的文本文件就可以写文章并方便的在线上发布。

一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```

更详细的目录结构说明请移步[Jekyll docs: Directory structure](http://jekyllrb.com/docs/structure/)。

其中，`_posts`目录里放的就是你的文章了。文件格式很重要，必须要符合: YEAR-MONTH-DAY-title.MARKUP。永久链接可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。

只需要将新的文章放在目录_posts下，并将文件名改为YYYY-MM-DD-name-of-post.md。你可参考本文的源文件来撰写你自己的博文。将头信息中的内容更改为你需要的，并在之后附上你自己的内容即可。

更详细的文章撰写说明请移步[Jekyll docs: Front Matter](http://jekyllrb.com/docs/frontmatter/)以及[Jekyll docs: Writing posts](http://jekyllrb.com/docs/posts/)。

# 网站部署

当你的网站在本地编译测试之后，就可以将其部署在GitHub Pages正式上线了！

如果你已经是GitHub的用户了，接下来你将轻车熟路。你只需要按照格式创建一个新的仓库：`ghname.github.io`，其中`ghname`指代你的GitHub账号名称。然后，将你本地的网站上传到这个仓库中就可以通过连接https://ghname.github.io 来访问你的网站了。

如果你的电脑已经安装并配置了git，那么就可以在终端中直接上传了。

{% highlight shell %}
$ git init
$ git clone http://github.com/ghname/ghname.github.io.git

$ git pull origin master

$ git add --all
$ git commit -m "leave a message"
$ git push origin master
{% endhighlight shell %}

更详细的部署说明请移步[Jekyll docs: GitHub Pages](https://jekyllrb.com/docs/github-pages/)。

# 延伸阅读

* GitHub Pages: [GitHub Pages](https://pages.github.com/) / [Pages Help](https://help.github.com/categories/github-pages-basics/) / [Dependency versions](https://pages.github.com/versions/)
* Jekyll: [Home](https://jekyllrb.com/) / [jekyllcn](http://jekyllcn.com/) / [wiki at GitHub](https://github.com/jekyll/jekyll/wiki) / [Liquid renderer](https://shopify.github.io/liquid/) / [wiki at GitHub](https://github.com/Shopify/liquid/wiki)
* Markdown: [Home](http://daringfireball.net/projects/markdown/) / [Kramdown](http://kramdown.gettalong.org/index.html) / [Online Kramdown Editor](http://kramdown.herokuapp.com/) / [Madoko IDE](https://www.madoko.net/)
