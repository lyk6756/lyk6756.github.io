---
layout: post
title:  "Table Syntax In Markdown With Kramdown"
---


As the [official Markdown documentation](http://daringfireball.net/projects/markdown/syntax) states, Markdown does not provide any special syntax for tables. Instead it uses HTML `<table>` syntax.

For example, to add an HTML table to a Markdown article:

```html
This is a regular paragraph.

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

This is another regular paragraph.
```

will render as

This is a regular paragraph.

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

This is another regular paragraph.

Here is an online [HTML Table Generator](http://www.tablesgenerator.com/html_tables) that generate html source code into website's source.

# Table syntax in Kramdown

But there exist Markdown syntax extensions which provide additional syntax for creating simple tables.

Kramdown, a fast, pure-Ruby Markdown-superset converter, provides such syntax which is based on the one from the [PHP Markdown Extra](https://michelf.ca/projects/php-markdown/extra/) package.

* Table rows:

```
| First cell|Second cell|Third cell
| First | Second | Third |

First | Second | | Fourth |
```

* Separator lines:

```
|----+----|
+----|----+
|---------|
|-
| :-----: |
-|-
```

  * Header separator lines:

```
|---+---+---|
+ :-: |:------| ---:|
| :-: :- -: -
:-: | :-
```

* Footer separator lines:

```
|====+====|
+====|====+
|=========|
|=
```

Here is an example for a kramdown table with a table header row, two table bodies and a table footer row:

```
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
```

The above example table is rather time-consuming to create without the help of an ASCII table editor. However, the table syntax is flexible and the above table could also be written like this:

```
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
```

will both render as:

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

# Display table border in Jekyll

A minimum table styling is

```scss
table{
    border-collapse: collapse;
    border-spacing: 0;
    border:2px solid #ff0000;
}

th{
    border:2px solid #000000;
}

td{
    border:1px solid #000000;
}
```

Just wrapped it in `_base.scss` file under directory `/_sass/` and that did it.

# Further reading

* [Tables - Kramdown syntax](http://kramdown.gettalong.org/syntax.html#tables)
* [Jekyll kramdown how to display table border](http://www.it1me.com/it-answers?id=28806135&ttl=Jekyll+kramdown+how+to+display+table+border)
