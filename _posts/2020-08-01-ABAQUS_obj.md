---
layout: article
title:  "在命令行窗口中运行ABAQUS"
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

* 提交作业：

```shell
abaqus job=<jobname>
```

* 提交带子程序的作业：

```shell
abaqus job=<jobname> user=<subroutine filename> cpus=N
```

job后面输入inp文件名，一般省略inp文件后缀。user后面是用户子程序。常用的ABAQUS子程序源文件使用Fortran语言编写，在使用中实时编译链接成目标文件参与计算。在Windows环境下，源文件必须以`.for`结尾；在Linux环境下，必须使用`.f`后缀。cpus=N，N必须是整数，表示分析使用的处理器核数。

登陆后输入`cat /proc/cpuinfo`即可查询服务器的核数，注意内核的编号是从零开始，因此第N个核的编号是N+1。另外，输入`top`命令可以查询机器运行状态，Tasks中running前面的那个数字就是机器的已用内核数，总核数减去已用内核数既是剩余内核数。

要监视分析作业的进度，您可以查看`.sta`文件。但这不会随着进度的进行而更新状态文件。要动态显示进度，可以使用`tail`命令：

```shell
tail -f <jobname>.sta
```

如果需要终止正在运行的作业，则可以使用`top`命令结束相关进程或使用`killall <process name>`结束该进程。进程名称可以从`top`命令中找到。

参考：

* [Execution Procedures](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-m-ExecutionProcedures-sb.htm), Section 3.2 in Abaqus Analysis User's Guide
  * [Abaqus/Standard and Abaqus/Explicit execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-analysisproc.htm), Section 3.2.2
  * [Abaqus/CAE execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-caeproc.htm), Section 3.2.7
  * [Abaqus/Viewer execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-viewerproc.htm), Section 3.2.8
* [Accessing an output database on a remote computer](https://abaqus-docs.mit.edu/2017/English/SIMACAECAERefMap/simacae-m-DbsNetworkodb-sb.htm)

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

为了摆脱编译器环境，可将目标文件和动态库文件放置在工作目录下，并在`abaqus_v6.env`文件中添加以下两行来将`usub_lib_dir`设置为当前工作目录，或将`usub_lib_dir`直接定义动态库文件所在的文件目录。`abaqus_v6.env`文件既可以放在工作目录，也可以放在主目录中。

```python
import os
usub_lib_dir=os.getcwd()
```

最后在不使用`user`选项的情况下运行作业。求解器将自动从动态库文件中将其加入运算：

```shell
abaqus job=input.inp cpus=n
```

## 运行Python脚本

脚本包含以纯ASCII格式存储的一系列Python语句。如果需要打开Abaqus/CAE并在其中运行脚本，可以直接在命令行输入：

```shell
abaqus cae script=myscript.py
```

其中的`myscript.py`表示脚本的文件名。对于在Abaqus/Viewer中运行的脚本，同样有：

```shell
abaqus viewer script=myscript.py
```

可以通过在命令行中输入`--`并以一个或多个空格分隔的参数来将参数传递到脚本中。这些参数可以在脚本中被访问，但将被Abaqus/CAE在执行时忽略。

如果要在没有图形用户界面（GUI）的情况下运行Abaqus/CAE脚本，可以直接在命令行输入：

```shell
abaqus cae noGUI=myscript.py
```

Abaqus/CAE将在文件中运行命令，并在命令完成后退出。如果没有给出文件扩展名，则默认扩展名是.py。该选项对于自动化分析前或分析后的处理任务很有用，而无需增加运行显示器的费用。由于未提供任何界面，因此脚本不能包含任何用户交互。如果使用`noGUI`选项，则Abaqus/CAE将忽略提供的任何其他命令行选项。

同样的，对于在没有图形用户界面（GUI）的Abaqus/Viewer中运行的脚本有：

```shell
abaqus viewer noGUI=myscript.py
```

如果已经打开了Abaqus/CAE的图形界面，除了可以通过菜单栏中选择`File > Run Script`来运行脚本，还可以在界面下方的Python命令行界面（CLI）采用Python内置函数`execfile`运行脚本：

```python
execfile('myscript.py')
```

需要注意的是，Abaqus仅支持Python 2版本，在最近的Python 3中，`execfile(fn)`函数已被移除，取而代之的是`exec(open(fn).read())`。

详见帮助文档[^3]

参考：

* [Execution Procedures](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-m-ExecutionProcedures-sb.htm), Section 3.2 in Abaqus Analysis User's Guide
  * [Abaqus/CAE execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-caeproc.htm), Section 3.2.7
  * [Abaqus/Viewer execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-viewerproc.htm), Section 3.2.8
  * [Python execution](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-pythonproc.htm), Section 3.2.10
* [How does the Abaqus Scripting Interface interact with Abaqus/CAE?](https://abaqus-docs.mit.edu/2017/English/SIMACAECMDRefMap/simacmd-c-aclintintrointerface.htm), Section 2.2 in Abaqus Scripting User's Guide

---

## 延伸阅读

* [Running an Abaqus analysis with user subroutines without FORTRAN compilers](https://www.linkedin.com/pulse/running-abaqus-analysis-user-subroutines-without-fortran-tripathy)
* [Abaqus子程序使用方法 - Shen](http://feishen.me/2018/02/06/Abaqus-Fortran/)
* [基于python或者.bat实现abaqus任务批处理 - 仿真秀](https://www.fangzhenxiu.com/post/23483)
* [批量执行ABAQUS的inp文件——整理 - CSDN博客](https://blog.csdn.net/qq_39957456/article/details/107191096)

* [Abaqus Analysis User's Guide - Abaqus 2016 Documentation](http://130.149.89.49:2080/v2016/books/usb/default.htm)
  * ["Execution Procedures" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-m-ExecutionProcedures-sb.htm), Section 3.2
* [Abaqus Scripting User's Guide - Abaqus 2016 Documentation](http://130.149.89.49:2080/v2016/books/cmd/default.htm)
  * ["How does the Abaqus Scripting Interface interact with Abaqus/CAE?" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAECMDRefMap/simacmd-c-aclintintrointerface.htm), Section 2.2

[^1]: ["Abaqus/Standard and Abaqus/Explicit execution" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-analysisproc.htm)", Section 3.2.2

[^2]: ["Making user-defined executables and subroutines" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAEEXCRefMap/simaexc-c-makeproc.htm), Section 3.2.18

[^3]: ["How does the Abaqus Scripting Interface interact with Abaqus/CAE?" - MIT](https://abaqus-docs.mit.edu/2017/English/SIMACAECMDRefMap/simacmd-c-aclintintrointerface.htm), Section 2.2
