---
layout: post
title:  "在Win10下利用VS2017及Intel Fortran Compiler安装配置FEAP"
date:   2017-09-07
author: 李宇琨
categories: Fortran
tags: FEAP Intel
cover:  "https://pnqw0q-dm2305.files.1drv.com/y4m0jG-CG3_RC_0fyGfFF9O0SzNsiL2XSMzQyLFdLcXXnuAAPWW7uwirx8cM_pVh09OCc4Z66Ug2TSm7QTUHtNBGJ3u89-AEVEF9anLU-f-LBWRihBjnI_Q2JI76fVEvpu2_kB72BfXeuBKPshY9gdJunSal0h6UdcIvsCh-qFHH1tb8SvFPyLBJMje_Q0xytHtlncfdP0DkjROFhRbtKnFtA?width=1687&height=809&cropmode=none"
---

<!-- TOC -->

- [前言](#前言)
- [部署平台](#部署平台)
- [准备工作](#准备工作)
    - [安装Visual Studio 2015](#安装Visual Studio 2015)
    - [安装Intel Parallel Studio XE](#安装Intel Parallel Studio XE)
- [安装FEAP](#安装FEAP)
    - [准备](#准备)
    - [生成链接库](#生成链接库)
    - [生成可执行文件](#生成可执行文件)
- [添加PARDISO求解器](#添加PARDISO求解器)
- [延伸阅读](#延伸阅读)

<!-- TOC -->

# 前言

[FEAP](http://projects.ce.berkeley.edu/feap/)(a Finite Element Analysis Program)，是由美国加州大学伯克利分校土木与环境工程系的Robert L. Taylor教授领导开发的通用有限元分析程序。整个程序由Fortran语言编写，并能够直接获取到源代码。是科研工作者的有力武器。

本文主要介绍FEAP在Win10操作系统下的安装部署，其中需要用到Visual Studio 2017集成开发环境以及Intel Fortran Compiler编译器。

[Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers)是知名的跨平台Fortran编译器，提供了对Intel最新处理器指令集的支持。[Intel Parallel Studio XE](https://software.intel.com/en-us/intel-parallel-studio-xe)是由Intel开发的跨平台软件开发工具套件。里面就包含了我们需要的Intel Fortran Compiler。其中就有Intel数学核心函数库[Intel Math Kernel Library](https://software.intel.com/en-us/mkl)。其他的包含内容可以参考[Documentation for Intel Parallel Studio XE Support](https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation)。同时，Intel Parallel Studio XE提供了Windows平台下对[Visual Studio](https://www.visualstudio.com/)集成开发环境的支持。

需要指出的是，Intel Parallel Studio XE是付费软件，一般用户可以下载提供30天免费体验的评估版本。

与此同时，Intel还为在校学生，教育工作者，科研工作者和开源提供者提供了免费的使用权限。在[Quafily for Free Software Tools](https://software.intel.com/en-us/qualify-for-free-software)页面就可以直接提出申请。


# 部署平台

* Windows 10 专业版 64位

* Visual Studio 2015 (Version 14.0)

* Intel Parallel Studio XE Cluster Edition for Windows (Version 2017 Update 4) / Intel Fortran Compiler 17.0 Update 4

* FEAP Version 8.5


# 准备工作

## 安装Visual Studio 2015

微软提供的[Visual Studio](https://www.visualstudio.com/zh-hans/vs/)是一款广泛应用在Windows平台的集成开发环境。目前最新版本的Visual Studio 2017提供了适用于学生、开源和个人开发人员的功能完备的免费版本[Visual Studio Community](https://www.visualstudio.com/zh-hans/vs/community/)。

**由于Intel Parallel Studio XE Version 2017 Update 4 并不能提供对VS2017最新版本的支持，需要前往[Visual Studio Dev Essentials section](https://www.visualstudio.com/dev-essentials/)下载VS2017 15.0版本的安装器。**随着Intel Parallel Studio XE的后续升级，将提供对VS2017最新版本的支持。

根据[Parallel Studio XE 2017: Getting Started with the Intel® Fortran Compiler 17.0 for Windows](https://software.intel.com/en-us/get-started-with-fortran-compiler-17.0-for-windows-parallel-studio-xe-2017)和[Installing Visual Studio 2015 for Use with Intel Compilers](https://software.intel.com/en-us/articles/installing-visual-studio-2015-for-use-with-intel-compilers)，为了使Visual Studio 2015与接下来安装的Intel C++ and Fortran Compilers for Windows（即Intel Parallel Studio XE 2017套件）适配，需要在安装界面勾选VS对C++的支持，即"使用C++的桌面开发"选项（Desktop development with C++)。

![安装Visual Studio 2015_1](https://software.intel.com/sites/default/files/managed/8b/68/community1_0.png)

![安装Visual Studio 2015_2](https://software.intel.com/sites/default/files/managed/0d/f2/community2_0.png)

## 安装Intel Parallel Studio XE

根据[Intel® Parallel Studio XE 2017 update 4 for Windows and Linux Release Notes](https://software.intel.com/sites/default/files/managed/86/c3/PSXE2017Update4_Release_Notes_en_US_Lin_Win.pdf)，我们使用的Intel Parallel Studio XE Cluster Edition for Windows (Version 2017 Update 4)版本安装包提供了对Visual Studio 2015的支持。更详细的安装前要求可参见[Intel® Parallel Studio XE 2017 Update 4 Installation Guide for Windows* OS](https://software.intel.com/sites/default/files/managed/5f/c3/parallel-studio-xe-install-guide-windows.pdf)。

直接双击运行已经下载好的离线安装器，并根据提示输入序列号即可完成安装。

如果安装程序在检测中提示找不到VS开发环境，表明VS版本过高，需要安装较低版本的，或直接更换为VS2015。详情参见：[Intel Parallel Studio 2017 Update 4 won't detect Visual Studio 2017](https://software.intel.com/zh-cn/forums/intel-visual-fortran-compiler-for-windows/topic/742726)。


# 安装FEAP

目前FEAP的最新版本为8.5，关于版本的详细信息请前往[http://projects.ce.berkeley.edu/feap/](http://projects.ce.berkeley.edu/feap/)了解。详细的安装步骤请参考[FEAP Installation Manual: v8.5](http://projects.ce.berkeley.edu/feap/imanual85.pdf)

我们接下来需要利用刚安装好的Intel Visual Fortran，在Visual Studio开发环境下将提供的FEAP源代码生成为可执行的FEAP二进制文件。其中也包含了所有的图形界面选项。

建议将所有下载到的所有信息放在一个名为`feap`的文件夹中，并在其中创建一个子文件夹`ver85`用于存放所有的程序源代码。具体的目录结构如下所示

```
feap
    ver85
        contact ------------+- main
        elements ---+       |- ntrnd
        main        |       |- nts2d
        maintain    |       |- nts3d
        plot        |       |- ptpnd
        program     |       |- tie2d
        unix        |       +- util
        user        +------------------- elements
        windows ----+- memory               |- acousticnd
        packages ---+- arpack -+- archive   |- frame
        unix        +- blas                 |- material
        user        +- lapack               |    |- small
        window1     +- meshmod              |    +- finite
        window2                             |- shells
        include ------------+- integer4     |- solid1d
                            +- integer8     |- solid2d
        parfeap ----+- partition            |- solid3d
                    +- unix                 |- thermal
                    +- windows              |- torsion
                    +- packages -+          |- couple3d
                                 +- arpack  |- robin
                                            |- winkler
```

## 准备

一般地，我们习惯于将安装包中的所有文件放置在一个单独的库中进行编译（主程序除外，位于源文件`main`文件夹中的`feap85.f`文件）。例如，创建一个名为*lib85*库并将所有的程序都添加在这之中。然后就可以创建主程序*feap*并让其包含这个库。

为了在后面的编译过程中，便于在Visual Studio中添加源文件。我们可以提前将各个文件目录下的所有源文件拷贝至一个集中的文件夹`compile`。一个简单的批处理文件就能够完成这项操作。对于64位操作系统，有如下的`win2comp8.bat`文件：

```
mkdir compile
copy  .\contact\main\*.f compile
copy  .\contact\ntrnd\*.f compile
copy  .\contact\nts2d\*.f compile
copy  .\contact\nts3d\*.f compile
copy  .\contact\ptpnd\*.f compile
copy  .\contact\tie2d\*.f compile
copy  .\contact\util\*.f compile
copy  .\elements\acousticnd\*.f compile
copy  .\elements\couple3d\*.f compile
copy  .\elements\frame\*.f compile
copy  .\elements\material\*.f compile
copy  .\elements\material\small\*.f compile
copy  .\elements\material\finite\*.f compile
copy  .\elements\robin\*.f compile
copy  .\elements\shells\*.f compile
copy  .\elements\solid1d\*.f compile
copy  .\elements\solid2d\*.f compile
copy  .\elements\solid3d\*.f compile
copy  .\elements\thermal\*.f compile
copy  .\elements\torsion\*.f compile
copy  .\elements\winkler\*.f compile
copy  .\include\*.h compile
copy  .\include\integer8\*.h compile
copy  .\plot\*.f compile
copy  .\program\*.f compile
copy  .\program\*.inc compile
copy  .\user\*.f compile
copy  .\windows\*.f compile
copy  .\windows\memory\*.f compile
copy  .\window2\*.f compile
```

只需将其放置在`ver85`文件夹下并运行就可以了。

对于32位操作系统，类似的批处理文件`win2comp4.bat`只需将其中的`copy  .\include\integer8\*.h compile`更换为`copy  .\include\integer4\*.h compile`即可。

## 生成链接库

在Visual Studio中创建一个新的项目：

* 选择模板为`Intel(R) Visual Fortran > Library > Static Library`，创建一个Fortran**静态**链接库。*注意这里不能选择动态链接库(Dynamic-link Library)*；
* 将项目名称起为*lib85*
* 将项目路径设置为`C:\Users\lyk\Documents\feap\build`

在创建了`lib85`项目之后，在菜单栏中选择`生成 > 配置管理器`（`Build > Configuration Manager`），或直接在工具栏中，调整`活动解决方案设置`（`Active solution configuration`）为`Release`。如果一定要使用`Debug`，就必须将编译器设置为忽略数组边界检查。对于64位操作系统，还可将`活动解决方案平台`（`Active solution platform`）从`x86`调整为`x64`。

![设置平台](https://qxpeqw-dm2305.files.1drv.com/y4p95v6mHPc544CvjbNVqyZfS-14br4c-e_wRHLZyBP1zfvDAf_cTz0f7i92V8-DBrIgFtfaF8bPxoUQUbyI3mAvHz1903dRalm-U1NGcp2bIrMjiSFK1FCcEPFU4ReFVJmjQXFobajXs6Y82QuSpBnNjKQwGs9QW5LMa80a6EYRjtPMmtjnrKgYRju3NWrGF9r92fW8bm2VKfWIJHWO8_0og/install_feap2.png?psid=1)

接下来，在菜单栏中选择`项目 > 属性`（`Project > Properties`），打开项目属性页，在左侧的配置属性中依次选择`Fortran > Preprocessor`，并在右侧的`Additional Include Directories`中添加两个路径

![添加路径](https://ythpiq-dm2305.files.1drv.com/y4pea9raeFdJL9Eej_XYIedthxyDefJci8zXZ93o3mdMPuHNgh2_e7P7-6Nc_nIzlyZ3f6KBrVN7P-XbFi-f48ryFGWTuPb-NtBR61au1aLx1q7A9-X_pt4bkwvSTV3TlV41tj_FqVc5hrxGlOS6-706HINb17BuTZAlGCfCGvTk8a-xkgFamCCiZDn9uWFzl67QANKn2cg8E_w9-qvbZW_2w/install_feap1.png?psid=1)

```
C:\Users\lyk\Documents\feap\ver85\include
C:\Users\lyk\Documents\feap\ver85\include\integer8
```

注意，对于32位操作系统，需要将第二个路径中的`integer8`更改为`integer4`。

以上填入的两个路径也可以用之前拷贝生成的`compile`替代：`C:\Users\lyk\Documents\feap\ver85\compile`。

然后，就是将程序源文件添加进VS中的项目里。在菜单栏中选择`项目 > 添加现有项`（`Project > Add Existing Item...`）， 将`ver85`目录下的`contact`, `element`, `plot`, `program`, `user`, `windows`文件夹中的所有Fortran源文件添加进项目中，包括这些文件夹下的所有子目录。然后选择`windows1`或者`windows2`文件夹这其中之一，将其中的所有Fortran源文件也一并添加进来。`windows1`和`windows2`的区别在于，`windows1`中的文件将会创建文本与图像整合在一起的窗口，而`windows2`则将创建分开的文本窗口和图像窗口。这些文件都在之前创建的`compile`文件夹中，可以一次性添加完成。添加完成后就能够在右侧的解决方案资源管理器（Solution Explorer）中的`Source Files`下看到刚才添加的所有文件。

最后，在菜单栏中选择`生成 > 生成解决方案`（`Build > Build Solution`），最后应该能够在输出窗口看到提示：`lib85 - 0 error(s), 0 warning(s)`。生成的所有静态库都保存在路径`C:\Users\lyk\Documents\feap\build\lib85\lib85\x64\Release`下。

## 生成可执行文件

在完成了静态链接库`lib85.lib`的编译后，就可以利用这个进行最后的可执行文件的生成。

在Visual Studio中创建一个新的项目：

* 选择模板为`Intel(R) Visual Fortran > QuickWin Application > QuickWin Application`；
* 将项目名称起为*feap*
* 将项目路径设置为`C:\Users\lyk\Documents\feap\build`

同样的，我们需要在创建了`feap`项目之后，在菜单栏中选择`生成 > 配置管理器`（`Build > Configuration Manager`），或直接在工具栏中，调整`活动解决方案设置`（`Active solution configuration`）为`Release`。如果一定要使用`Debug`，就必须将编译器设置为忽略数组边界检查。对于64位操作系统，还可将`活动解决方案平台`（`Active solution platform`）从`x86`调整为`x64`。

接下来，在菜单栏中选择`项目 > 属性`（`Project > Properties`），打开项目属性页，在左侧的配置属性中依次选择`Fortran > Preprocessor`，并在右侧的`Additional Include Directories`中添加两个路径

```
C:\Users\lyk\Documents\feap\ver85\include
C:\Users\lyk\Documents\feap\ver85\include\integer8
```

注意，对于32位操作系统，需要将第二个路径中的`integer8`更改为`integer4`。

以上填入的两个路径也可以用之前拷贝生成的`compile`替代：`C:\Users\lyk\Documents\feap\ver85\compile`。

然后，就是将上一步中生成的链接库添加进当前的项目里。在菜单栏中选择`项目 > 添加现有项`（`Project > Add Existing Item...`）， 将路径`C:\Users\lyk\Documents\feap\build\lib85\lib85\x64\Release`下的`lib85.lib`文件添加进来。

接着，将主程序添加进当前的项目中。找到在源代码文件夹，将`ver85`目录下`main`中的`feap85.f`添加进来。

最后，在菜单栏中选择`生成 > 生成解决方案`（`Build > Build Solution`）。生成的可执行保存在路径`C:\Users\lyk\Documents\feap\build\feap\feap\x64\Release`下，其中的`feap.exe`就是我们需要的程序。


# 添加PARDISO求解器

[Pardiso](http://www.pardiso-project.org/)是一个用于求解大型稀疏对称和非对称线性方程组的求解器。PARDISO的算法针对共享内存和分布式内存多处理器的高性能计算器进行优化，具有非常高的计算效率和并行性。同时，Intel的数学核心库(Math Kernel Library, MKL)提供了针对PARDISO的支持，可以直接调用。

更多参考资料请参见：

* [Topic: MKL Pardiso Solver - Thread Parallel](http://feap.berkeley.edu/forum/index.php?topic=761.0)

* [PARDISO](http://www.pardiso-project.org/)

* [Intel® Math Kernel Library (Intel® MKL)](https://software.intel.com/en-us/mkl) / [Documentation for Intel® Math Kernel Library](https://software.intel.com/en-us/mkl/documentation)
* [Developer Reference for Intel® Math Kernel Library 2017 - Fortran](https://software.intel.com/en-us/mkl-developer-reference-fortran) / [Intel MKL PARDISO - Parallel Direct Sparse Solver Interface](https://software.intel.com/en-us/mkl-developer-reference-fortran-intel-mkl-pardiso-parallel-direct-sparse-solver-interface)
* [Intel® MKL PARDISO](https://software.intel.com/en-us/articles/intel-mkl-pardiso)
* [Link your Project to MKL libraries](https://software.intel.com/en-us/articles/link-your-project-to-mkl-libraries) / [Compiling and Linking Intel® Math Kernel Library with Microsoft* Visual C++*](https://software.intel.com/en-us/articles/intel-math-kernel-library-intel-mkl-compiling-and-linking-with-microsoft-visual-cc)


# 延伸阅读

* [FEAP](http://projects.ce.berkeley.edu/feap/) / [FEAPpv](http://projects.ce.berkeley.edu/feap/feappv) / [FEAP User Forum](http://feap.berkeley.edu/forum/index.php)
* [FEAP Installation Manual: v8.5](http://projects.ce.berkeley.edu/feap/imanual85.pdf)
* [FEAP Install Mac or Linux (Cygwin too) - YouTube](https://www.youtube.com/watch?v=_ohQ__rqq3Y)
* [FEAP Install Windows 7 with VS2010 and Intel XE Fortran 2011 - YouTube](https://www.youtube.com/watch?v=7QAh6QvOT6s)



* [Intel Parallel Studio XE](https://software.intel.com/en-us/intel-parallel-studio-xe) / [Documentation for Intel Parallel Studio XE Support](https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation)
* [Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers) / [Documentation for Intel Fortran Compiler Support](https://software.intel.com/en-us/fortran-compilers-support/documentation)
* Intel® Parallel Studio XE 2017 Update 4: [Readme](https://software.intel.com/en-us/articles/intel-parallel-studio-xe-2017-update-4-readme) / [Release Notes](https://software.intel.com/en-us/articles/intel-parallel-studio-xe-release-notes) / [Installation Guide for Windows* OS](https://software.intel.com/en-us/download/parallel-studio-xe-2017-install-guide-windows)
* [Intel® Software Documentation Library](https://software.intel.com/en-us/intel-software-technical-documentation)
* [Parallel Studio XE 2017: Getting Started with the Intel® Fortran Compiler 17.0 for Windows*](https://software.intel.com/en-us/get-started-with-fortran-compiler-17.0-for-windows-parallel-studio-xe-2017)
* [Intel® Fortran Compiler 17.0 Developer Guide and Reference](https://software.intel.com/en-us/intel-fortran-compiler-17.0-user-and-reference-guide) / [Using Microsoft Visual Studio (Windows*)](https://software.intel.com/en-us/node/677902)
* [Installing Visual Studio 2015 for Use with Intel Compilers](https://software.intel.com/en-us/articles/installing-visual-studio-2015-for-use-with-intel-compilers)
* [Installing Microsoft Visual Studio* 2017 for Use with Intel® Compilers](https://software.intel.com/en-us/articles/installing-microsoft-visual-studio-2017-for-use-with-intel-compilers)
* [Intel® C++ and Fortran Compilers for Windows Integration Into Microsoft Visual Studio 2017](https://software.intel.com/en-us/articles/intel-c-fortran-compilers-for-windows-integration-into-microsoft-visual-studio-2017)
* [Intel Parallel Studio 2017 Update 4 won't detect Visual Studio 2017](https://software.intel.com/zh-cn/forums/intel-visual-fortran-compiler-for-windows/topic/742726)
* [Intel® Software Development tools integration to Microsoft* Visual Studio 2017 issues](https://software.intel.com/en-us/articles/intel-software-development-tools-integration-to-vs2017-issue)
* [Troubleshooting Fortran Integration Issues with Microsoft Visual Studio*](https://software.intel.com/en-us/articles/troubleshooting-fortran-integration-issues-with-visual-studio)
