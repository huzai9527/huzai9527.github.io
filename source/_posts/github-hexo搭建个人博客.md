---
title: github+hexo搭建个人博客
date: 2018-11-11 17:46:19
tags: github
---
### 1.创建的项目名默认为  **用户名.github.io**,创建时点击生成readme文件，方便后面添加说明
<img aligen="center" src="https://i.loli.net/2018/11/13/5beaa5e07e5a7.png">
### 2.在本地创建一个文件夹，我是在E盘创建的blog，推荐用vscode作为编辑器，在编辑器里面打开文件夹，打开Terminer
![使用vscode打开文件夹](https://i.loli.net/2018/11/13/5beaacf147c83.png)
### 3.使用hexo初始化文件夹，这一步会产生很多的hexo配置文件，我们先不管，先跑起来
![hexo初始化文件夹](https://i.loli.net/2018/11/13/5beaae3c7ee9d.png)
### 4.运行hexo server打开服务，看看本地能不能显示
![hexo server](https://i.loli.net/2018/11/13/5beab03a63524.png)
运行后访问url，如果看到如图就成功了
![运行效果](https://i.loli.net/2018/11/13/5beab09f5e2ab.jpg)
### 5.配置文件中填写git的配置信息，按照如下格式填写
![配置信息](https://i.loli.net/2018/11/13/5beab1fb7f83a.png)
### 6.打开文件夹，右键git bash here
![git bash here](https://i.loli.net/2018/11/13/5beab3362770b.png)
### 7.输入cd ~/.ssh，进入ssh文件夹
![ssh](https://i.loli.net/2018/11/13/5beab3e76e0c4.png)
### 8.配置git中的用户名和邮箱
![配置用户名](https://i.loli.net/2018/11/13/5beab93273357.png)
### 9.生成ssh密钥
![生成密钥](https://i.loli.net/2018/11/13/5beab95f2f069.png)
### 10.在github的项目中加入密钥
![添加密钥](https://i.loli.net/2018/11/13/5beab988e1bda.png)
### 11.测试密钥链接是否成功
![测试](https://i.loli.net/2018/11/13/5beab9fc045d7.png)
### 12.测试成功后再再编辑器中运行
     hexo clean
     hexo g
     hexo d
![4.png](https://i.loli.net/2018/11/13/5beaba9fb29d7.png)这样就算上传成功
### 13.访问你的博客，看到之前再本地运行的界面，就行了





  
