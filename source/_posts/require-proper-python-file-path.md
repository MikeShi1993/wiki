title: 获取Python脚本所在目录的正确方法
date: 2015-11-17 19:22:26
categories: Python
tags: 
  -  技术
  -  Python
---
## 以前的方法
如果是要获得程序运行的当前目录所在位置，那么可以使用os模块的`os.getcwd()`函数。

## 正确的方法
但以上这些其实都不是脚本文件所在目录的位置,获取Python脚本所在目录实际应使用`os.path.split(os.path.realpath(__file__))[0]`其中`__file__`虽然是所在.py文件的完整路径，但是这个变量有时候返回相对路径，有时候返回绝对路径，因此 还要用`os.path.realpath()`函数来处理一下。

