title: Hexo搭建教程(1)
categories: hexo
tags:
  - 技术
description: "hexo是一个基于Node.js的静态博客程序,出自台湾大学生 tommy351 之手，其编译上百篇文字只需要几秒。"
date: 2014-08-07 09:48:25
---
## 概括

一直想搭建一个博客，但是自己从头搭建一个实在是太费心力，直到我看见了**hexo**，hexo出自台湾大学生 tommy351 之手，是一个基于Node.js的静态博客程序，其编译上百篇文字只需要几秒。hexo生成的静态网页可以直接放到GitHub Pages，BAE，SAE等平台上。先看看tommy是如何吐槽Octopress的 →＿→ [Hexo颯爽登場](http://zespia.tw/blog/2012/10/11/hexo-debut) 。
## 安装
### 准备工作
1. [安装node.js](http://nodejs.org/)
2. [安装git](http://git-scm.com/)

### 安装hexo
``` bash
$ npm install -g hexo
```
## 配置
### 初始化
然后，执行init命令初始化hexo到你指定的目录
``` bash
$ hexo init <folder>
$ hexo install
```
也可cd到你指定的目录然后init
### 生成静态页面
cd 到你的init目录，执行如下命令，生成静态页面至hexo\public\目录。
``` bash
$ hexo g
```
### 本地启动
执行如下命令，启动本地服务，进行文章预览调试。
``` bash
$ hexo s
```
浏览器输入http://localhost:4000 就可以看到效果。