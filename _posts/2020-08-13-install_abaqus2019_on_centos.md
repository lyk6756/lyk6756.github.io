---
layout: article
title:  "在CentOS上安装ABAQUS 2019并搭建子程序开发环境"
author: 李宇琨
key: 20200813
lang: zh
tags: ABAQUS Fortran Linux
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://m2qziq.dm.files.1drv.com/y4mzZWEjjAaNARefyxVkKlxgwEqMB9rIn39wANVzd5uOzUAzLqeuSf42u3C7tSgXdUgrJZgR4-vcrINIiY7YVn1tMjgnuI3pF6Z8KzW6Fb318P6UCPtiZd_k0QYcsEUMmDeeJCoTGPhJz3tIsnBGikod3UQNlytoJym4wcdypIwKdDWVnWdaMzOnBusQVoIn1N71leU_ISdOrv3cxIijF73MQ?width=870&height=400&cropmode=none"
---

## 系列文章

* [在命令行窗口中运行ABAQUS](https://lyk6756.github.io/2020/08/01/ABAQUS_obj.html)
* [在Win10下搭建Abaqus子程序开发环境](https://lyk6756.github.io/2017/12/12/Link_Abaqus_with_Fortran.html)
* [Install Abaqus2016 on Linux (Ubuntu 16.04 64bit)](https://lyk6756.github.io/2016/11/18/install_abaqus2016_on_linux.html)

## 部署平台

* CentOS Linux release 7.8.2003

* ABAQUS 2019

* Intel Parallel Studio XE 2019

## 安装前的准备

首先，对系统中已安装的软件包进行更新：

```shell
sudo yum update
sudo yum upgrade
```

然后进行必要环境的安装：

```shell
sudo yum install ksh
sudo yum install redhat-lsb
sudo yum install gcc
sudo yum install gcc-c++
sudo yum install gcc-gfortran
sudo yum install openmotif
```

## 安装证书服务器

破解文件的目录如下：

```text
Crack
├── SSQ_UniversalLicenseServer_Core_<release-date>.zip
│   └── SolidSQUAD_License_Servers
│       └── ...
├── SSQ_UniversalLicenseServer_Module_DSSimulia_<release-date>.zip
│   └── Vendors
│       └── DSSimulia
│           └── ...
└──Readme.txt
```

如果从未安装过SolidSQUAD License Server：

* 将`SSQ_UniversalLicenseServer_Core_<release-date>.zip`中的`SolidSQUAD_License_Servers`文件夹解压至目标文件夹，例如`/opt/DassaultSystemes/SolidSQUAD_License_Servers`；

* 将`SSQ_UniversalLicenseServer_Module_DSSimulia_<release-date>.zip`中的`Vendors`文件夹解压至刚才的`SolidSQUAD_License_Servers`文件夹中；

* 运行 `SolidSQUAD_License_Servers`文件夹中的`install_or_update.sh`，等待脚本完成；

```shell
sudo ksh ./install_or_update.sh
```

### Troubleshooting

#### 运行`install_or_update.sh`时报错

```shell
...
Cannot find a source for symlink to /lib/ld-lsb.so.3! Exiting...
```

使用`yum provides`命令查找缺失的库文件：

```shell
yum provides /lib/ld-lsb.so.3
```

返回：

```shell
...
redhat-lsb-core-4.1-47.el8.i686 : LSB Core module support
Repo        : AppStream
Matched from:
Filename    : /lib/ld-lsb.so.3
```

安装缺失的库文件：

```shell
sudo yum install redhat-lsb-core
```

#### 运行`install_or_update.sh`时系统日志`journalctl -xe`报错

```text
SELinux is preventing (lmgrd) from execute access on the file lmgrd.
...
```

SELinux系统是强制访问控制(MAC)安全系统，它拒绝了证书服务器的运行。`getenforce`命令用于查看SELinux运行状态；`setenforce 0`命令用于临时关闭SELinux，重启后失效；永久关闭SELinux，需要修改其配置文件`/etc/selinux/config`，将`SELINUX=enforcing`改为`SELINUX=disabled`，保存后退出，并重启系统。

## 运行Abaqus安装程序

```shell
sudo ksh 1/StartGUI.sh
```

选择需要安装的组件：

* Extended Product Documentation
* Abaqus Simulation Services
* Abaqus Simulation Services CAA API
* Abaqus/CAE
* fe-safe
* Tosca
* Isight

**注意**：*不要*安装自带的FLEXnet License Server

在安装Abaqus/CAE时，
Extended Product Documentation的安装目录：`/opt/DassaultSystemes/SIMULIA2019doc`

Abaqus Simulation Services及Abaqus Simulation Services CAA API的安装目录：`/opt/DassaultSystemes/SimulationServices/V6R2019x`

Abaqus/CAE的安装目录：`/opt/DassaultSystemes/SIMULIA/CAE/2019`

CAE Commands的安装目录：`/opt/DassaultSystemes/SIMULIA/Commands`

CAE external plugins的安装目录：`/opt/DassaultSystemes/SIMULIA/CAE/plugins/2019`

fe-safe的安装目录：`/opt/DassaultSystemes/SIMULIA/fe-safe/2019`

Tosca的安装目录：`/opt/DassaultSystemes/SIMULIA/Tosca/2019`

Isight的安装目录：`/opt/DassaultSystemes/SIMULIA/Isight/2019`

### Troubleshooting

#### Ubuntu等Linux发行版无法直接运行安装程序

由于ABAQUS默认只支持一下几种Linux发行版：Red Hat Enterprise Linux，Centos和SuSE Linux Enterprise Server。因此首先我们需要使安装程序绕过系统监测：

```shell
export DSYAuthOS_`lsb_release -si`=1
export DSY_Force_OS=linux_a64
export NOLICENSECHECK=true
```

然后运行图形安装界面：

```shell
ksh 1/StartGUI.sh
```

或直接运行命令：

```shell
cd <mounted CD folder>/1/
export DSYAuthOS_`lsb_release -si`=1 && export DSY_Force_OS=linux_a64 && ksh ./StartGUI.sh
```

参考：

* [Kevin-Mattheus-Moerman/Abaqus-Installation-Instructions-for-Ubuntu: Abaqus 2018 Installation Instructions for Ubuntu 18.04](https://github.com/Kevin-Mattheus-Moerman/Abaqus-Installation-Instructions-for-Ubuntu)

#### 运行`StartGUI.sh`时报错

```text
...
error while loading shared libraries: libz.so ...
```

安装包`zlib`中提供依赖的库文件`libz.so.1`，安装命令：

```shell
sudo yum install zlib
```

然后分别将目录`/usr/lib/`及`/usr/lib64/`下的库文件`libz.so.1`复制并重命名为`libz.so`：

```shell
cp libz.so.1 libz.so
```

#### 安装ABAQUS/CAE时，在选择证书服务器（License Server Configuration）为SIMULIA FLEXnet后点击下一步时报错

```shell
Stdout:
Stderr: unzip: loadlocale.c:130: _nl_intern_locale_data: Assertion `cnt < (sizeof (_nl_value_type_LC_TIME) / sizeof (_nl_value_type_LC_TIME[0]))' failed.

Action LaunchAppAction from feature CODE\linux_a64\SMATocLicPanel failed.
Action ID: unzip_siteIDandDslsStat
```

可以在安装中跳过证书设置，这并不影响软件的安装。在完成安装之后，将`/opt/DassaultSystemes/SimulationServices/V6R2019x/linux_a64/SMA/site/custom_v6.env`中的

```python
license_server_type=DSLS
dsls_license_config="/var/DassaultSystemes/Licenses/DSLicSrv.txt"
```

改为

```python
license_server_type=FLEXNET
abaquslm_license_file="27800@localhost"
# license_server_type=DSLS
# dsls_license_config="/var/DassaultSystemes/Licenses/DSLicSrv.txt"
```

可以使用以下指令来查看证书状态：

```shell
/opt/DassaultSystemes/SIMULIA/Commands/abaqus licensing ru
```

参考：[Error during installation · Issue #2 · Kevin-Mattheus-Moerman/Abaqus-Installation-Instructions-for-Ubuntu](https://github.com/Kevin-Mattheus-Moerman/Abaqus-Installation-Instructions-for-Ubuntu/issues/2)

## 安装Intel Fortran编译器

Intel Parallel Studio XE 2019支持的操作系统有：

* CentOS* 6 (Intel(R) 64), 7 (Intel(R) 64)
* Debian* 8 (Intel(R) 64), 9 (Intel(R) 64)
* Fedora* 27 (Intel(R) 64), 28 (Intel(R) 64)
* Red Hat Enterprise Linux* 6 (Intel(R) 64), 7 (Intel(R) 64)
* SUSE Linux Enterprise Server* 12 (Intel(R) 64), 15 (Intel(R) 64)
* Ubuntu* 16.04 (Intel(R) 64), 18.04 (Intel(R) 64)

安装目录：`/opt/intel`

安装文件会提示需要安装以下32位的共享库文件：

```shell
sudo yum install libstdc++.i686
sudo yum install glibc glibc.i686
sudo yum install libgcc libgcc.i686
```

安装完成后，还需要使用其提供的脚本进行环境设置，在`~/.bashrc`中添加：

```shell
source <install_dir>/bin/compilervars.sh intel64
export PATH=$PATH:/opt/intel/bin
```

重启命令行后就可以在任意目录下使用`ifort -v`查看intel fortran编译器的版本了。

使用`whereis ifort`指令可以查看其所在位置，默认路径为`/opt/intel/bin/ifort`。

## 配置Abaqus运行环境

### 运行Abaqus/CAE

当系统开机或重启后，证书服务器将会自动启动。手动重启服务器：

```shell
sudo ksh /opt/DassaultSystemes/SolidSQUAD_License_Servers/install_or_update.sh
```

以管理员身份使用以下命令来启动Abaqus/CAE：

```shell
/opt/DassaultSystemes/SIMULIA/Commands/abaqus cae
```

或

```shell
/opt/DassaultSystemes/SIMULIA/Commands/abq2016 cae
```

如果出现图形渲染问题，可以在启动指令后添加`-mesa`来禁止硬件图形加速渲染，参考：[Hardware acceleration (all platforms)](https://abaqus-docs.mit.edu/2017/English/SIMACAEILGRefMap/simailg-c-viewcusthardware.htm)

如果出现CAE窗口透明的情况，可以在启动指令前添加`XLIB_SKIP_ARGB_VISUALS=1`。

打开CAE后，需要更改工作目录到/home下的任意路径。放置在/home下的文件才能够在普通权限下进行读写，如果没有更改工作路径，ABAQUS会报错sim文件不存在等问题，无法进行计算。

使用以下指令设置默认的工作目录：

```shell
export TMPDIR=~/temp
```

### 创建快捷方式

使用以下几种方式中的任意一种来使`abaqus`指令得到全局访问：

* 修改`~/.bashrc`，使用`export`将命令所在目录加入环境变量：

```shell
export PATH=$PATH:/opt/DassaultSystemes/SIMULIA/Commands
```

* 修改`~/.bashrc`，使用`alias`添加简化指令：

```shell
alias abaqus='/opt/DassaultSystemes/SIMULIA/Commands/abaqus'
```

* 在`/usr/bin/`中创建同步链接：

```shell
sudo ln /opt/DassaultSystemes/SIMULIA/Commands/abaqus /usr/bin/abaqus
```

### 连接Intel Fortran编译器

修改`~/.bashrc`，添加Intel Fortran共享库的路径：

```shell
export LD_LIBRAY_PATH=$LD_LIBRAY_PATH:/opt/intel/compilers_and_libraries/linux/lib/intel64
```

综上，只需在`~/.bashrc`文件中增加如下内容，即可完成对Intel Fortran编译器和Abaqus运行环境的设置：

```shell
# User specific aliases and functions

# ifort env. config.
source /opt/intel/bin/compilervars.sh intel64
export PATH=$PATH:/opt/intel/bin

# abaqus env. config.
export PATH=$PATH:/opt/DassaultSystemes/SIMULIA/Commands # global access to abaqus commands
export LD_LIBRAY_PATH=$LD_LIBRAY_PATH:/opt/intel/compilers_and_libraries/linux/lib/intel64 # link shared libraries
```

重启命令行后，使用以下指令来测试编译器的运行情况：

```shell
abaqus info=system
abaqus verify -user_std
```

参考：

* [Linking Intel fortran compiler to ABAQUS and using UMAT - Saiwal's HomePage](http://home.iitk.ac.in/~saiwal/engineering/intel-abaqus/)
* [Linking Abaqus/Fortran for running subroutine in UBUNTU (linux)-Abaqus GUI Graphical issue(Transparent-/transluscent) - iMechanica](https://imechanica.org/node/13804)
* [how to link Fortran with Abaqus CAE 6.14 in Redhat linux terminal? - Stack Overflow](https://stackoverflow.com/questions/44133632/how-to-link-fortran-with-abaqus-cae-6-14-in-redhat-linux-terminal)

---

## 延伸阅读

* [Simulia Established Products 2019 Installation Guide](https://1drv.ms/b/s!Alob-1bHMoykm0VL_XlPEyE9rk2D?e=cD6RI3)

* [Solid-Mechanics/Install-ABAQUS-on-Ubuntu: Install ABAQUS 6.14-5 on Ubuntu 16.04 64bit](https://github.com/Solid-Mechanics/Install-ABAQUS-on-Ubuntu)
* [imirzov/Install-Abaqus-2019-on-Ubuntu-18.04-LTS: Instruction manual to install Abaqus 2019 on Ubuntu 18.04 LTS](https://github.com/imirzov/Install-Abaqus-2019-on-Ubuntu-18.04-LTS)

* [ABAQUS 2018 and Fortran Compilers on Ubuntu 18.04LTS - PDF](http://coquake.eu/wp-content/uploads/2019/02/Abaqus18_on_Ubuntu18.04LTS.pdf)
* [Using gfortran compiler for user subroutines in ABAQUS 2016/2017 - Saiwal's HomePage](http://home.iitk.ac.in/~saiwal/engineering/abaqus2016-2017-gfortran-compiler/)

* [Useful commands, tips for using ABAQUS over command-line in linux - Saiwal's HomePage](http://home.iitk.ac.in/~saiwal/engineering/useful-commands-tips-for-using-abaqus-over-command-line-in-linux/)
* [The ABAQUS FAQ](http://www-h.eng.cam.ac.uk/help/programs/fe/abaqus/faq68/abaqusf2.html#Introductions)
