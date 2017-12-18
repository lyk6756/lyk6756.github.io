---
layout: post
title:  "在Linux平台上安装配置FEAP"
date:   2017-12-15
author: 李宇琨
categories: Fortran
tags: FEAP
cover:  "https://pnqw0q-dm2305.files.1drv.com/y4m0jG-CG3_RC_0fyGfFF9O0SzNsiL2XSMzQyLFdLcXXnuAAPWW7uwirx8cM_pVh09OCc4Z66Ug2TSm7QTUHtNBGJ3u89-AEVEF9anLU-f-LBWRihBjnI_Q2JI76fVEvpu2_kB72BfXeuBKPshY9gdJunSal0h6UdcIvsCh-qFHH1tb8SvFPyLBJMje_Q0xytHtlncfdP0DkjROFhRbtKnFtA?width=1687&height=809&cropmode=none"
---


# 系列文章

* [在Win10下利用VS2017及Intel Fortran Compiler安装配置FEAP](https://lyk6756.github.io/fortran/2017/09/07/install_FEAP_on_windows.html)


# 前言

[FEAP](http://projects.ce.berkeley.edu/feap/)(a Finite Element Analysis Program)，是由美国加州大学伯克利分校土木与环境工程系的Robert L. Taylor教授领导开发的通用有限元分析程序。整个程序由Fortran语言编写，并能够直接获取到源代码。是科研工作者的有力武器。

由于开发者提供了程序的源代码，FEAP可以通过编译部署在Linux/Unix系统上。同时，FEAP能够利用[PETSc](http://www.mcs.anl.gov/petsc/) 在Linux/Unix平台上实现并行计算。

PETSc(Portable, Extensible Toolkit for Scientific Computation)是由美国阿贡国家实验室开发的可移植可扩展科学计算工具箱，主要用于在分布式存储环境高效求解偏微分方程组及相关问题。线性方程组求解器是PETSc的核心组件之一。PETSc用C语言开发，支持多种语言进行代码编写，包括Fortran 77/90、C、C++和Python等。


# 部署平台

* Ununtu 16.04.3 LTS "xenial" (GNU/Linux 4.10.0-28-generic x86_64)

* GNU GCC / Gfortran 5.4.0 (Ubuntu 5.4.0-6ubuntu1~16.04.5)

* PETSc 3.7.7

* FEAP 8.5


# 准备工作

首先对系统上的apt-get源进行更新和升级。运行：

```shell
sudo apt-get update
sudo apt-get upgrade
```

为了能够对源代码进行编译，需要在系统中安装必要的编译器。运行：

```
sudo apt-get install build-essential
sudo apt-get install gfortran
sudo apt-get install cmake
sudo apt-get install libblas-dev liblapack-dev
```

为了实现并行计算，PETSc的运行需要MPI(Message Passing Interface)库。这里我们选择安装MPICH：

```shell
sudo apt-get install mpich
sudo apt-get install libmpich-dev
```

PETSc推荐在系统上安装valgrind，一款内存调试工具：

```
sudo apt-get install valgrind
```

由于FEAP的运行中需要X Window环境，需要安装必要的X11开发包：

```
sudo apt-get install libx11-dev
sudo apt-get install xorg-dev
```

FEAP在显示中使用了Helvetica字体，而Ubuntu默认并没有安装该字体，因此需要另外安装：

```
sudo apt-get install xfonts-75dpi xfonts-100dpi
```

可以通过执行命令`xlsfonts | grep helvetica`来查询是否已经安装了该字体。


# 安装编译PETSc

从PETSc官网下载到源代码的压缩包解压后，在其中创建编译文件`BuildPETSc`

```shell
#!/bin/bash

function prtPaths {
    echo "PETSC_DIR=  $(echo $PETSC_DIR)"
    echo "PETSC_ARCH= $(echo $PETSC_ARCH)"
}

export PETSC_DIR=/home/lyk/Documents/petsc-3.7.7

cd $PETSC_DIR

if [[ $1 == 'opt' ]] ; then
    # Building from the beggining - Optimized
    export PETSC_ARCH=gnu-opt
    prtPaths
    ./configure \
    --with-cc=/usr/bin/mpicc \
    --with-fc=/usr/bin/mpif90 \
    --with-cxx=/usr/bin/mpicxx \
    --with-mpiexec=/usr/bin/mpiexec \
    --with-debugging=0 \
    --with-shared-libraries=0 \
    --download-spooles \
    --download-parmetis \
    --download-superlu \
    --download-superlu_dist \
    --download-prometheus \
    --download-ml \
    --download-hypre \
    --download-metis \
    --download-mumps \
    --download-scalapack \
    --download-blacs \
    --download-fblaslapack \
    --download-suitesparse
    
elif [[ $1 == 'dbg' ]] ; then
    # Building from the beggining - With Debugging
    export PETSC_ARCH=gnu-dbg
    prtPaths
    ./configure \
    --with-cc=/usr/bin/mpicc \
    --with-fc=/usr/bin/mpif90 \
    --with-cxx=/usr/bin/mpicxx \
    --with-mpiexec=/usr/bin/mpiexec \
    --with-debugging=1 \
    --with-shared-libraries=0 \
    --download-spooles \
    --download-parmetis \
    --download-superlu \
    --download-superlu_dist \
    --download-prometheus \
    --download-ml \
    --download-hypre \
    --download-metis \
    --download-mumps \
    --download-scalapack \
    --download-blacs \
    --download-fblaslapack \
    --download-suitesparse
    
fi

make all
make test
```

根据[FEAP Parallel Manual: v8.5](http://projects.ce.berkeley.edu/feap/parmanual85.pdf)给出的安装说明，需要在编译文件中给出源文件的路径`PETSC_DIR`，编译器`with-cc`、`with-fc`、`with-cxx`和`with-mpiexec`，以及下载配套的外部宏包指令`download`。这里安装了:

* [Spooles](http://www.netlib.org/linalg/spooles/spooles.2.2.html): SParse Object Oriented Linear Equations Solver 稀疏矩阵线性解析库
* [ParMETIS](http://glaros.dtc.umn.edu/gkhome/metis/parmetis/overview): Parallel Graph Partitioning and Fill-reducing Matrix Ordering
* [SuperLU](http://crd-legacy.lbl.gov/~xiaoye/SuperLU/) & [SuperLU_DIST](http://crd-legacy.lbl.gov/~xiaoye/SuperLU/)
* [Prometheus](https://prometheus.io/): Monitoring system & time series database
* [MPICH](http://www.mpich.org/): High-Performance Portable MPI
* [ML](https://trilinos.org/packages/ml/): Multi Level Preconditioning Package
* [Hypre](https://computation.llnl.gov/projects/hypre-scalable-linear-solvers-multigrid-methods): The Parallel High Performance Preconditioners
* [METIS](http://glaros.dtc.umn.edu/gkhome/metis/metis/overview): Serial Graph Partitioning and Fill-reducing Matrix Ordering
* [MUMPS](http://mumps.enseeiht.fr/): MUltifrontal Massively Parallel Sparse direct Solver
* [ScaLAPACK](http://www.netlib.org/scalapack/index.html): Scalable Linear Algebra PACKage
* [blacs](http://www.netlib.org/blas/): Basic Linear Algebra Subprograms
* fblaslapack
* [SuiteSparse](http://faculty.cse.tamu.edu/davis/suitesparse.html): a suite of sparse matrix software

其中，MUMPS需要ScaLapack和BLACS的支持。用户可以根据自己的需要定制其他的安装附件。

在完成编译文件的编辑之后，执行以下指令来为其赋予执行权限：

```
chmod +x BuildPETSc
```

接下来就可以在源文件目录下直接运行编译文件来对源文件进行编译了：

```
./BuildPETSc opt
```

在完成安装之后，安装进程还会自动对安装结果进行检测（`make test`）。还可以执行下面指令来评估计算性能：

```
make PETSC_DIR=/home/lyk/Documents/petsc-3.7.7 PETSC_ARCH=gnu-opt streams
```

更详细的安装说明可以参考[http://www.mcs.anl.gov/petsc/documentation/installation.html](http://www.mcs.anl.gov/petsc/documentation/installation.html)


# 安装编译FEAP

在安装编译FEAP之前，首先要添加源文件路径的环境变量。对于bash，在`.bashrc`文件中添加：

```
export PETSC_DIR=/home/lyk/Documents/petsc-3.7.7
export PETSC_ARCH=gnu-opt
export FEAPHOME8_5=/home/lyk/Documents/FEAP/ver85
```

## 编辑makefile.in

打开包含有所有源文件的FEAP文件夹`ver85`，编辑其中的`makefile.in`文件：

1. 如果要在编译中使用ARPACK，需要将`ARCHIVELIB`和`ARPACKLIB`取消注释；
2. 对于64位操作系统，在`FINCLUDE`中使用`integer8`；
3. 对于Ubuntu，在`CINCLUDE`中增加`\usr\include`；
4. 对于并行计算的编译器，`FFMPI`和`FFE2`设置为`/usr/bin/mpif90`，`CCMPI`和`CCE2`设置为`/usr/bin/mpicc`；
5. 对于加载选项`LDOPTIONS`，将其修改为`-L/usr/lib/x86_64-linux-gnu -lX11 -lblas -llapack -lm`；
6. 对于加载选项`LDOPTIONSFE2`，将其修改为`-L/usr/lib/mpich/lib $(LDOPTIONS)`。

完整的`makefile.in`文件内容如下所示：

```shell
#------------------------------------------------------------------------
# To use this makefile the path for "$(FEAPHOME8_5)" must be set using
#   setenv FEAPHOME8_5=/....            (in .chrc or .tchrc)  or
#   export FEAPHOME8_5=/....            (in .bashrc or file used)
# N.B. Information after the slash defines to FEAP directories. 
#------------------------------------------------------------------------
# Set include file type to use: integer4 for 32 bit machines
#                               integer8 for 64 bit machines

# Use of integer8 files sets pointers to be integer*8 and all other
# integers to be integer*4.  This limits the size of any single array to
# an integer*4 value (approx 4 GByte).

# Use of integer4 files sets all integers (including pointers) to be
# integer*4.

# N.B. If a compiler option is used that sets ALL integers to be
#      integer*8, it is necessary to reset the ipr parameter to 'ipr = 1'
#      in file 'feap85.f' located in the 'main' directory.
#
#------------------------------------------------------------------------
# arpack archive library (uncomment to use ARPACK eigensolver)
#  ARCHIVELIB = $(FEAPHOME8_5)/packages/arpack/archive/libarchive.a
# arpack serial library (uncomment to use ARPACK eigensolver)
#  ARPACKLIB = $(FEAPHOME8_5)/packages/arpack/libarpack.a

# No one should need these as you should have native libraries already
# (uncomment if you need a bare bones LAPACK and BLAS)
# Local lapack library (use if you do not have lapack already)
#  LAPACKLIB = $(FEAPHOME8_5)/packages/lapack/liblapack.a
# Local blas library
#  BLASLIB   = $(FEAPHOME8_5)/packages/blas/libblas.a    

#------------------------------------------------------------------------
# Location of feap include files

# Fortran includes
# (select either integer*4 or integer*8 based on your machine, add
#  additional -I directories as needed, for example -I/opt/include in place of -I/sw/include)

# (integer*4 pointer case)
# FINCLUDE = $(FEAPHOME8_5)/include -I$(FEAPHOME8_5)/modules -I$(FEAPHOME8_5)/include/integer4 

# (integer*8 pointer case)
  FINCLUDE = $(FEAPHOME8_5)/include -I$(FEAPHOME8_5)/modules -I$(FEAPHOME8_5)/include/integer8 

# C includes (some common options, pick as appropriate)
# CINCLUDE = /opt/local/include
# CINCLUDE = /usr/X11R6/include
  CINCLUDE = /usr/include

# IGA include file locations (no need to change)
  NINCLUDE = $(FEAPHOME8_5)/igafeap/include -I$(FEAPHOME8_5)/igafeap/modules

#------------------------------------------------------------------------
# Which MPI compilers to use for FE2 and parallel FEAP
# (Set to compiler names available on your computer)

# Parallel MPI Build

FFMPI = /usr/bin/mpif90
CCMPI = /usr/bin/mpicc

#  FFMPI = $(PETSC_DIR)/$(PETSC_ARCH)/bin/mpif90
#  CCMPI = $(PETSC_DIR)/$(PETSC_ARCH)/bin/mpicc

# Parallel FE2 Build

FFE2 = /usr/bin/mpif90
CCE2 = /usr/bin/mpicc

#  FFE2 = $(PETSC_DIR)/$(PETSC_ARCH)/bin/mpif90
#  CCE2 = $(PETSC_DIR)/$(PETSC_ARCH)/bin/mpicc

# Serial compiler names (set as appropriate for your computer)

# GNU Compiler Compilation
  FF = gfortran
  CC = gcc

# Intel compiler
# FF = ifort
# CC = icc

#------------------------------------------------------------------------
# Select optimization level to use for fortran and C
# (common options are given below)

# Gnu: gfortran/gcc compilers

# FFOPTFLAG = -O2 -Wall -J$(FEAPHOME8_5)/modules
# CCOPTFLAG = -O2 -Wall

  FFOPTFLAG = -g -O2 -Wall -J$(FEAPHOME8_5)/modules
  CCOPTFLAG = -g -O2 -Wall

# FFOPTFLAG = -g -Wall -J$(FEAPHOME8_5)/modules
# CCOPTFLAG = -g -Wall

# Intel: ifort/icc compilers

# FFOPTFLAG = -O2 -Warn all -J$(FEAPHOME8_5)/modules
# CCOPTFLAG = -O2 -Wall

# FFOPTFLAG = -g -O2 -Warn all -J$(FEAPHOME8_5)/modules
# CCOPTFLAG = -g -O2 -Wall 

# FFOPTFLAG = -g -Warn all -J$(FEAPHOME8_5)/modules
# CCOPTFLAG = -g -Wall

#------------------------------------------------------------------------
# Source Types (generally this is blank)

   FSOURCE   = 
   F90SOURCE =
   CSOURCE   = 

#------------------------------------------------------------------------
# Source Extender (generally this just 'f' and 'c')

   FEXT = f
   CEXT = c

   F90EXT = f90

#------------------------------------------------------------------------
# Other options to be used by the compiler (generally this is blank)

   FOPTIONS =
   COPTIONS =

#------------------------------------------------------------------------
# Set options to be used by the loader (Set to the location of your
# X11 librarys; leave the -lm at the end to load the math librarys).
# -ljepg is if you are building with the jpeg output option (see makefile)
# -mkl if you have the Intel compilers for BLAS etc.
# (use -L tags to help the loader locate your libraries if they are
#  in non standard locations, e.g. /sw/lib)

# (some common cases)
# Intel
# LDOPTIONS = -L/opt/local/lib -mkl -lX11 -lm
# LDOPTIONS = -L/opt/local/lib -mkl -lX11 -ljpeg -lm 
# LDOPTIONS = -L/usr/X11R6/lib -mkl -lX11 -ljpeg -lm

# GNU
# LDOPTIONS = -L/opt/local/lib -lX11 -lm
# LDOPTIONS = -L/opt/local/lib -lX11 -lblas -llapack -lm
# LDOPTIONS = -L/usr/X11R6/lib -lX11 -lblas -llapack ljpeg -lm
  LDOPTIONS = -L/usr/lib/x86_64-linux-gnu -lX11 -lblas -llapack -lm

# Loader options for FE2 build (assumes you are using openmpi, adjust as
# necessary)
# LDOPTIONSFE2 = -L/usr/local/lib $(LDOPTIONS)
# LDOPTIONSFE2 = -L$(PETSC_DIR)/$(PETSC_ARCH)/lib/openmpi $(LDOPTIONS)
  LDOPTIONSFE2 = -L/usr/lib/mpich/lib $(LDOPTIONS)
#------------------------------------------------------------------------
# What archiving to use
  AR = ar rv

#------------------------------------------------------------------------
# Archive name (no need to change)

 ARFEAP = $(FEAPHOME8_5)/Feap8_5.a
#------------------------------------------------------------------------
# IgA Archive name (no need to change)

  ARIFEAP = $(FEAPHOME8_5)/igafeap/libifeap8_5.a
#------------------------------------------------------------------------
```

## 编辑makefile

打开`ver85`下的`makefile`文件，将其中的

```
    (cd unix/jpeg; make archive)   # Can be 'jpeg' or 'nojpeg'
```

更改为

```
    (cd unix/nojpeg; make archive)   # Can be 'jpeg' or 'nojpeg'
```

完整的`makefile`文件如下所示：

```shell
# N.B.  It is necessary to modify 'makefile.in' before using make.

include $(FEAPHOME8_5)/makefile.in

CLEANDIRS = include include/integer4 include/integer8 maintain \
	program contact elements plot unix user main \
	packages/arpack packages/arpack/archive packages/blas \
	packages/lapack packages/meshmod program/memory unix/memory \
	parfeap parfeap/packages/arpack parfeap/partition modules

feap: archive
	(cd main; make feap)
	@@echo "--> Feap executable made <--"

archive:   
	(cd program; make archive)
	(cd elements; make archive)
	(cd plot; make archive)
	(cd unix; make archive)
	(cd unix/nojpeg; make archive)   # Can be 'jpeg' or 'nojpeg'
	(cd user; make archive)
	(cd unix/memory; make archive)
	(cd contact; make archive)
	@@echo "--> Feap Archive updated <--"

install: archive feap

clean:
	for i in $(CLEANDIRS); do (cd $$i; make clean); done
	@@echo "--> Feap cleaned <--"

arclean:
	if [ -f $(ARFEAP) ]; then rm $(ARFEAP); fi

fclean:
	rm -f feap
```

## 编译

如果不需要附加其他宏包，可直接在在完成所有的编辑之后，在`ver85`目录下执行命令

```
make install
```

这就可以直接完成所有的安装工作，直接在`ver85/main`目录下生成可执行文件`feap`。

或者，也可以分开执行。首先在`ver85`目录下运行命令

```
make archive
```

这将在当前目录下创建`Feap8_5.a`。

然后前往`ver85/main/`目录下执行命令

```
make feap
```

这就生成了可执行的FEAP程序`feap`。

对于可执行并行运算指令的FEAP程序，直接前往`ver85/parfeap`目录下执行命令

```
make install
```

这就在当前目录下生成了并行运算的FEAP程序`feap`。更详细的编译设定可编辑`ver85/parfeap`目录下的`makefile`文件。


# 延伸阅读

* [FEAP - University of California, Berkeley](http://projects.ce.berkeley.edu/feap/) / [FEAP User Forum](http://feap.berkeley.edu/forum/index.php) / [FEAP - A Finite Element Analysis Program](http://faculty.ce.berkeley.edu/sanjay/FEAP/feap.html)
* [Installation Videos - FEAP User Forum](http://feap.berkeley.edu/forum/index.php?topic=984.0)
* [FEAP Installation Manual: v8.5](http://projects.ce.berkeley.edu/feap/imanual85.pdf)
* [FEAP Parallel Manual: v8.5](http://projects.ce.berkeley.edu/feap/parmanual85.pdf)
* [PETSc/Tao: Home Page](http://www.mcs.anl.gov/petsc/) / [Download](http://www.mcs.anl.gov/petsc/download/index.html) / [Installation](http://www.mcs.anl.gov/petsc/documentation/installation.html)
