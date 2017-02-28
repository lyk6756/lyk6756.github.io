---
layout: post
title:  "为Jekyll添加Google Analytics（分析）服务"
date:   2017-03-01
author: 李宇琨
categories: Jekyll
tags:	jekyll
cover:  "https://p3peqw-dm2305.files.1drv.com/y3mxpVytTtUi2cE_mU2XfHE7L2RDOVs7HqDLSbVhLaLgHClZZ_np5ZKKlOHiNE7MyDJpBtnkfVps7l4KLrRcYXRizN-Ec0GFJvDtzdvY6dg6E0w6pyjVtuitmTQfXK5vdhw5As2dCvBscRo0l-HQPYZXp9ztNuA8D1qjkljcjlSa-8?width=1280&height=720&cropmode=none"
---

<!-- TOC -->

- [什么是Google Analytics](#什么是google-analytics)
- [Analytics（分析）使用入门](#analytics分析使用入门)
- [设置Google Analytics（分析）跟踪](#设置google-analytics分析跟踪)
- [检查网络跟踪代码设置](#检查网络跟踪代码设置)
- [延伸阅读](#延伸阅读)

<!-- /TOC -->

# 什么是Google Analytics

[Google Analytics](https://www.google.com/analytics/)（谷歌分析，简称GA）是著名互联网公司Google提供的一款**免费**为网站提供的数据统计服务。可以对目标网站进行访问数据统计和分析，并提供多种参数供网站拥有者使用。

需要注意的是，你可能需要科学的上网方式才能够访问Google的相关网站。

# Analytics（分析）使用入门

访问[Get started with Analytics - Analytics Help](https://support.google.com/analytics/answer/1008015)来对Analytics（分析）的使用入门。它将指导你如何注册Analytics（分析）帐户并获得目标站点的跟踪ID（Tracking ID）以及相关的跟踪代码段。

# 设置Google Analytics（分析）跟踪

Google Analytics（分析）有多种数据收集方式，如何选择取决于跟踪对象是网站、应用还是其他联网设备。访问[Set up Analytics tracking - Analytics Help](https://support.google.com/analytics/answer/1008080)，根据您的跟踪对象选择最合适的安装方法。

由于由Jekyll生成的网站属于静态网站，因此必须获取Google Analytics（分析）跟踪代码，然后将其粘贴到要跟踪的每个网页的源代码中。

首先，在网站的`_includes`目录下创建你一个叫`google-analytics.html`的文件。然后将如下的跟踪代码段复制在文件中：

{% highlight javascript %}
{% raw %}
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', '{{ site.google_analytics }}', 'auto');
  ga('send', 'pageview');

</script>
{% endraw %}
{% endhighlight %}

然后，在`_config.yml`文件中添加如下代码，并将`TRACKING_ID`替换成你在上一步中得到的跟踪ID。

{% highlight yaml %}
google_analytics: TRACKING_ID
{% endhighlight yaml %}

接下来，需要将这些代码添加到我们的页面中去。在文件`_includes/head.html`中添加：

```html
{% raw %}{% if jekyll.environment == 'production' and site.google_analytics %}
{% include google-analytics.html %}
{% endif %}{% endraw %}
```

需要注意的是，这里我们添加了判断`if jekyll.environment == 'production'`。由于一般的Jekyll编译环境默认为`development`。这样一来，当我们在本地运行`jekyll serve`来测试我们的网址时，Google Analytics（分析）服务将不会在本地的页面中激活。这就避免了来自`localhost:4000`或是`127.0.0.1:4000`的访问混淆在正常的统计数据之中。

如果你需要在本地编译时启动Google Analytics（分析）服务，那么就需要将编译环境设置为`production`。在运行`jekyll build`时添加`JEKYLL_ENV=production`来激活：

```shell
$ JEKYLL_ENV=production jekyll build
```

# 检查网络跟踪代码设置

一旦你成功地启动了Google Analytics（分析）服务，它就将在24小时之后得到包括访问数，用户特征以及浏览信息在内的站点报告。访问[check your web tracking code setup immediately](https://support.google.com/analytics/answer/1008083)了解如何通过一些方法来检查网站中的 Analytics（分析）跟踪代码是否运行正常。

# 延伸阅读

* [Google Analytics Solutions](https://www.google.com/analytics/) / [Analytics Help](https://support.google.com/analytics)
* [Google Analytics setup for Jekyll - Michael Lee](https://michaelsoolee.com/google-analytics-jekyll/)
* [Google Analytics for Jekyll - Desired Persona](https://desiredpersona.com/google-analytics-jekyll/)
* [Adding Google analytics to Jekyll - Logical Solutions](https://spock.rocks/tech/2016/03/22/add-google-analytics-to-jekyll.html)
