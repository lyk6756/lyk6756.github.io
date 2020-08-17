---
layout: article
title:  "为Abaqus中的状态变量（SDV）自定义关键字"
author: 李宇琨
key: 20200817
lang: zh
tags: ABAQUS Fortran
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://m2qziq.dm.files.1drv.com/y4mzZWEjjAaNARefyxVkKlxgwEqMB9rIn39wANVzd5uOzUAzLqeuSf42u3C7tSgXdUgrJZgR4-vcrINIiY7YVn1tMjgnuI3pF6Z8KzW6Fb318P6UCPtiZd_k0QYcsEUMmDeeJCoTGPhJz3tIsnBGikod3UQNlytoJym4wcdypIwKdDWVnWdaMzOnBusQVoIn1N71leU_ISdOrv3cxIijF73MQ?width=870&height=400&cropmode=none"
---

Abaqus子程序中常见的状态变量（Solution-Dependent state Variables, SDV)，常见于UMAT、VUMAT、USDFLD、VUSDFLD等子程序中。其默认输出形式为`SDVn`，其中的n表示状态变量的顺序。其个数在`.inp`作业文件中由关键字`*Depvar`声明：

```
*Depvar
    4
```

上述语句声明了4个状态变量，可在后处理中找到他们，分别是`SDV1`至`SDV4`。

为了能够在状态变量较多时更好地区分各个状态变量代表的含义，可在以上声明语句之后继续定义各个变量的关键字及其描述：

```
*Depvar
    4
1, DFT, "fiber tensile damage"
2, DFC, "fiber compressive damage"
3, DMT, "matrix tensile damage"
4, DMC, "matrix compressive damage"
```

更一般的语法为：

```
*Depvar
    <number>
<index>, <label>, <description>
```

其中，

* `<number>`声明了状态变量的个数。

* `<index>`表明定义输出关键字及描述的状态变量索引序号，对于第一个状态变量，该值为1。

* `<label>`定义了状态变量的输出关键字，其命名需要满足：最多可包含80个字符；除非用引号引起来，否则标签内的所有空格都将被忽略；未用引号引起来的必须以字母开头，且不得包含句号（.）；不得包含逗号和等号等字符。此外，不能以双下划线开头和结尾（例如`__STEEL__`），此标签格式保留供Abaqus内部使用。更详细的名称规范可参见[Input Syntax Rules](https://abaqus-docs.mit.edu/2017/English/SIMACAEMODRefMap/simamod-c-inputsyntax.htm)。**特别的，大小写将会被保留。**

* `<description>`给出了输出变量的描述，一般用引号引起来。其命名规则需满足[Input Syntax Rules](https://abaqus-docs.mit.edu/2017/English/SIMACAEMODRefMap/simamod-c-inputsyntax.htm)中规定的labels。

最终在Abaqus/Viewer中看到的效果为：`SDV_<label>`。以上述为例，最终显示为`SDV_DFC`、`SDV_DFT`、`SDV_DMC`和`SDV_DMT`。

---

## 延伸阅读

* [*DEPVAR - abaqus-docs.mit.edu › simakey-r-depvar](https://abaqus-docs.mit.edu/2017/English/SIMACAEKEYRefMap/simakey-r-depvar.htm)

* [Input Syntax Rules - abaqus-docs.mit.edu › simamod-c-inputsyntax](https://abaqus-docs.mit.edu/2017/English/SIMACAEMODRefMap/simamod-c-inputsyntax.htm)
