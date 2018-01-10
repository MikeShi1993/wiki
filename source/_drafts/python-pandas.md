title: 十分钟上手Python数据分析模块pandas
date: 2014-08-10 20:37:05
categories: Python
tags: 
  -  技术
  -  Python
  -  数据分析
description: pandas是一个旨在对结构化数据提供快速、灵活的分析和表达的模块。他是一个非常强大的数据分析模块，其作者目标是让它成为世界上最好的数据分析模块，没有之一→_→
---
## 概括
这是一个对pandas模块的简单介绍，从而让新手能够对它快速上手。详细的请参考[*Cookbook*](http://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook)
## 使用方法
### 导入
通常我们这样导入模块：
``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
### Series和DataFrame的创建
1.通过列表传值来创建一个索引为整数的Series