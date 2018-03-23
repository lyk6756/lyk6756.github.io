---
layout: post
title:  "在MacOS平台上使用Eclipse/Photran搭建Fortran开发环境"
date:   2017-12-30
author: 李宇琨
categories: Fortran
tags: FEAP
cover:  "https://pnqw0q-dm2305.files.1drv.com/y4m0jG-CG3_RC_0fyGfFF9O0SzNsiL2XSMzQyLFdLcXXnuAAPWW7uwirx8cM_pVh09OCc4Z66Ug2TSm7QTUHtNBGJ3u89-AEVEF9anLU-f-LBWRihBjnI_Q2JI76fVEvpu2_kB72BfXeuBKPshY9gdJunSal0h6UdcIvsCh-qFHH1tb8SvFPyLBJMje_Q0xytHtlncfdP0DkjROFhRbtKnFtA?width=1687&height=809&cropmode=none"
---


# 系列文章

* [在MacOS下搭建Fortran开发环境](https://lyk6756.github.io/fortran/2017/08/04/Fortran_for_MacOS.html)


# 前言

[Eclipse](http://www.eclipse.org/)是一款著名的跨平台开源集成开发环境（IDE）。Eclipse的本身只是一个框架平台，最初基于Java语言开发，目前通过插件已经能够支持C++、Fortran、Python、PHP等各种语言的开发工具。

[Photran](http://www.eclipse.org/photran/)就是一款基于Eclipse和[CDT(C/C++ Development Tooling)](http://www.eclipse.org/cdt/)的Fortran集成开发环境。Photran 9.1于2015年6月24日与Eclipse 4.5(Mars)一起发布。Photran支持Fortran 77-2008。Photran目前是[Eclipse Parallel Tools Platform(PTP)](http://www.eclipse.org/ptp/)的一个组件。

# 部署平台

* macOS High Sierra 10.13.2

* gcc version 7.2.0
* gdb version 8.0.1

* Java(TM) SE Runtime Environment (build 9.0.1+11)

* Eclipse Oxygen.2 (4.7.2) 
	* CDT
	* PTP


# 准备工作

由于Eclipse是基于Java语言开发的，首先需要确定系统中有Java运行环境。在终端中运行指令

```
java -version
```

就能够获取系统中安装的Java版本号。如果提示未安装相应环境，可以前往[http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)来获取最新版本的Java运行环境。或者直接使用`brew cask`来进行安装：

```
brew cask install java
```

另外，如果要编译和构建Fortran应用程序，则必须在系统路径中包含make程序（如[GNU Make](http://www.gnu.org/software/make/)）和Fortran编译器（如[gfortran](https://gcc.gnu.org/fortran/)，GNU Fortran编译器）。要调试Fortran应用程序，则必须安装[GNU GDB](http://www.gnu.org/software/gdb/)。关于GDB的详细设置将在后面讨论。

可以直接采用`brew`进行安装：

```
brew install cmake gcc gdb
```


# 安装PTP

可以直接前往[Eclipse package downloads page](http://www.eclipse.org/downloads/eclipse-packages/)下载`Eclipse for Parallel Application Developers`，这其中就包含了Photran，C/C++ Development Tools，Eclipse Parallel Tools Platform以及其他的一些插件。

接下来，为了能够在启动Eclipse时能够成功找到PATH，还需要以下操作：

1. 在应用程序中找到`Eclipse.app`，右键选择`显示包内容`；
2. 打开`Contents`文件，修改`Info.plist`中的内容；
3. 在其中的`<dict>`行和`<key>CFBundleExecutable</key>`行之间添加一个LSEnvironment路径。如下所示：

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">

<dict>
        <key>LSEnvironment</key>
                <dict>
                        <key>PATH</key>
                        <string>/usr/local/gfortran/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin</string>
                </dict>
        <key>CFBundleExecutable</key>
                <string>eclipse</string>
...
```

其中`<string>`标签中就是添加的`PATH`路径。

5. 在终端中执行以下命令：

```
/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -v -f /Applications/eclipse/eclipse.app
```


# 设置gdb调试器

[GDB](http://www.gnu.org/software/gdb/)是GNU项目中的一个程序调试工具。广泛应用在UNIX/LINUX操作系统下。

对于最新的macOS来说，操作系统的保护机制`System Integrity Protection(SIP)`使得GDB无法直接访问系统内核。关于SIP的详细介绍可以参见[这里](https://developer.apple.com/library/content/documentation/Security/Conceptual/System_Integrity_Protection_Guide/ConfiguringSystemIntegrityProtection/ConfiguringSystemIntegrityProtection.html#//apple_ref/doc/uid/TP40016462-CH5-SW1)。在使用`Homebrew`完成`gdb`的安装之后会提示：

```
gdb requires special privileges to access Mach ports.
You will need to codesign the binary. For instructions, see:

  https://sourceware.org/gdb/wiki/BuildingOnDarwin

On 10.12 (Sierra) or later with SIP, you need to run this:

  echo "set startup-with-shell off" >> ~/.gdbinit
```

提示需要对GDB进行证书授权才能够正常使用gdb调试程序。

1. 启动`钥匙串访问`(`Keychain Access`)应用程序，打开菜单：钥匙串访问(Keychain Access)>证书助理(Certificate Assistant)>创建证书...(Creat a Certificate...)；
2. 名称(Name)填写`gdb-cert`，身份类型(Identity Type)选择`自签名根证书`(`Self Signed Root`)，证书类型选择`代码签名`(`Code Signing`)，并勾选`让我覆盖这些默认值`(`Let me override defaults`)；
3. 接下来连续点击`继续`，在指定用于该证书的位置时(Specify a Location For The Certificate)，选择钥匙串(Keychain)为`系统`(`System`)；

如果无法将证书创建在`系统`钥匙串下，可以先将证书创建在`登录`钥匙串下，然后将其导出后再导入进`系统`钥匙串下。

4. 在刚创建的证书`gdb-cert`上点击右键，选择`显示简介`(`Get Info`)，将信任选项卡下的`使用此证书时:`更改为`始终信任`；
5. 重启电脑；
6. 对证书进行签名。打开终端，在其中输入指令：

```
codesign -s gdb-cert /usr/local/bin/gdb
```

7. 对于macOS 10.12(Sierra)版本以上的操作系统，还需要禁止gdb从shell中启动调试程序。可以直接通过创建`.gdbinit`文件来实现：

```
echo "set startup-with-shell off" >> ~/.gdbinit
```

## Troubleshooting

如果在执行了以上步骤之后仍然不能够顺利运行gdb，可以考虑关闭SIP：

1. 重启系统并按住`Command`+`R`，进入恢复模式；
2. 在使用工具中启动终端，并执行命令`csrutil disable`;
3. 关闭终端并重启系统，重新创建证书并签名。

在终端中执行`csrutil status`可以查看当前SIP的运行情况；重复以上步骤执行`csrutil enable`可以重新开启SIP。


# 延伸阅读

* [Eclipse](http://www.eclipse.org/)
* [Photran - An Integrated Development Environment and Refactoring Tool for Fortran](http://www.eclipse.org/photran/)
* [Eclipse CDT (C/C++ Development Tooling)](http://www.eclipse.org/cdt/)
* [Eclipse Parallel Tools Platform(PTP)](http://www.eclipse.org/ptp/)
* Eclipse wiki: [PTP/Photran/](http://wiki.eclipse.org/PTP/Photran/) / [PTP/photran/Documentation](http://wiki.eclipse.org/PTP/photran/documentation) / [Photran 9.1 Installation Guide](http://wiki.eclipse.org/PTP/photran/documentation/photran9installation)
* [PTP/release notes](http://wiki.eclipse.org/PTP/release_notes)
* [GNU GDB](http://www.gnu.org/software/gdb/) / [BuildingOnDarwin - GDB Wiki](https://sourceware.org/gdb/wiki/BuildingOnDarwin)
* [gdb error with Sierra OS upgrade - stackoverflow](https://stackoverflow.com/questions/39794587/gdb-error-with-sierra-os-upgrade)
* [Installing GDB on MacOS Sierra - Oscar Alsing](https://www.oscaralsing.com/installing-gdb-on-macos-sierra/)
* [mac上eclipse用gdb调试](https://www.cnblogs.com/yinxiangpei/articles/3897701.html)
* [Install gdb on macOS Sierra 10.12.2 - YouTube](https://www.youtube.com/watch?v=AoDSUadbl-M)
* [How To Install Fortran Eclipse MacOS](https://www.youtube.com/watch?v=HakTEhU3Q9U)
* [Creating a Fortran project in Eclipse - YouTube](https://www.youtube.com/watch?v=IjjZjITwbXE)
