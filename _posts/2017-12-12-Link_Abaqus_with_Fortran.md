---
layout: article
title:  "在Win10下搭建Abaqus子程序开发环境"
author: 李宇琨
key: 20171212
lang: zh
tags: ABAQUS Fortran Microsoft
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://pnqw0q-dm2305.files.1drv.com/y4m0jG-CG3_RC_0fyGfFF9O0SzNsiL2XSMzQyLFdLcXXnuAAPWW7uwirx8cM_pVh09OCc4Z66Ug2TSm7QTUHtNBGJ3u89-AEVEF9anLU-f-LBWRihBjnI_Q2JI76fVEvpu2_kB72BfXeuBKPshY9gdJunSal0h6UdcIvsCh-qFHH1tb8SvFPyLBJMje_Q0xytHtlncfdP0DkjROFhRbtKnFtA?width=1687&height=809&cropmode=none"
---

## 前言

Abaqus为用户提供了强大而又灵活的用户子程序接口和应用程序接口。用户可以定义包括边界条件、荷载条件、接触条件、材料特性以及利用用户子程序和其它应用软件进行数据交换等等。这些用户子程序接口使用户解决一些问题时有很大的灵活性，同时大大的扩充了Abaqus的功能。

由于Abaqus的子程序需要使用Fortran程序语言编写，因此需要有编译器对子程序进行编译才能被Abaqus调用。Abaqus为Intel Fortran Compiler提供了程序接口。目前，Intel Fortran Compiler已被集成在[Intel Parallel Studio XE](https://software.intel.com/en-us/intel-parallel-studio-xe)中提供。此外，Microsoft Visual Studio也需要一并安装，来为Intel Fortran Compiler提供必要的开发环境。

本文介绍在Win10平台下关联Abaqus、Intel Fortran编译器以及Microsoft Visual Studio的具体方法。**需要注意的是，在这三个软件中，某个软件的最新版本并不一定能够得到其他软件的互相支持。**因此在选择程序的版本号时需要用户进行仔细的考查。[这个网页](https://software.intel.com/content/www/us/en/develop/articles/intel-parallel-studio-xe-compilers-required-microsoft-visual-studio.html)给出了Visual Studio和Intel Parallel Studio XE各个版本的适配情况。

下面的配置方案能够为你提供一个参考。

## 部署平台

* Windows 10 专业版 64位

* Microsoft Visual Studio Ultimate 2013 with Update 5 (Version 12.0.X Update 5)

* Intel Parallel Studio XE Cluster Edition for Windows (Version 2016 Update 4) / Intel Fortran Compiler 16.0 Update 4

* Abaqus 2017

## 安装步骤

默认您已完成Abaqus 2017的安装工作。

接下来请务必按照如下步骤安装。

### 步骤1：下载安装Microsoft  Visual Studio

社区版本的Microsoft Visual Studio 2013能够在微软官网上免费下载获得：[https://www.visualstudio.com/en-us/news/releasenotes/vs2013-community-vs](https://www.visualstudio.com/en-us/news/releasenotes/vs2013-community-vs)。

在安装时务必勾选“用于C++的Microsoft基础类”包。

### 步骤2：下载安装Intel  Parallel Studio XE

Intel Parallel Studio XE是付费软件，一般用户可以下载提供30天免费体验的评估版本。

与此同时，Intel还为在校学生，教育工作者，科研工作者和开源提供者提供了免费的使用权限。在[Quafily for Free Software Tools](https://software.intel.com/en-us/qualify-for-free-software)页面就可以直接提出申请。

对于Windows和Linux平台，C/C++编译器和Fortran编译器被集成在了一个安装包内，在下载页面下载Intel Parallel Studio XE  Edition for Fortran macOS，并在安装时提交Intel提供的序列号即可完成安装。

在安装的最后，安装程序将自动完成Visual Studio与Intel Fortran Compiler的关联工作。

### Troubleshooting

完成Abaqus 2017的安装后，如果在启动CAE时命令行显示：

```text
License server system does not support this feature.
Feature:       cae_teaching
License path:  27011devil;
FLEXnet Licensing error:-18,147
For further information, refer to the FLEXnet Licensing documentation,
or contact your local Abaqus representative.
Abaqus Error: Abaqus/CAE Kernel exited with an error.
```

将文件`C:\Program Files\Dassault Systemes\SimulationServices\V6R2017x\win_b64\SMA\site\custom_v6.env`中的最后一行

```python
academic=TEACHING
```

删除并重新运行CAE。

## 关联配置

### 准备工作

查找以下文件的路径：

* Visual Studio的`vcvars64.bat`文件。默认路径为`C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\amd64\vcvars64.bat`

* Intel Fortran Compiler的`ifortvars.bat`文件。默认路径为`C:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2016.4.246\windows\bin\ifortvars.bat`

## 设置Abaqus CAE及Abaqus Command启动方式

为了能够在启动Abaqus时默认加载Intel Fortran Compiler，需要对启动Abaqus的快捷方式进行修改：

找到启动Abaqus CAE的批处理文件`launcher.bat`。默认路径为`C:\SIMULIA\CAE\2017\win_b64\resources\install\cae\launcher.bat`。右键点击`编辑`，在其中添加启动Visual Studio和Fortran编译器的指令

```
@call "C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\amd64\vcvars64.bat"
@call "C:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2016.4.246\windows\bin\ifortvars.bat" intel64 vs2013
```

这样就完成了关联配置工作。

或参考：[Abaqus2019关联VS2017和IVF2019](http://www.kudincha.cn/156.html)

另一种关联方法是对快捷方式的目标进行设置：

* 对于Abaqus CAE快捷方式，`右键`->`属性`->`快捷方式`选项卡中的`目标`一栏中，将

```
C:\SIMULIA\CAE\2017\win_b64\resources\install\cae\launcher.bat cae || pause
```

更改为

```
"C:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2016.4.246\windows\bin\ifortvars.bat" intel64 vs2013 & C:\SIMULIA\CAE\2017\win_b64\resources\install\cae\launcher.bat cae || pause
```

* 对于Abaqus Command快捷方式，`右键`->`属性`->`快捷方式`选项卡中的`目标`一栏中，将

```
C:\Windows\system32\cmd.exe /k
```

更改为

```
"C:\Program Files (x86)\IntelSWTools\compilers_and_libraries_2016.4.246\windows\bin\ifortvars.bat" intel64 vs2013 & C:\Windows\system32\cmd.exe /k
```

在运行时，需要用户提供管理员权限。

### 验证

* 为了验证Abaqus是否能够查询到Fortran编译器，可以在Abaqus Command中执行命令：`abaqus info=system`。在给出的信息中，`C++ Compiler`、`Linker Version`、`Fortran Compiler`和`MPI`应给出正确的相关信息。

* 为了验证Abaqus是否能够正确运行子程序，可以在Abaqus Command中执行命令：`abaqus verify –user_std` (Abaqus Standard subroutines)、“abaqus verify –user_exp” (Abaqus Explicit subroutines)、“abaqus verify –all” (All Abaqus verifications) 或是直接运行Abaqus Verification，如果关于subroutines的验证信息显示PASS，则说明已经成功完成所有工作。

Enjoy:)

## 更新：已知的其他配置

* Abaqus 6.14 + Visual Studio 2013 + Intel Visual Fortran XE 2013 [参考](https://blog.csdn.net/qintianhaohao/article/details/79355893)

* Abaqus 2018/2019 + Visual Studio 2015 + Intel Parallel Studio XE 2019 [参考](https://blog.csdn.net/ghfuidy/article/details/102863933)

* Abaqus 2020 + Visual Studio 2019 + Intel Parallel Studio XE 2020 [参考](https://zhuanlan.zhihu.com/p/112449922)

---

## 延伸阅读

* [How to link abaqus with intelfortran? - ResearchGate](https://www.researchgate.net/post/How_to_link_abaqus_with_intelfortran)
* [Linking ABAQUS 2017 and Intel Parallel Studio XE2016 (Visual Fortran) in Windows 10 x64 - ResearchGate](https://www.researchgate.net/publication/313924098_Linking_ABAQUS_2017_and_Intel_Parallel_Studio_XE2016_Visual_Fortran_in_Windows_10_x64)
