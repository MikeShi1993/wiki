title: 初学MongoDB
categories: Python
tags: 
  -  技术
  -  Python
  -  MogoDB
  -  数据分析
description: MongoDB,是目前非常流行的一种非关系型数据库(NoSql),数据存储方式十分灵活。MongoDB很好的实现了面向对象的思想(OO思想),在MongoDB中 每一条记录都是一个Document对象。Mongo DB最大的优势在于所有的数据持久操作都无需开发人员手动编写SQL语句,直接调用方法就可以轻松的实现CRUD操作。
---
今天初学MongoDB，感觉比关系型数据库好上手多了，而且比较符合人类思维也不用担心Sql注入之类的问题，其实本来不想换数据库的，这都是被WeRobot逼的，谁叫它只支持NoSql数据库啊，T^T，不过上手感觉还不错，比Mysql简单多了，半小时就上手了，就是Mysql向MongoDB数据迁移比较麻烦，出现了很多问题，下面是我找到的解决办法，就记录下来备忘。

首先在安装目录bin文件夹下shift+左键打开cmd，执行以下命令：
``` bash
mongod --logpath D:/mongodb/logs/mongodb.log --logappend
--dbpath D:/mongodb/data/db --directoryperdb --serviceName MongoDB --install
```

该命令行指定了日志文件：/logs/MongoDB.log，日志是以追加的方式输出的。数据文件目录：/data/db，并且参数--directoryperdb说明每个DB都会新建一个目录。Windows服务的名称：MongoDB；
以上的三个参数都是可以根据自己的情况而定的。最后是安装参数：--install，与之相对的是--remove，以后就可以在cmd下用命令net start MongoDB和net stop MongoDB来启动和停止MongoDB了，也可以在本地服务中看到。