title: Linux下Python编译安装Scipy
date: 2015-3-07 21:00:00
categories: Python
tags:
  -  技术
  -  Python
description: SciPy是一个开源的Python算法库和数学工具包。在小石学长摸索了整整一天后终于在Linux下编译成功SciPy^_^
---

## SciPy简介
SciPy是一个开源的Python算法库和数学工具包。但是由于依赖一些fortran库在Linux下很难编译安装，下面便是我经过一天的摸索找到的安装方法，以飨大家。
## SciPy安装方法
### 编译BLAS
首先编译并静态链接Fortran库BLAS和LAPACK。
``` bash
mkdir -p ~/src/
cd ~/src/
wget http://www.netlib.org/blas/blas.tgz
tar xzf blas.tgz
cd BLAS

## NOTE: The selected Fortran compiler must be consistent for BLAS, LAPACK, NumPy, and SciPy.
## For GNU compiler on 32-bit systems:
#g77 -O2 -fno-second-underscore -c *.f                     # with g77
#gfortran -O2 -std=legacy -fno-second-underscore -c *.f    # with gfortran
## OR for GNU compiler on 64-bit systems:
#g77 -O3 -m64 -fno-second-underscore -fPIC -c *.f                     # with g77
gfortran -O3 -std=legacy -m64 -fno-second-underscore -fPIC -c *.f    # with gfortran
## OR for Intel compiler:
#ifort -FI -w90 -w95 -cm -O3 -unroll -c *.f

# Continue below irrespective of compiler:
ar r libfblas.a *.o
ranlib libfblas.a
rm -rf *.o
export BLAS=~/src/BLAS/libfblas.a
```
根据Linux版本执行g77/gfortran/ifort 5条命令中的一条，下面的LAPACK安装同样需要Fortran编译器并且应与编译BLAS库的编译器相同。

### 编译LAPACK
以gfortran编译器为例
``` bash
mkdir -p ~/src
cd ~/src/
wget http://www.netlib.org/lapack/lapack.tgz
tar xzf lapack.tgz
cd lapack-*/
cp INSTALL/make.inc.gfortran make.inc          # On Linux with lapack-3.2.1 or newer
make lapacklib
make clean
export LAPACK=~/src/lapack-*
```

如果Linux系统是64位那么应对make.inc进一步修改,在OPTS和NOOPT选项后加上-m64和-fPIC选项。修改后的make.inc例子如下：
``` bash
####################################################################
#  LAPACK make include file.                                       #
#  LAPACK, Version 3.5.0                                           #
#  November 2013                                                   #
####################################################################
#
SHELL = /bin/sh
#  
#  Modify the FORTRAN and OPTS definitions to refer to the
#  compiler and desired compiler options for your machine.  NOOPT
#  refers to the compiler options desired when NO OPTIMIZATION is
#  selected.  Define LOADER and LOADOPTS to refer to the loader and
#  desired load options for your machine.
#
FORTRAN  = gfortran
OPTS     = -O2 -frecursive -m64 -fPIC
DRVOPTS  = $(OPTS)
NOOPT    = -O0 -frecursive -m64 -fPIC
LOADER   = gfortran
LOADOPTS =
#
# Timer for the SECOND and DSECND routines
#
# Default : SECOND and DSECND will use a call to the EXTERNAL FUNCTION ETIME
#TIMER    = EXT_ETIME
# For RS6K : SECOND and DSECND will use a call to the EXTERNAL FUNCTION ETIME_
# TIMER    = EXT_ETIME_
# For gfortran compiler: SECOND and DSECND will use a call to the INTERNAL FUNCTION ETIME
TIMER    = INT_ETIME
# If your Fortran compiler does not provide etime (like Nag Fortran Compiler, etc...)
# SECOND and DSECND will use a call to the INTERNAL FUNCTION CPU_TIME
# TIMER    = INT_CPU_TIME
# If neither of this works...you can use the NONE value... In that case, SECOND and DSECND will always return 0
# TIMER     = NONE
#
#  Configuration LAPACKE: Native C interface to LAPACK
#  To generate LAPACKE library: type 'make lapackelib'
#  Configuration file: turned off (default)
#  Complex types: C99 (default)
#  Name pattern: mixed case (default)
#  (64-bit) Data model: LP64 (default)
#
# CC is the C compiler, normally invoked with options CFLAGS.
#
CC = gcc
CFLAGS = -O3
#
# LAPACKE has also the interface to some routines from tmglib,
# if LAPACKE_WITH_TMG is selected, we need to add those routines to LAPACKE
#LAPACKE_WITH_TMG = Yes
#
#  The archiver and the flag(s) to use when building archive (library)
#  If you system has no ranlib, set RANLIB = echo.
#
ARCH     = ar
ARCHFLAGS= cr
RANLIB   = ranlib
#
#  Location of the extended-precision BLAS (XBLAS) Fortran library
#  used for building and testing extended-precision routines.  The
#  relevant routines will be compiled and XBLAS will be linked only if
#  USEXBLAS is defined.
#
# USEXBLAS    = Yes
XBLASLIB     =
# XBLASLIB    = -lxblas
#
#  The location of the libraries to which you will link.  (The
#  machine-specific, optimized BLAS library should be used whenever
#  possible.)
#
BLASLIB      = ../../librefblas.a
LAPACKLIB    = liblapack.a
TMGLIB       = libtmglib.a
LAPACKELIB   = liblapacke.a
```
### 安装SciPy Package
执行 pip install scipy命令即可成功安装SciPy。
