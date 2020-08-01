---
layout: article
title:  "在控制台中运行ABAQUS子程序"
author: 李宇琨
key: 20200801
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

## 在关联了Fortran编译器的环境中

常用的ABAQUS子程序源文件以`.for`结尾，使用Fortran语言编写。在使用中实时编译链接成目标文件参与计算。

```shell
abaqus job=input.inp user=subroutine.for cpus=n
```

详见帮助文档[^1]

## 在未关联编译器的环境中

如果子程序已开发完成，需要进行分发使用。为了使子程序能够在没有关联编译环境的计算机上执行，或者不希望用户关注到源代码，可以使用ABAQUS自带的MAKE工具将`.for`源文件封装成目标文件和动态库文件。

在关联了Fortran编译器的环境下执行：

```shell
abaqus make library=subroutine.for object_type=fortran
```

详见帮助文档[^2]

将生成两个文件，目标文件和动态库文件。目标文件以`.obj`（Windows系统下）或`.o`（Linux系统下）结尾，动态库文件以`.dll`（Windows系统下）或`.so`（Linux系统下）结尾。Abaqus/Standard的目标文件后缀为`-std`， Abaqus/Explicit的单精度目标文件后缀为`-xpl`；双精度目标文件后缀为`-xplD`。生成的Abaqus/Standard动态库文件名为`standardU`，Abaqus/Explicit动态库文件名为`explicitU`和`explicitU-D`。

我们这里可以使用生成的目标文件`subroutine-std.obj`来提交计算，但仍然需要链接编译器环境。

```shell
abaqus job=input.inp user=subroutine-std.obj cpus=n
```

为了摆脱编译器环境，可将目标文件和动态库文件放置在工作目录下，并在`abaqus_v6.env`文件中添加以下两行来将`usub_lib_dir`设置为当前工作目录。`abaqus_v6.env`文件既可以放在工作目录，也可以放在主目录中。

```python
import os
usub_lib_dir=os.getcwd()
```

最后在不使用`–user`选项的情况下运行分析。求解器将自动从动态库文件中将其加入运算。

```shell
abaqus job=input.inp cpus=n
```

---

## 延伸阅读

* [Running an Abaqus analysis with user subroutines without FORTRAN compilers](https://www.linkedin.com/pulse/running-abaqus-analysis-user-subroutines-without-fortran-tripathy)
* [Abaqus子程序使用方法 - Shen](http://feishen.me/2018/02/06/Abaqus-Fortran/)
* [Abaqus Analysis User's Guide - Abaqus 2016 Documentation](http://130.149.89.49:2080/v2016/books/usb/default.htm)
  * ["Execution Procedures" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-m-ExecutionProcedures-sb.htm), Section 3.2

[^1]: ["Abaqus/Standard and Abaqus/Explicit execution" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-analysisproc.htm)", Section 3.2.2

[^2]: ["Making user-defined executables and subroutines" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-makeproc.htm), Section 3.2.18