title: Hexo搭建教程(2)
categories: hexo
tags:
  - 技术
description: Pacman是一款为Hexo打造的一款扁平化，有着响应式设计的主题。本站正是使用了该主题，同时你也可以访问Demo查看效果。主题源码托管在Github上。
date: 2014-08-07 13:11:30
---
## 安装指南
Pacman是一款为Hexo打造的一款扁平化，有着响应式设计的主题。本站正是使用了该主题，同时你也可以访问Demo查看效果。主题源码托管在Github上。
### 安装
``` bash
$ git clone https://github.com/A-limon/pacman.git themes/pacman
```
**Pacman需要安装Hexo 2.4.5** 或以上版本 请先升级您的Hexo程序，再启用此主题。

### 启用
修改你的博客根目录下的`config.yml`配置文件中的`theme`属性，将其设置为`pacman`。

### 更新
``` bash
cd themes/pacman
git pull
```
**请先备份你的`_config.yml` 文件后再升级**

## 配置指南
Pacman主题提供了丰富的配置属性，配置文件`_config.yml位`于主题根目录下。配置文件中已经包含了详细的英文注释，所以下面就用中文进行说明。

### 属性

```  yaml
##### Menu
menu:
  Home: /
  Archives: /archives 
#### Widgets
widgets: 
- category
- tag
- rss
#### RSS
rss: 
#### Image
imglogo:
  enable: true
  src: /img/logo.svg 
  favicon: /img/favicon.ico 
  apple_icon: /img/pacman.jpg
#### Author Avatar Picture
author_img_enable: true
dataURI: false
author_img_data: 
author_img: /img/author.jpg
#### Font
ShowCustomFont: true  
#### Toc
toc:
  article: true 
  aside: true 
#### Fancybox
fancybox: true 
#### Author information
author:
  google_plus: 
  intro_line1: 
  intro_line2: 
  weibo: 
  twitter: 
  github: 
  facebook: 
  tsina: 
#### Comment
duoshuo: 
  enable: false        
  short_name: 
#### Share button
jiathis:
  enable: false  
  id: 
  tsina:
#### Analytics
google_analytics:
  enable: false
  id:
  site:
#### Custom Search
google_cse: 
  enable: false
  cx:
```