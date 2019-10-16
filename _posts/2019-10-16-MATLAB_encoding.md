---
layout: post
title:  "将MATLAB的字符集编码更改为UTF-8"
date:   2019-10-16
author: 李宇琨
categories: MATLAB
tags: MATLAB
cover:  "https://pic3.zhimg.com/v2-3661bd8883f020e1560ba73d8064bf44_1200x500.jpg"
---

# 部署平台

* Windows 10 64-bit

* MATLAB R2019b (Version 9.7.0.1190202)


# 查看当前编码方式

在命令窗口输入命令：

```
feature('DefaultCharacterSet')
feature('locale')
```

或使用命令：

```
current = slCharacterEncoding()
```

返回当前 MATLAB 字符集编码。


# 修改字符集编码

如果要将编码方式更改为`UTF-8`编码，需要编辑MATLAB的locale数据库文件`lcdata.xml`。具体方法如下：

在MATLAB安装目录中找到`lcdata_utf8.xml`文件（其默认路径为`C:\Program Files\MATLAB\R2019b\bin`），并将其重命名为`lcdata.xml`。

在文件中删除

```
<encoding name="GBK">
    <encoding_alias name="936">
</encoding>
```

并将

```
<encoding name="UTF-8">
    <encoding_alias name="utf8"/>
</encoding>
```

修改为

```
<encoding name="UTF-8">
    <encoding_alias name="utf8"/>
    <encoding_alias name="GBK"/>
</encoding>
```

然后重启MATLAB即可。

Enjoy:)

# 延伸阅读

* [slCharacterEncoding - MathWorks](https://www.mathworks.com/help/simulink/slref/slcharacterencoding.html)
* [Matlab如何以UTF-8编码保存？ - 知乎](https://www.zhihu.com/question/27933621)
* [How do I get my MATLAB editor to read UTF-8 characters? UTF-8 characters in blank squares in editors, but in the command window and workspace works fine. - MATLAB Answers](https://www.mathworks.com/matlabcentral/answers/280988-how-do-i-get-my-matlab-editor-to-read-utf-8-characters-utf-8-characters-in-blank-squares-in-editors)
