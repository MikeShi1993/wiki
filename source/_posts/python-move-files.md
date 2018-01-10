title: Python os模块简介
date: 2014-08-08 18:31:58
categories: Python
tags:
  -  技术
  -  Python
description: Python的os模块包含了很多很有用的关于操作文件和目录的函数。如果你希望你的程序能够与平台无关的话，这个模块是尤为重要的。即它允许一个程序在编写后不需要任何改动，也不会发生任何问题，就可以在Linux和Windows下运行，这也是他的强大之处。
---

## 概括

Python的os模块包含了很多很有用的关于操作文件和目录的函数。如果你希望你的程序能够与平台无关的话，这个模块是尤为重要的。即它允许一个程序在编写后不需要任何改动，也不会发生任何问题，就可以在Linux和Windows下运行，这也是他的强大之处。

### 常用函数
1.获得当前路径：os.getcwd()
``` python
>>> os.getcwd()
'C:\\Python34'
>>>
```
2.获得目录中的内容： os.listdir(path) 类似于windows下的dir命令，括号里的参数是你想列的目录。在windows下路径最好是双反斜杠，或者在路径前面加`r`。
``` python
>>> os.listdir('C:\\python34')
['basemap-wininst.log', 'DLLs', 'Doc', 'include', 'Lib', 'libs', 'LICENSE.txt', 'lxml-wininst.log', 'matplotlib-wininst.log', 'netCDF4-wininst.log', 'NEWS.txt', 'numpy-wininst.log', 'pandas-wininst.log', 'pyparsing-wininst.log', 'python.exe', 'pythonw.exe', 'qt.conf', 'README.txt', 'Removebasemap.exe', 'Removelxml.exe', 'Removematplotlib.exe', 'RemovenetCDF4.exe', 'Removenumpy.exe', 'Removepandas.exe', 'Removepyparsing.exe', 'Removerequests.exe', 'Removescipy.exe', 'requests-wininst.log', 'scipy-wininst.log', 'Scripts', 'tcl', 'Tools']
>>>
```
3.创建目录：`os.mkdir(path)`参数为要创建的目录所在的位置路径比如：
``` python
os.mkdir('E:\\book\\temp')
```
4.删除目录：`os.rmdir(path)`参数为要删除目录所在的路径，注意**此目录必须为空才能删除，否则出错。**
5.判断是否为目录 或者文件：`os.isdir(path)`，`os.isfile(path)`返回True则为目录或者文件，否则相反
6.更改当前工作目录：`os.chdir(path)`参数为要设的目录
``` python
>>> os.getcwd()
'C:\\Python34'
>>> os.chdir('C:\\Python34\\libs')
>>> os.getcwd()
'C:\\Python34\\libs'
>>>
```
7.删除文件`os.remove(path)`
``` python
>>>os.remove('C:\\python34\\test.py')
>>>
```
8.重命名文件或者目录: `os.rename(oldpath,newpath)`这个函数特别强大不仅可以改变文件名称还可以在**相同分区内**改变文件位置，十分方便。
``` python
>>>os.rename('C:\\python34\\1.py','C:\\2.py')
>>>
```
9.另外OS模块还有一个非常方便的方法，可以打开windows下的可执行程序，word文档啦，exe文件啦，只要是可执行的，都可以使用os的startfile打开，前提是你在系统中已经安装了相应的打开程序。比如：
``` python
>>>import os
>>>os.startfile('D:\\movie\\test.mkv')
```
然后就会执行你电脑里默认的视频播放程序打开test.mkv视频播放。很方便吧。

### 示例程序
我每回下载的视频文件都放在迅雷文件夹里面看完后每回都要手动进行分门别类的整理觉得很不爽，于是就利用Python花了2个小时编了一个小程序来自动帮我归档视频，下面是源代码：
``` python
import os
import re
import time
def get_list(old_list,pattern):
    new_list = []
    for i in old_list:
        if pattern.search(i):
            new_list.append(i)
    return new_list
#根据下载时间来判断是否归档该文件
def get_new_list(old_list):
    new_list = []
    for i in old_list:
        element_time = os.stat(i).st_mtime
        difference = (time.time() - element_time)/86400
        if difference >=4 :
            new_list.append(i)
    return new_list
#归档相关文件
def change_dir_list(old_list):
    for i in old_list:
        if 'The.Last.Ship' in i:
            old_list.remove(i)
            os.rename(i,r'H:/电影/末日孤舰/'+i)
            print(i.ljust(35)+'移至H:/电影/末日孤舰')
        elif 'Tyrant' in i:
            old_list.remove(i)
            os.rename(i,r'H:/电影/Tyrant/'+i)
            print(i.ljust(35)+'移至H:/电影/Tyrant')
        elif '24.S09' in i:
            old_list.remove(i)
            os.rename(i,r'H:/电影/24h/'+i)
            print(i.ljust(35)+'移至H:/电影/24h')
        elif 'The.Flash' in i:
            old_list.remove(i)
            os.rename(i,r'H:/电影/The Flash/'+i)
            print(i.ljust(35)+'移至H:/电影/The Flash')
        else:
            os.rename(i,r'H:/电影/'+i)
            print(i.ljust(35)+'移至H:/电影')
    return old_list
def change_dir(list_dir):
    pattern = re.compile(r'.*\.(mkv|mp4|rmvb|ass|srt)$') #正则匹配视频和字幕文件
    os.chdir(list_dir)
    old_list = os.listdir()
    new_list = get_list(old_list,pattern)
    move_list = get_new_list(new_list)
    new_move_list = change_dir_list(move_list[:])
    return len(move_list)
if __name__ == "__main__":
    a = time.time()
    b = change_dir(r'H:\迅雷下载')
    dir_list = [i for i in os.listdir() if os.path.isdir(i)]
    for i in dir_list:
        c = change_dir('H://迅雷下载//'+i)
        b = b+c
    print('本次共移动%s部电影' %b)
    print(time.time()-a)
    input('按Enter键退出')
```
自从用了这个小脚本，帮我节省了好多整理文件的时间，果然是科技改变生活啊。
