title: Python通过xlwt模块编辑xls文件
date: 2014-08-09 21:01:29
categories: Python
tags: 
  -  技术
  -  Python
description: xlwt是Python一个编辑xls文件的模块，它生成的文件能很好的与Excel2000/2003/OpenOffice/Gnumeric兼容，并且完美支持unicode。通过xlwt模块Excel表格可以在任何平台生成，不需要依赖Excel或者COM服务器。
---

## xlwt模块简介
xlwt是Python一个编辑xls文件的模块，它生成的文件能够很好的与大部分主流电子表格办公软件如Excel2000/2003/OpenOffice/Gnumeric等兼容，并且完美支持unicode。通过xlwt模块可以使Excel表格在任何平台生成，不需要依赖Excel或者COM服务器。
### 下载地址
[xlwt-future 0.8.0](https://pypi.python.org/pypi/xlwt-future/0.8.0)
### 安装方法
下载后解压缩文件，然后cd到目标文件夹，执行以下命令即可：
``` bash
python setup.py install
```
### 简单使用
1.导入xlwt
``` python
import xlwt
```
2.创建Workbook
``` python
file = xlwt.Workbook() #注意这里的Workbook首字母是大写
```
3.新建一个sheet
``` python
table = file.add_sheet('sheet name')
```
4.写入数据table.write(行,列,value)
``` python
table.write(0,0,'test')
```
5.保存文件
``` python
file.save('demo.xls')
```
6.使用style调整表格样式
``` python
style = xlwt.XFStyle() # 初始化样式
font = xlwt.Font() #为样式创建字体
font.name = 'Times New Roman' #选择字体
font.bold = True  #是否加粗
style.font = font #为样式设置字体
table.write(0, 0, 'some bold Times text', style) # 使用样式
font.height = 500 #设置高度
al = xlwt.Alignment()
al.horz = xlwt.Alignment.HORZ_CENTER #设置水平居中
al.vert = xlwt.Alignment.VERT_CENTER #设置垂直居中
al.wrap = xlwt.Alignment.WRAP_AT_RIGHT #设置文字可以换行
style.alignment = al
```
7.合并表格file.write_merge(row_1,row_2,col_1,col_2,value,style)
``` python
file.write_merge(1,2,3,5,'value',style) #合并从第1行到第2行第3列到第4列的表格
```
### 例子
更详细的例子请参考python编译xlwt模块后，解压缩文件夹下../xlwt/examples里面的代码。