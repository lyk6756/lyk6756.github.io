---
layout: post
title:  "在线文档部署方案：Sphinx + Read the Docs"
date:   2018-01-30
author: 李宇琨
categories: 
tags: 
cover:  "https://i.ytimg.com/vi/hLFYvtL_nZM/maxresdefault.jpg"
---


# 前言

[Sphinx](http://www.sphinx-doc.org/en/stable/)是一个基于Python的用于创建文档的工具。它最早是用来制作Python语言的帮助文档。具有以下特征：

* 输出格式：HTML(包括Windows HTML Help)，LaTeX(用于打印的PDF版本)，ePub，Texinfo, 手册页，纯文本；
* 强大的交叉引用：语义标记和对函数、类、引用、术语表和类似信息的自动链接功能；
* 层次结构：简单的文本树定义，并能自动链接同级、父级和子级；
* 自动索引：一般索引以及语言特定模块索引；
* 代码处理：利用[Pygments](http://pygments.org/)实现代码高亮；
* 开放的扩展：支持代码块的自动测试,并包含Python模块的自述文档(API docs)等。

Sphinx使用[reStructuredText](http://docutils.sourceforge.net/rst.html)作为标记语言，它的优势来自于reStructuredText语言的强大和直接，及其解析和翻译套件[Docutils](http://docutils.sourceforge.net/)。


# 安装和快速开始

对于已经安装有Python的系统，可以直接使用pip安装Sphinx：

```
pip install sphinx sphinx-autobuild
```

完成安装之后，可以在命令窗口输入`sphinx-build -h`来查看sphinx的版本号和该指令的其他控制参数。

关于不同平台下更详细的安装说明，可参考[Installing Sphinx](http://www.sphinx-doc.org/en/stable/install.html)。

在需要创建文档的目录下，直接在命令行中输入：

```
sphinx-quickstart
```

就会进入Sphinx的创建向导，通过回答一系列问题就能够创建一个Sphinx工程的空白模板（确保关于`autodoc`的选项设置为`yes`）。

在完成了向导配置之后，运行

```
make html
```

就可以生成html形式的文档了，虽然它还是空白的。

还可以使用`sphinx-autobuild`来自动重载文档。运行下面指令来实现：

```
sphinx-autobuild . _build/html
```


# 添加内容

如果要想快速开始使用Sphinx，可以参考[First Steps with Sphinx](http://www.sphinx-doc.org/en/stable/tutorial.html)或[Sphinx初尝](http://zh-sphinx-doc.readthedocs.io/en/latest/tutorial.html)。

更加详细的说明文档可参考[Sphinx documentation](http://www.sphinx-doc.org/en/stable/contents.html)或[Sphinx 使用手册](http://zh-sphinx-doc.readthedocs.io/en/latest/index.html)。

或者也可以参考这里：[使用sphinx记笔记](http://jwch.sdut.edu.cn/book/tool/UseSphinx.html)。

## 配置文档

使用`sphinx-quickstart`指令将生成包括`conf.py`在内的配置文件，以及一份主文档文件`index.rst`。

`conf.py`文件包含了该sphinx工程的所有配置选项，包括一些无法在`sphinx-quickstart`向导中进行设置的复杂选项。更加详细的`conf.py`配置内容可参考[The build configuration file](http://www.sphinx-doc.org/en/stable/config.html)。

## rST简介

[reStructuredText](http://docutils.sourceforge.net/rst.html)是一种易于阅读、所见即所得的纯文本标记语言。它非常利于快速创建简单的网页和独立的文档，尤其是程序的参考手册。reStructuredText是专门为了特定应用的扩展性而设计的，它的解析器是[Docutils](http://docutils.sourceforge.net/index.html)的一个组件。

这篇文章告诉了你为何不要使用Markdown进行文档写作：[Why You Shouldn’t Use "Markdown" for Documentation](http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/)，主要原因有以下几点：

> * Lack of a standard
> * Flavors
> * Lack of Extensibility
> * Lack of Semantic Meaning
> * Lock In and Lack of Portability

[reStructuredText](http://docutils.sourceforge.net/rst.html)为用户提供了快速入门指南和参考手册：

* 快速入门指南：[A ReStructuredText Primer](http://docutils.sourceforge.net/docs/user/rst/quickstart.html)
* 参考手册：[Quick reStructuredText](http://docutils.sourceforge.net/docs/user/rst/quickref.html)

更加详细的说明文档可参考[reStructuredText Primer](http://www.sphinx-doc.org/en/stable/rest.html)或[reStructuredText 简介](http://zh-sphinx-doc.readthedocs.io/en/latest/rest.html)。

或者也可以参考这里：[reStructuredText 简明教程](http://jwch.sdut.edu.cn/book/rst.html)


# 文档托管

[Read the Docs](https://readthedocs.org/)是一个基于Sphinx的在线文档托管系统，使得文档完全可搜索且易于查找。它从在线的Subversion、Bazaar、Git或Mercurial仓库获取到基于Sphinx创建的文档代码，生成文档并为用户托管。

Read the Docs是一个开源的项目，可以免费地在GitHub上获取到[项目源代码](http://github.com/rtfd/readthedocs.org)。

在完成文档的创作之后，只需将文档工程托管在GitHub上，并在[Read the Docs](https://readthedocs.org/)网站上创建账号导入GitHub中对应的工程，网站就能够自动帮助你进行编译和发布。

前往[Getting Started Guide](https://docs.readthedocs.io/en/latest/getting_started.html)来了解如何在readthedocs上进行文档托管。

同时，readthedocs在GitHub上也有为初学者准备的[演示代码](https://github.com/readthedocs/template)，供大家学习使用。


# 延伸阅读

* [Sphinx](http://www.sphinx-doc.org/en/stable/) / [Documentation](http://www.sphinx-doc.org/en/stable/contents.html) / [First Steps with Sphinx](http://www.sphinx-doc.org/en/stable/tutorial.html) / [reStructuredText Primer](http://www.sphinx-doc.org/en/stable/rest.html)
* [Sphinx 文档目录 — Sphinx 使用手册](http://zh-sphinx-doc.readthedocs.io/en/latest/contents.html) / [reStructuredText 简介](http://zh-sphinx-doc.readthedocs.io/en/latest/rest.html)
* [reStructuredText](http://docutils.sourceforge.net/rst.html)
* [Read the Docs](https://readthedocs.org/) / [Documentation](https://docs.readthedocs.io/en/latest/index.html) / [Getting Started Guide](https://docs.readthedocs.io/en/latest/getting_started.html)

* [写最好的文档:Sphinx + Read the Docs](https://avnpc.com/pages/writing-best-documentation-by-sphinx-github-readthedocs)
* [如何用 ReadtheDocs、Sphinx 快速搭建写书环境 - 简书](https://www.jianshu.com/p/78e9e1b8553a)
* [reStructuredText(rst)快速入门语法说明 - 简书](https://www.jianshu.com/p/1885d5570b37)
* [使用sphinx记笔记](http://jwch.sdut.edu.cn/book/tool/UseSphinx.html) / [reStructuredText 简明教程](http://jwch.sdut.edu.cn/book/rst.html)
* [A beginner’s guide to writing documentation](http://docs.writethedocs.org/guide/writing/beginners-guide-to-docs/)
* [Why You Shouldn’t Use “Markdown” for Documentation](http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/)
* [Lightweight Markup: Markdown, reStructuredText, MediaWiki, AsciiDoc, Org-mode - Hyperpolyglot](http://hyperpolyglot.org/lightweight-markup)
