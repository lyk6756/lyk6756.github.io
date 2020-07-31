---
layout: article
titles:
  # @start locale config
  en      : &EN       Typography
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
  zh-Hans : &ZH_HANS  版式
  zh      : *ZH_HANS
  zh-CN   : *ZH_HANS
  zh-SG   : *ZH_HANS
  zh-Hant : &ZH_HANT  版式
  zh-TW   : *ZH_HANT
  zh-HK   : *ZH_HANT
  ko      : &KO       체재
  ko-KR   : *KO
  fr      : &FR       Typographie
  fr-BE   : *FR
  fr-CA   : *FR
  fr-CH   : *FR
  fr-FR   : *FR
  fr-LU   : *FR
  # @end locale config
key: page-typography
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "/assets/images/header_image.jpg"
aside:
  toc: true
---

- [h1. Headings](#h1-headings)
  - [h2. Heading](#h2-heading)
    - [h3. Heading](#h3-heading)
      - [h4. Heading](#h4-heading)
        - [h5. Heading](#h5-heading)
          - [h6. Heading](#h6-heading)
- [H1. TeXt Heading](#h1-text-heading)
  - [H2. TeXt Heading](#h2-text-heading)
- [Lists](#lists)
  - [Unordered list](#unordered-list)
  - [Ordered list](#ordered-list)
  - [Task list](#task-list)
- [Tables](#tables)
  - [Align](#align)
  - [Table With Images](#table-with-images)
  - [Table With Long Text](#table-with-long-text)
- [Code Blocks](#code-blocks)
  - [Code Spans](#code-spans)
  - [Standard Code Blocks](#standard-code-blocks)
  - [Highlighting Code Snippets](#highlighting-code-snippets)
    - [Line Numbers](#line-numbers)
  - [Fenced Code Blocks](#fenced-code-blocks)
- [Images](#images)
  - [With ALT](#with-alt)
  - [With Title](#with-title)
  - [Specify Width and Height](#specify-width-and-height)
- [Links](#links)
  - [With Title](#with-title-1)
  - [Reference Links](#reference-links)
  - [Link Within A Paragraph](#link-within-a-paragraph)
- [Horizontal Rules](#horizontal-rules)
- [Footnote](#footnote)
- [Definition](#definition)
- [Blockquotes](#blockquotes)
- [Emphasis](#emphasis)
- [MathJax](#mathjax)
- [Extensions](#extensions)
  - [Audio](#audio)
    - [SoundCloud](#soundcloud)
    - [Netease Cloud Music (网易云音乐)](#netease-cloud-music-网易云音乐)
  - [Video](#video)
    - [YouTube](#youtube)
    - [TED](#ted)
    - [bilibili (哔哩哔哩)](#bilibili-哔哩哔哩)
  - [Slide](#slide)
    - [SlideShare](#slideshare)
  - [Demos](#demos)
    - [CodePen](#codepen)
- [Additional Styles](#additional-styles)
  - [Alert](#alert)
  - [Tag](#tag)
  - [Image](#image)
    - [Mixture](#mixture)
  - [Extra](#extra)

# h1. Headings

## h2. Heading

### h3. Heading

#### h4. Heading

##### h5. Heading

###### h6. Heading

**markdown:**

    # H1. TeXt Heading
    ## H2. TeXt Heading
    ### H3. TeXt Heading
    #### H4. TeXt Heading
    ##### H5. TeXt Heading
    ###### H6. TeXt Heading

H1. TeXt Heading
==================

H2. TeXt Heading
------

**markdown:**

    H1. TeXt Heading
    ==================

    H2. TeXt Heading
    ------

# Lists

## Unordered list

* Aenean
* vel
    * libero
    * eget
* ante

**markdown:**

    * Aenean
    * vel
        * libero
        * eget
    * ante

## Ordered list

1. Aenean
2. vel
3. libero
4. eget
5. ante

**markdown:**

    1. Aenean
    2. vel
    3. libero
    4. eget
    5. ante

## Task list

- [ ] a bigger project
  - [x] first subtask
  - [x] follow up subtask
  - [ ] final subtask
- [ ] a separate task

# Tables

## Align

|-----------------+------------+-----------------+----------------|
| Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    |
| Second line     |foo         | **strong**      | baz            |
| Third line      |quux        | baz             | bar            |
|-----------------+------------+-----------------+----------------|
| Second body     |            |                 |                |
| 2 line          |            |                 |                |
|=================+============+=================+================|
| Footer row      |            |                 |                |
|-----------------+------------+-----------------+----------------|

**markdown:**

    |-----------------+------------+-----------------+----------------|
    | Default aligned |Left aligned| Center aligned  | Right aligned  |
    |-----------------|:-----------|:---------------:|---------------:|
    | First body part |Second cell | Third cell      | fourth cell    |
    | Second line     |foo         | **strong**      | baz            |
    | Third line      |quux        | baz             | bar            |
    |-----------------+------------+-----------------+----------------|
    | Second body     |            |                 |                |
    | 2 line          |            |                 |                |
    |=================+============+=================+================|
    | Footer row      |            |                 |                |
    |-----------------+------------+-----------------+----------------|

---

|---
| Default aligned | Left aligned | Center aligned | Right aligned
|-|:-|:-:|-:
| First body part | Second cell | Third cell | fourth cell
| Second line |foo | **strong** | baz
| Third line |quux | baz | bar
|---
| Second body
| 2 line
|===
| Footer row

**markdown:**

    |---
    | Default aligned | Left aligned | Center aligned | Right aligned
    |-|:-|:-:|-:
    | First body part | Second cell | Third cell | fourth cell
    | Second line |foo | **strong** | baz
    | Third line |quux | baz | bar
    |---
    | Second body
    | 2 line
    |===
    | Footer row

## Table With Images

| Model | iPhone 6S | iPhone 6S Plus | iPhone SE | iPhone 7 | iPhone 7 Plus | iPhone 8 | iPhone 8 Plus | iPhone X |
| ----- | --------- | -------------- | --------- | -------- | ------------- | -------- | ------------- | -------- |
| Picture | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9b/IPhone_6s_vector.svg/210px-IPhone_6s_vector.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/IPhone_6s_Plus_vector.svg/250px-IPhone_6s_Plus_vector.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/IPhone_SE_in_silver.png/190px-IPhone_SE_in_silver.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/IPhone_7_Jet_Black.svg/210px-IPhone_7_Jet_Black.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/IPhone_7_Plus_Jet_Black.svg/250px-IPhone_7_Plus_Jet_Black.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/IPhone_8_vector.svg/210px-IPhone_8_vector.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/IPhone_8_plus_vector.svg/250px-IPhone_8_plus_vector.svg.png) | ![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/IPhone_X_vector.svg/220px-IPhone_X_vector.svg.png) |
| Initial release operating system | iOS 9.0 | iOS 9.0 | iOS 9.3 | iOS 10.0 | iOS 10.0 | iOS 11.0 | iOS 11.0 | iOS 11.0.1 |
| Display  | 4.7 in (120 mm), 4.1 in (100 mm) by 2.3 in (58 mm), 16:9 aspect ratio, aluminosilicate glass covered 16,777,216-color (24-bit), IPS LCD screen, 1,334 × 750 px screen resolution at 326 ppi, 1400:1 contrast ratio, 500 ​cd⁄m² max brightness, LED backlight and fingerprint-resistant oleophobic coating | 5.5 in (140 mm), 4.8 in (120 mm) by 2.7 in (69 mm), 16:9 aspect ratio, aluminosilicate glass covered 16,777,216-color (24-bit), IPS LCD screen, 1,920 × 1,080 px (Full HD) screen resolution at 401 ppi, 1300:1 contrast ratio, 500 ​cd⁄m² max brightness, LED backlight and fingerprint-resistant oleophobic coating | 4 in (100 mm), 3.5 in (89 mm) by 1.9 in (48 mm), 71:40 (~16:9) aspect ratio, aluminosilicate glass covered 16,777,216-color (24-bit), IPS LCD screen, 1,136 × 640 px (WSVGA) screen resolution at 326 ppi, pixel size 78 µm, 800:1 contrast ratio, 500 ​cd⁄m² max brightness, LED backlight and fingerprint-resistant oleophobic coating | In addition to 6S: 625 ​cd⁄m² max brightness | In addition to 6S Plus: 625 ​cd⁄m² max brightness | In addition to 7: True Tone display | In addition to 7 Plus: True Tone display | 5.8 in (150 mm), 5.31 in (135 mm) by 2.45 in (62 mm), ~19.5:9 aspect ratio, aluminosilicate glass covered 16,777,216-color (24-bit), AMOLED screen, 2,436 × 1,125 px screen resolution at 458 ppi, 1,000,000:1 contrast ratio, 625 ​cd⁄m² max brightness, fingerprint-resistant oleophobic coating, True Tone display, Dolby Vision and HDR10 support |

> From Wikipedia, the free encyclopedia

## Table With Long Text

| Language | Demo |
| -------- | ---- |
| C | printf("hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!"); |
| C++ | std::cout<<"hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!"<<std::endl; |
| Java | System.out.println("hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!"); |
| JavaScript | console.log('hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!hello,world!'); |

# Code Blocks

## Code Spans

Use `<html>` tags for this.

Here is a literal `` ` `` backtick.
And here is ``  `some`  `` text (note the two spaces so that one is left
in the output!).

```javascript
(() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
```

**markdown:**

    Here is a literal `` ` `` backtick.
    And here is ``  `some`  `` text (note the two spaces so that one is left
    in the output!).

## Standard Code Blocks

    Here comes some code

    This text belongs to the same code block.

^
    This one is separate.

**markdown:**

```
    Here comes some code

    This text belongs to the same code block.

^
    This one is separate.
```

---

```
(() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
```

**markdown:**

    ```
    (() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
    ```

---

```javascript
(() => console.log('hello, world!'))();
```

**markdown:**

    ```javascript
    (() => console.log('hello, world!'))();
    ```

---

```none
(() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
```

## Highlighting Code Snippets

{% highlight javascript %}
(() => console.log('hello, world!'))();
{% endhighlight %}

**markdown:**

```
{%- raw -%}
{% highlight javascript %}
(() => console.log('hello, world!'))();
{% endhighlight %}
{% endraw %}
```

### Line Numbers

{% highlight javascript linenos %}
var hello = 'hello';
var world = 'world';
var space = ' ';
(() => console.log(hello + space + world + space + hello + space + world + space + hello + space + world + space + hello + space + world))();
{% endhighlight %}

**markdown:**

```
{%- raw -%}
{% highlight javascript linenos %}
var hello = 'hello';
var world = 'world';
var space = ' ';
(() => console.log(hello + space + world + space + hello + space + world + space + hello + space + world + space + hello + space + world))();
{% endhighlight %}
{% endraw %}
```

---

{% highlight javascript %}
(() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
{% endhighlight %}

{% highlight none %}
(() => console.log('hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world! hello, world!'))();
{% endhighlight %}

## Fenced Code Blocks

~~~
Here comes some code.
~~~

**markdown:**

    ~~~
    Here comes some code.
    ~~~

---

# Images

![](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg)

An :apple: a day, keeps :woman_health_worker: :man_health_worker: away.

**markdown:**

    ![](path-to-image)

## With ALT

![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg)

**markdown:**

    ![Image](path-to-image)

## With Title

![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image")

**markdown:**

    ![Image](path-to-image "Image")

## Specify Width and Height

![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image@128x128"){:width="128px" height="128px"}

**markdown:**

    ![Image](path-to-image){:width="128px" height="128px"}

---

![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image@64x64"){:width="64px" height="64px"}

**markdown:**

    ![Image](path-to-image){:width="64px" height="64px"}

# Links

[TeXt](https://github.com/kitian616/jekyll-TeXt-theme/)

**markdown:**

    [TeXt](https://github.com/kitian616/jekyll-TeXt-theme/)

## With Title

[TeXt](https://github.com/kitian616/jekyll-TeXt-theme/ "TeXt")

**markdown:**

    [TeXt](https://github.com/kitian616/jekyll-TeXt-theme/ "TeXt")

## Reference Links

[TeXt][TeXt] is a super customizable Jekyll theme.

[TeXt]: https://github.com/kitian616/jekyll-TeXt-theme/ "TeXt"

**markdown:**

    [TeXt][TeXt] is a super customizable Jekyll theme.

    [TeXt]: https://github.com/kitian616/jekyll-TeXt-theme/ "TeXt"

## Link Within A Paragraph

[TeXt](https://github.com/kitian616/jekyll-TeXt-theme/) is a super customizable Jekyll theme for personal site, team site, blog, project, documentation, etc. Similar to iOS 11 style, it has large and prominent titles, round buttons and cards.

**markdown:**

    [TeXt](https://github.com/kitian616/jekyll-TeXt-theme/) is a super customizable Jekyll theme for personal site, team site, blog, project, documentation, etc. Similar to iOS 11 style, it has large and prominent titles, round buttons and cards.

# Horizontal Rules

* * *

    * * *

***

    ***

*****

    *****

- - -

    - - -

---------------------------------------

    ---------------------------------------

# Footnote

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here’s one with multiple blocks.

    Subsequent paragraphs are indented to show that they
belong to the previous footnote.

**markdown:**

    Here is a footnote reference,[^1] and another.[^longnote]

    [^1]: Here is the footnote.

    [^longnote]: Here’s one with multiple blocks.

        Subsequent paragraphs are indented to show that they
    belong to the previous footnote.

# Definition

kramdown
: A Markdown-superset converter

Maruku
:     Another Markdown-superset converter

**markdown:**

    kramdown
    : A Markdown-superset converter

    Maruku
    :     Another Markdown-superset converter

# Blockquotes

> “There is nothing either good or bad, but thinking makes it so.”
>
> —Hamlet in *Hamlet*

**markdown:**

    > “There is nothing either good or bad, but thinking makes it so.”
    >
    > —Hamlet in *Hamlet*

---

> “From women’s eyes this doctrine I derive:
>
> They sparkle still the right Promethean fire;
>
> They are the books, the arts, the academes,
>
> That show, contain, and nourish all the world.”
>
> —Berowne in *Love’s Labor’s Lost*

# Emphasis

*Should Old Acquaintance be forgot*

_Should Old Acquaintance be forgot_

**Should Old Acquaintance be forgot**

__Should Old Acquaintance be forgot__

**markdown:**

    *Should Old Acquaintance be forgot*
    _Should Old Acquaintance be forgot_
    **Should Old Acquaintance be forgot**
    __Should Old Acquaintance be forgot__

---

This is a ***text with light and strong emphasis***.

This **is _emphasized_ as well**.

This *does _not_ work*.

This **does __not__ work either**.

**markdown:**

```
This is a ***text with light and strong emphasis***.
This **is _emphasized_ as well**.
This *does _not_ work*.
This **does __not__ work either**.
```

# MathJax

When $$a \ne 0$$, there are two solutions to $$ax^2 + bx + c = 0$$ and they are

$$x_1 = {-b + \sqrt{b^2-4ac} \over 2a}$$

$$x_2 = {-b - \sqrt{b^2-4ac} \over 2a} \notag$$

You need set `mathjax: true` in the *_config.yml* or the markdown’s front matter to **enable** it.
{:.warning}

**After MathJax enabled**, you can set `mathjax_autoNumber: true` to have equations be numbered automatically, You can use `\notag` or `\nonumber` to prevent individual equations from being numbered.
{:.info}

[Documentation](https://tianqi.name/jekyll-TeXt-theme/docs/en/markdown-enhancements#mathjax)

**markdown:**

```tex
When $$a \ne 0$$, there are two solutions to $$ax^2 + bx + c = 0$$ and they are
$$x_1 = {-b + \sqrt{b^2-4ac} \over 2a}$$
$$x_2 = {-b - \sqrt{b^2-4ac} \over 2a} \notag$$
```

**front matter:**

    ---
    ...
    mathjax: true
    mathjax_autoNumber: true
    ---

# Extensions

With the help of extensions, you can easily add **audios**, **videos**, **slides** and **demos** in your posts.

<div>{%- include extensions/ted.html id='emily_esfahani_smith_there_s_more_to_life_than_being_happy' -%}</div>

[Documentation](https://tianqi.name/jekyll-TeXt-theme/docs/en/extensions)

## Audio

### SoundCloud

<div>{%- include extensions/soundcloud.html id='313627932' -%}</div>

### Netease Cloud Music (网易云音乐)

Available in Chinese mainland.

<div>{%- include extensions/netease-cloud-music.html id='413812448' -%}</div>

## Video

### YouTube

<div>{%- include extensions/youtube.html id='wbY97-hdD5c' -%}</div>

### TED

<div>{%- include extensions/ted.html id='emily_esfahani_smith_there_s_more_to_life_than_being_happy' -%}</div>

### bilibili (哔哩哔哩)

<div>{%- include extensions/bilibili.html id='11091080' -%}</div>


## Slide

### SlideShare

<div>{%- include extensions/slideshare.html id='u9L9zDsqEWNKE1' -%}</div>

## Demos

### CodePen

<div>{%- include extensions/codepen.html user='kitian616' hash='aQmWZG' default_tab='html,result' -%}</div>

# Additional Styles

Success!
{:.success}

`success`{:.success} `info`{:.info} `warning`{:.warning} `error`{:.error}

<div class="grid-container">
<div class="grid grid--p-3">
<div class="cell cell--12 cell--md-5 cell--lg-4" markdown="1">
![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_rounded"){:.rounded}
</div>
<div class="cell cell--12 cell--md-5 cell--lg-4" markdown="1">
![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_circle+shadow"){:.circle.shadow}
</div>
</div>
</div>

<div class="grid-container">
<div class="grid grid--p-1">
<div class="cell cell--6 cell--md-4 cell--lg-2">
<div class="button button--success button--pill my-2"><i class="fas fa-space-shuttle"></i> CLICK ME</div>
</div>
<div class="cell cell--6 cell--md-4 cell--lg-2">
<div class="button button--outline-info button--pill my-2"><i class="fas fa-space-shuttle"></i> CLICK ME</div>
</div>
<div class="cell cell--6 cell--md-4 cell--lg-2">
<div class="button button--warning button--rounded my-2"><i class="fas fa-user-astronaut"></i> CLICK ME</div>
</div>
<div class="cell cell--6 cell--md-4 cell--lg-2">
<div class="button button--outline-error button--rounded my-2"><i class="fas fa-user-astronaut"></i> CLICK ME</div>
</div>
</div>
</div>

[Documentation](https://tianqi.name/jekyll-TeXt-theme/docs/en/additional-styles)

## Alert

Success Text.
{:.success}

Info Text.
{:.info}

Warning Text.
{:.warning}

Error Text.
{:.error}

## Tag

`success`{:.success}

`info`{:.info}

`warning`{:.warning}

`error`{:.error}

## Image

| `Border` | `Shadow` |
| ---- | ---- |
| ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_border"){:.border} | ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_shadow"){:.shadow} |

| `Rounded` | `Circle` |
| ---- | ---- |
| ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_rounded"){:.rounded} | ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_circle"){:.circle} |

### Mixture

| `Border+Rounded` | `Circle+Shadow` |
| ---- | ---- |
| ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_border+rounded"){:.border.rounded} | ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_circle+shadow"){:.circle.shadow} |

| `Rounded+Shadow` | `Circle+Border+Shadow` |
| ---- | ---- |
| ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_rounded+shadow"){:.circle.rounded.shadow} | ![Image](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/image.jpg "Image_circle+border+shadow"){:.circle.border.shadow}

## Extra

| Name | Description |
| ---- | ---- |
| Spacing | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/spacing) |
| Grid | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/grid) |
| Icons | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/icons) |
| Image | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/image) |
| Button | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/button) |
| Item | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/item) |
| Card | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/card) |
| Hero | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/hero) |
| Swiper | [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/swiper) |
