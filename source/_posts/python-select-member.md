title: Python消息统计
date: 2014-08-07 18:55:25
categories: Python
tags: 
  -  技术
  -  Python
description: Python, 是一种面向对象、解释型计算机程序设计语言，Python语法简洁而清晰，具有丰富和强大的类库,码代码效率非常高。这是我用Python编写的统计发言数的小脚本。
---
这是我统计QQ群成员发言数的Python代码，需要依赖[pandas](http://pandas.pydata.org/)库,下载后解压缩文件，然后cd到目标文件夹，执行以下命令：
``` bash
python setup.py install
```
然后pandas库就可以使用了，这是我统计发言数的源代码：
``` python
from pandas import Series, DataFrame
import pandas as pd
def get_name(txt_list):
    name_list =[]
    new_name_list =[]
    for i in txt_list:
        a = i.split(' ')
        if len(a)==3:
            if len(a[1]) ==8 and len(a[0]) ==10:
                    name_list.append(a[2])
    for i in name_list:
        if i[0]== '【':
            new_name_list.append(i[4:])
        else:
            new_name_list.append(i)
    return new_name_list
if __name__ == "__main__":
    file_dir = r'C:\Users\46474_000\Desktop\一帮逗比欢乐多.txt'
    f = open(file_dir,'r',encoding= 'utf-8').readlines()[8:]
    f = [i.strip() for i in f if i.strip() != '']
    f = f[6:]
    name_list = Series(get_name(f))
    a= name_list.value_counts()
    for i in a.index:
        print(i,a.ix[i])
```
只要修改一下file_dir将目录指向导出的QQ消息记录就可以运行了。