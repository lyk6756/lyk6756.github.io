---
layout: post
title:  "Build a Blog on GitHub Pages Using Jekyll"
---

# Choose your solution

There are varies ways to creat your personal website.
Without comparing their pros and cons, here lists some popular platforms and frameworks that people use widely:

Platforms:

* [Blogger.com - Create a unique and beautiful blog. It's easy and free.](https://www.blogger.com/)
* [Tumblr - Come for what you love. Stay for what you discover.](https://www.tumblr.com/)
* [GitHub Pages - Websites for you and your projects, hosted directly from your GitHub repository.](https://pages.github.com/)
* [LOFTER (乐乎) - 记录生活，发现同好](http://www.lofter.com/)
* [简书 - 交流故事，沟通想法](http://www.jianshu.com/)
* [博客园 - 开发者的网上家园](http://www.cnblogs.com/)

Frameworks:

* [WordPress.com - Create a free website or blog](https://wordpress.com/)
* [Hexo - A fast, simple & powerful blog framework powered by Node.js.](https://hexo.io/)
* [Jekyll - Simple, blog-aware, static sites - Transform your plain text into static websites and blogs](https://jekyllrb.com/)
* [Django - The Web framework for perfectionists with deadlines](https://www.djangoproject.com/)

In this article I will show how to use jekyll generating webpages, and use GitHub Pages to host sites.

# Introduction

## Why GitHub Pages

[GitHub](https://github.com/) is an online project hosting platform using Git. More than 11 million people use GitHub to discover, fork, and contribute to over 29 million projects. GitHub offers both plans for private and free repositories on the same account which are commonly used to host open-source software projects.

[GitHub Pages](https://pages.github.com/) is a static site hosting service provided by GitHub.GitHub Pages is designed to host your personal, organization, or project pages directly from a GitHub repository. Compared with other services, you don't need to rent a server, or deal with databases, even know a lot about HTML. [Pages Help](https://help.github.com/categories/github-pages-basics/) offers wizzard guiding you publish your pages. All you need to do is to put these codes into a new repository, just like managing your other projects on GitHub. Most important, all these services are **free**.

On the [homepage](https://pages.github.com/) of GitHub Pages, there is video *What is GitHub Pages?* introducing GitHub Pages. And teach you how to build a hello-world page step by step. 

## What is Jekyll

Apart from simple HTML pages, GitHub Pages also provides a simple, blog-aware, static site generator: [Jekyll](https://jekyllrb.com/). It takes a template directory containing raw text files in various formats, runs it through a converter (like [Markdown](https://daringfireball.net/projects/markdown/)) and our [Liquid](https://github.com/Shopify/liquid/wiki) renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server.

Since Jekyll is the default engine behind GitHub Pages,we can use Jekyll to host your project’s page, blog, or website from GitHub’s servers **for free**.

Visit [Jekyll docs](https://jekyllrb.com/docs/home/), which covers topics such as getting your site up and running, creating and managing your content, customizing the way your site works and looks and deploying to various environments.

# Establishing development environment

You need to install Jekyll locally if you want to use it.

Jekyll is developed with [Ruby](http://www.ruby-lang.org/en/downloads/). The best way to install Jekyll is via [RubyGems](https://rubygems.org/pages/download). At the terminal prompt, simply run the following command to install Jekyll:

```shell
$ gem install jekyll
```

Since most themes need other gems supported, Bundler gems becomes necessary. The command becomes:

```shell
$ gem install jekyll bundler
```

It should be noted that MS Windows is not an officially-supported platform. What's more, you will need to install Xcode and the Command-Line Tools if you are using macOS.

Visit [Jekyll docs: Installation](https://jekyllrb.com/docs/installation/) to learn more.

# Creating sites

With Jekyll,you can create a new site by doing the following:

```shell
~ $ gem install jekyll bundler
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle exec jekyll serve
```

And then visit http://localhost:4000 to see your awesome site.

The Jekyll gem makes a `jekyll` executable available to you in your Terminal window. You can use this command in a number of ways:

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

## Use a theme

By default, the Jekyll site installed by jekyll new uses a gem-based theme called [Minima](https://github.com/jekyll/minima). Apart from this, you can also download themes shared on the Internet. Here lists some popular platforms sharing Jekyll themes:

* [Jekyll Themes](http://jekyllthemes.org/)
* [Jekyll Themes](http://themes.jekyllrc.org/)
* [Jekyll Themes & Templates](https://jekyllthemes.io/)
* [Themes · jekyll/jekyll Wiki · GitHub](https://github.com/jekyll/jekyll/wiki/Themes)

What's more, you can also directly fork others' pretty sites hosting on GitHub. [Sites · jekyll/jekyll Wiki · GitHub](https://github.com/jekyll/jekyll/wiki/sites) lists lots of blogs made with Jekyll hosting on GitHub.

Visit [Jekyll docs: Themes](https://jekyllrb.com/docs/themes/) to learn more.

# Writing posts

Finally, you can write something belong to you. Jekyll is, at its core, a text transformation engine. The concept behind the system is this: you give it text written in your favorite markup language, be that Markdown, Textile, or just plain HTML, and it churns that through a layout or a series of layout files.

## Markdown

[Markdown](http://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax designed so that it can be converted to HTML and many other formats using a tool by the same name. Markdown is often used to format readme files, for writing messages in online discussion forums, and to create rich text using a plain text editor. Here are some quick start on Markdown syntax:

* [Markdown 语法说明(简体中文版)](http://www.appinn.com/markdown/)
* [认识与入门 Markdown - 少数派](http://sspai.com/25137/)
* [Markdown——入门指南 - 简书](http://www.jianshu.com/p/1e402922ee32/)
* [献给写作者的Markdown 新手指南 - 简书](http://www.jianshu.com/p/q81RER)

[kramdown](http://kramdown.gettalong.org/index.html), a fast, pure-Ruby Markdown-superset converter, is Jekyll's default Markdown language converter. What's more, you can also find some advance functions that is not included in the original Markdown on [kramdown Syntax](https://kramdown.gettalong.org/syntax.html), such as math equations, complex tables. Using [Online Kramdown Editor](http://kramdown.herokuapp.com/), you can directly edit your article on a webpage.

If you are interested in writing papers or slides using markdown, you can follow [Madoko](https://www.madoko.net/) project which is provided by MS Research.

## Publish posts

One of Jekyll’s best aspects is that it is "blog aware". What does this mean, exactly? Well, simply put, it means that blogging is baked into Jekyll’s functionality. If you write articles and publish them online, you can publish and maintain a blog simply by managing a folder of text-files on your computer.

A basic Jekyll site usually looks something like this:

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

Visit [Jekyll docs: Directory structure](http://jekyllrb.com/docs/structure/) to learn more.

Directory `_posts` is your dynamic content, so to speak. The naming convention of these files is important, and must follow the format: `YEAR-MONTH-DAY-title.MARKUP`. The permalinks can be customized for each post, but the date and markup language are determined solely by the file name. 

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Visit [Jekyll docs: Front Matter](http://jekyllrb.com/docs/frontmatter/) and [Jekyll docs: Writing posts](http://jekyllrb.com/docs/posts/) to learn more.

# Deploying on GitHub Pages

If you have already tested your sites locally, you can upload your code to GitHub now!

If you are a user of GitHub, it will be quite easy for the next few steps. Just add a new repository with name `ghname.github.io`, where `ghname` is the ID of your GitHub account. Then put your site's code into this repository. And voila! Your site will be automatically built. You can visit it following the link https://ghname.github.io.

{% highlight shell %}
$ git init
$ git clone http://github.com/ghname/ghname.github.io.git

$ git pull origin master

$ git add --all
$ git commit -m "leave a message"
$ git push origin master
{% endhighlight shell %}

Visit [Jekyll docs: GitHub Pages](https://jekyllrb.com/docs/github-pages/) to learn more.

# Further reading

* GitHub Pages: [GitHub Pages](https://pages.github.com/) / [Pages Help](https://help.github.com/categories/github-pages-basics/) / [Dependency versions](https://pages.github.com/versions/)
* Jekyll: [Home](https://jekyllrb.com/) / [jekyllcn](http://jekyllcn.com/) / [wiki at GitHub](https://github.com/jekyll/jekyll/wiki) / [Liquid renderer](https://shopify.github.io/liquid/) / [wiki at GitHub](https://github.com/Shopify/liquid/wiki)
* Markdown: [Home](http://daringfireball.net/projects/markdown/) / [Kramdown](http://kramdown.gettalong.org/index.html) / [Online Kramdown Editor](http://kramdown.herokuapp.com/) / [Madoko IDE](https://www.madoko.net/)
