---
layout: post
title:  "在MacOS下搭建Fortran开发环境"
date:   2017-08-04
author: 李宇琨
categories: Fortran
tags: Intel Xcode
cover:  "https://pnqw0q-dm2305.files.1drv.com/y4m0jG-CG3_RC_0fyGfFF9O0SzNsiL2XSMzQyLFdLcXXnuAAPWW7uwirx8cM_pVh09OCc4Z66Ug2TSm7QTUHtNBGJ3u89-AEVEF9anLU-f-LBWRihBjnI_Q2JI76fVEvpu2_kB72BfXeuBKPshY9gdJunSal0h6UdcIvsCh-qFHH1tb8SvFPyLBJMje_Q0xytHtlncfdP0DkjROFhRbtKnFtA?width=1687&height=809&cropmode=none"
---

<!-- TOC -->

- [前言](#前言)
- [部署平台](#部署平台)
- [安装步骤](#安装步骤)
    - [安装Xcode及Command Line Tools](#安装Xcode及Command Line Tools)
    - [下载安装Intel Parallel Studio XE](#下载安装Intel Parallel Studio XE)
- [配置](#配置)
    - [准备工作](#准备工作)
    - [在Xcode中运行Fortran](#在Xcode中运行Fortran)
    - [Troubleshooting](#Troubleshooting)
- [延伸阅读](#延伸阅读)

<!-- TOC -->

# 前言

Fortran语言作为世界上最早出现的计算机高级程序设计语言，历经了几十年的发展和积累，目前依旧广泛应用在科学和工程计算领域。

目前跨平台的主流Fortran编译器主要有：

1. [GFortran](https://gcc.gnu.org/fortran/)：[GNU Project](http://www.gnu.org/)的一部分，一般集成在[GCC](https://gcc.gnu.org/)中，提供对Fortran 95/2003/2008的编译支持，是一款免费的开源编译器；
2. [Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers)：在Windows平台就是知名的Intel Visual Fortran，提供了对Intel最新处理器指令集的支持。但这是一款收费的软件。

[Intel Parallel Studio XE](https://software.intel.com/en-us/intel-parallel-studio-xe)是由Intel开发的跨平台软件开发工具套件。里面就包含了我们需要的Intel Fortran Compiler。其他的包含内容可以参考[Documentation for Intel Parallel Studio XE Support](https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation)。同时，Intel Parallel Studio XE提供了macOS下对[Xcode](https://developer.apple.com/xcode/)的支持，因此我们选择安装这一套件。


# 部署平台

* MacOS 10.12

* Intel Parallel Studio XE Composer Edition for Fortran macOS (Version 2017 Update 4) / Intel Fortran Compiler 17.0 Update 4

* Xcode 8.2 with Command Line Tools


# 安装步骤

## 安装Xcode及Command Line Tools

根据[Intel® Parallel Studio XE 2017 Update 4 for macOS* Installation Guide
and Release Notes](https://software.intel.com/sites/default/files/managed/86/c3/PSXE2017Update4_Release_Notes_en_US_OSX.pdf)，2017 Update 4版本最高支持macOS 10.12.1和Xcode 8.3。因此，除了可以在App Store中直接下载安装对应版本的Xcode中之外，还可以前往Apple的开发者页面，在登录Apple ID后访问[Downloads for Apple Developers](https://developer.apple.com/download/more/)下载对应版本的Xcode。与其相对应的Command Line Tools也能够一并在该页面找到。

从App Store下载的Xcode，默认是没有安装command Line Tools的。在成功安装Xcode之后，打开一个新的终端并输入：
```
$ xcode-select --install
```
根据弹出的提示完成安装即可。

## 下载安装Intel Parallel Studio XE

Intel Parallel Studio XE是付费软件，一般用户可以下载提供30天免费体验的评估版本。

与此同时，Intel还为在校学生，教育工作者，科研工作者和开源提供者提供了免费的使用权限。在[Quafily for Free Software Tools](https://software.intel.com/en-us/qualify-for-free-software)页面就可以直接提出申请。

对于Windows和Linux平台，C/C++编译器和Fortran编译器被集成在了一个安装包内，而对于MacOS平台，C/C++编译器和Fortran编译器被分装成两个安装包。

在下载页面下载Intel Parallel Studio XE Composer Edition for Fortran macOS，并在安装时提交Intel提供的序列号即可完成安装。

默认的安装路径为`/opt/intel`


# 配置

## 准备工作

在使用之前，首先需要运行脚本来设置环境变量。

为了运行储存在安装目录下的环境变量设置脚本`/opt/intel/bin/compilervars.sh`，需要在终端中运行：

```
$ source /opt/intel/bin/compilervars.sh <arg>
```

其中`<arg>`可以使用下面两种参数：

* `intel64`：适用于Intel 64位架构
* `ia32`：适用于IA-32架构

## 在Xcode中运行Fortran

为了能够在Xcode中编译Fortran语言程序，需要对Xcode进行一些设置：

1. 打开或者新建一个 命令行工具应用 工程，在选择语言时选择C或C++；
![新建工程](https://software.intel.com/sites/default/files/did_feeds_images/A8B3860F-5287-4E4C-AC9E-1C8AF07194E6/A8B3860F-5287-4E4C-AC9E-1C8AF07194E6-imageId=C85BB269-0409-4261-BE9B-087EF6CCF016.png)

2. 在`Build Rules`选项卡中添加新的编译规则：`Process`->`Fortran source files`，`Using`->`Intel® Fortran Compiler Latest Release`；如果Xcode中看不到关于Intel® Fortran Compiler的选项，可以参考[https://software.intel.com/en-us/node/677955](https://software.intel.com/en-us/node/677955)
![修改编译规则](https://software.intel.com/sites/default/files/did_feeds_images/A8B3860F-5287-4E4C-AC9E-1C8AF07194E6/A8B3860F-5287-4E4C-AC9E-1C8AF07194E6-imageId=685680A1-8434-4C8C-88F1-3AFF4A4E76D7.png)

3. 将工程中原本的C或C++源代码文件清楚，并添加Fortran源代码文件`Fortran Fixed Format File`或`Fortran Free Format File`；

## Troubleshooting

如果对编译好的可执行文件运行时，在输出窗口出现如下错误：
```
dyld: Library not loaded: @rpath/libmkl_intel_lp64.dylib
```
说明未对动态库进行设置。可以通过下面两种方法来解决这一错误：

1. 采用静态库进行编译。

在`Build Settings`中找到`Intel® Fortran Compiler Latest Release - Runtime`条目下的`Intel Runtime Libraries`，将选项从`Default`或`Dynamic Libraries`改为`Static Libraries`。

2. 如果需要采用动态库或共享库进行编译，就需要对环境变量`DYLD_LIBRARY_PATH`进行设置。具体设置方法可以参考[https://software.intel.com/en-us/node/677959](https://software.intel.com/en-us/node/677959)


# 延伸阅读

* [Intel Parallel Studio XE](https://software.intel.com/en-us/intel-parallel-studio-xe) / [Documentation for Intel Parallel Studio XE Support](https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation)
* [Intel Fortran Compiler](https://software.intel.com/en-us/fortran-compilers) / [Documentation for Intel Fortran Compiler Support](https://software.intel.com/en-us/fortran-compilers-support/documentation)
* [Intel® Software Documentation Library](https://software.intel.com/en-us/intel-software-technical-documentation)
* [Intel® Fortran Compiler 17.0 Developer Guide and Reference](https://software.intel.com/en-us/intel-fortran-compiler-17.0-user-and-reference-guide) / [Getting Started](https://software.intel.com/en-us/node/677894) / [Using Xcode (OS X) ](https://software.intel.com/en-us/node/677953)
* [Getting Started with Intel® Parallel Studio XE Composer Edition for OS X*](https://software.intel.com/en-us/get-started-with-parallel-studio-xe-for-osx)
* [Parallel Studio XE 2017: Getting Started with the Intel Fortran Compiler 17.0 for OS X](https://software.intel.com/en-us/get-started-with-fortran-compiler-17.0-for-macos-parallel-studio-xe-2017)
* [Intel Parallel Studio XE 2017 Update 4 for macOS Installation Guide and Release Notes](https://software.intel.com/sites/default/files/managed/86/c3/PSXE2017Update4_Release_Notes_en_US_OSX.pdf)


* [Quick Link Intel® MKL In Xcode* IDE: A Fortran Sample](https://software.intel.com/en-us/articles/quick-link-intel-mkl-in-xcode-ide-a-fortran-sample/)
* [How to link application against Intel MKL using XCode IDE](https://software.intel.com/en-us/articles/how-to-link-application-against-intel-mkl-using-xcode-ide)
* [Compiling and linking MKL with Xcode*](https://software.intel.com/en-us/articles/intel-math-kernel-library-for-mac-os-compiling-and-linking-with-xcode)
